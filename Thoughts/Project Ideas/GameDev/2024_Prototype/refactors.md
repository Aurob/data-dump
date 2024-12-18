I understand your preference for a more functional approach. While classes can provide benefits in terms of encapsulation and organization, we can certainly improve the code without heavily relying on them. Let's focus on enhancing the existing structure with modern C++ features and best practices. Here are some suggestions:

1. Use smart pointers:
Replace raw pointers with std::unique_ptr or std::shared_ptr where appropriate. For example, in the main function:


```74:77:src/main.cpp
    SDL_Window *mpWindow = SDL_CreateWindow("Untitled",
        SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED,
        width, height,
        SDL_WINDOW_OPENGL | SDL_WINDOW_RESIZABLE | SDL_WINDOW_SHOWN);
```


Can be replaced with:

```cpp
auto mpWindow = std::unique_ptr<SDL_Window, decltype(&SDL_DestroyWindow)>(
    SDL_CreateWindow("Untitled", SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED,
    width, height, SDL_WINDOW_OPENGL | SDL_WINDOW_RESIZABLE | SDL_WINDOW_SHOWN),
    SDL_DestroyWindow
);
```

2. Use std::array for fixed-size arrays:
Replace C-style arrays with std::array. For example:

```cpp
std::array<GLfloat, 2> cursorPos = {0, 0};
std::array<GLfloat, 2> globalCursorPos = {0, 0};
std::array<GLfloat, 2> offsetValue = {0.0f, 0.0f};
std::array<GLfloat, 2> toplefttile = {0.0f, 0.0f};
```

3. Use constexpr for compile-time constants:

```cpp
constexpr float defaultGSV = 16.0f;
constexpr float defaultMoveSpeed = 1.15f;
```

4. Use std::optional for values that might not exist:

```cpp
std::optional<entt::entity> _player;
```

5. Use structured bindings:
In the mainloop function:


```176:178:src/main.cpp

    Position &playerPos = registry.get<Position>(_player);
    Shape &playerShape = registry.get<Shape>(_player);
```


Can be replaced with:

```cpp
auto [playerPos, playerShape] = registry.get<Position, Shape>(_player);
```

6. Use std::function for callbacks:
Instead of using function pointers, use std::function for more flexibility:

```cpp
std::function<void(int, SDL_Event*)> EventHandler;
```

7. Use namespaces to organize related functions:
Create namespaces for related functionality, e.g.:

```cpp
namespace Systems {
    void updateMovement(entt::registry& registry) { /* ... */ }
    void updateCollisions(entt::registry& registry) { /* ... */ }
    // ...
}
```

8. Use RAII for resource management:
Create RAII wrappers for SDL and OpenGL resources. For example:

```cpp
struct SDLInitializer {
    SDLInitializer() {
        if (SDL_Init(SDL_INIT_VIDEO) < 0) {
            throw std::runtime_error("SDL could not initialize!");
        }
    }
    ~SDLInitializer() { SDL_Quit(); }
};
```

9. Use std::chrono for time management:
Replace SDL_GetTicks() with std::chrono:

```cpp
auto lastTime = std::chrono::high_resolution_clock::now();
// ...
auto currentTime = std::chrono::high_resolution_clock::now();
deltaTime = std::chrono::duration<float>(currentTime - lastTime).count();
lastTime = currentTime;
```

These changes maintain a functional approach while leveraging modern C++ features for improved safety and readability. They also help in resource management and type safety without introducing unnecessary complexity.


Multithreading could be beneficial in several areas of your game engine, particularly for computationally intensive tasks that can be parallelized. Here are some potential areas for multithreading and how to implement them:

1. Entity Updates:
   The `updateFrame` function (lines 102-141 in src/main.cpp) contains several update functions that could potentially be parallelized:


```132:139:src/main.cpp
    // Update entity movement and interactions
    updateTeleporters(registry);
    updateInteractions(registry);
    updateShapes(registry);
    updateLinkedEntities(registry);
    updateMovement(registry);
    updateCollisions(registry);
    updatePositions(registry);
```


   These updates could be split across multiple threads, each handling a subset of entities. You could use std::thread or a thread pool to manage this.

2. Collision Detection:
   The `updateCollisions` function in Systems.hpp could benefit from multithreading, especially if you have many entities:


```73:86:include/Systems.hpp
void updateCollisions(entt::registry &registry)
{
    // Sort so that the player is checked first
    registry.sort<Collidable>([&](const entt::entity lhs, const entt::entity rhs)
                              { return registry.all_of<Player>(lhs) && !registry.all_of<Player>(rhs); });

    auto collidables = registry.view<Collidable, Position, Shape, InView>();

    for (auto entity : collidables)
    {
        if (!registry.all_of<Movement>(entity))
            continue;

        bool hasLink = registry.all_of<Linked>(entity);
```


   You could divide the entities into chunks and process each chunk in a separate thread.

3. Shader Compilation:
   In the `loadGL1` function (GLUtils.hpp), shader compilation could be parallelized:


```112:159:include/GLUtils.hpp
void loadGL1(GLuint &shaderProgram, std::string program_name)
{

    // Create and compile vertex shader
    GLuint vertexShader = glCreateShader(GL_VERTEX_SHADER);
    glShaderSource(vertexShader, 1, &shaderGLSLMap[program_name][0], NULL);
    glCompileShader(vertexShader);
    
    // Check for vertex shader compilation errors
    GLint success;
    GLchar infoLog[512];
    glGetShaderiv(vertexShader, GL_COMPILE_STATUS, &success);
    /
```


   Compile vertex and fragment shaders in separate threads.

4. Texture Loading:
   The texture loading process in the `js_loaded` function (src/main.cpp) could be parallelized:


```152:155:src/main.cpp
        // Load textures from textureMap
        for(auto& [name, src] : textureMap) {
            printf("Loading texture: %s\n", src.c_str());
            textureIDMap[name] = loadGLTexture(shaderProgramMap["texture"], src.c_str());
```


   Load multiple textures concurrently using a thread pool.

5. JSON Processing:
   In JSUtils.hpp, the JSON processing could be multithreaded if you're dealing with large JSON structures:


```126:140:include/JSUtils.hpp

        if (js_json.contains("Entities") && js_json["Entities"].is_array())
        {
            for (auto &_el : js_json["Entities"])
            {
                // entt::entity entity;
                if (_el.is_object())
                {
                    bool is_player = false;

                    // Check if the Player key is present
                    if (_el.contains("Player") && _el["Player"].is_boolean())
                    {
                        is_player = _el["Player"];
                    }
```


   Process different sections of the JSON in parallel.

To implement multithreading, you could use C++11's threading capabilities. Here's a basic example of how you might implement a thread pool for entity updates:

```cpp
#include <thread>
#include <vector>
#include <queue>
#include <functional>
#include <mutex>
#include <condition_variable>

class ThreadPool {
public:
    ThreadPool(size_t numThreads) {
        for (size_t i = 0; i < numThreads; ++i) {
            workers.emplace_back([this] {
                while (true) {
                    std::function<void()> task;
                    {
                        std::unique_lock<std::mutex> lock(queueMutex);
                        condition.wait(lock, [this] { return !tasks.empty() || stop; });
                        if (stop && tasks.empty()) return;
                        task = std::move(tasks.front());
                        tasks.pop();
                    }
                    task();
                }
            });
        }
    }

    template<class F>
    void enqueue(F&& f) {
        {
            std::unique_lock<std::mutex> lock(queueMutex);
            tasks.emplace(std::forward<F>(f));
        }
        condition.notify_one();
    }

    ~ThreadPool() {
        {
            std::unique_lock<std::mutex> lock(queueMutex);
            stop = true;
        }
        condition.notify_all();
        for (std::thread &worker : workers) {
            worker.join();
        }
    }

private:
    std::vector<std::thread> workers;
    std::queue<std::function<void()>> tasks;
    std::mutex queueMutex;
    std::condition_variable condition;
    bool stop = false;
};

// Usage in updateFrame:
ThreadPool pool(std::thread::hardware_concurrency());

pool.enqueue([&]{ updateTeleporters(registry); });
pool.enqueue([&]{ updateInteractions(registry); });
pool.enqueue([&]{ updateShapes(registry); });
pool.enqueue([&]{ updateLinkedEntities(registry); });
pool.enqueue([&]{ updateMovement(registry); });
pool.enqueue([&]{ updateCollisions(registry); });
pool.enqueue([&]{ updatePositions(registry); });
pool.enqueue([&]{ updateOther(registry); });
```

Remember to handle synchronization carefully when implementing multithreading, especially when multiple threads might access or modify the same data. Use mutexes or atomic operations where necessary to prevent race conditions.