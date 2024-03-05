> [!important]  
> Certain entities, such as pollinators and flowers, can interact positively when they are in close proximity. Pollinators can collect pollen from flowers, helping with their reproduction, while flowers provide nectar as a reward.  

  

Testing URL: [https://rau.lol/sdlgame/?flowers](https://rau.lol/sdlgame/?flowers)

I already have a simple system to place flowers in the world, but they are purely decoration right now. I have been wanting to add butterflies, but I think there are some features I’ll need to create in order to properly implement them. Ideally these features might be applicable to other creatures down the road.

  

**Butterfly Design**

These would be simple entities consisting of 2 rectangles for the wings, a thin rectangle for the body and 2 lines protruding from the top of the body.

![[Untitled 2.png|Untitled 2.png]]

This allows for the butterfly to be procedural. I can make the wings different colors/sizes. Same for the body and antenna. I can also add subtle movements to each part over time as the butterfly moves.

I don’t want to try rotating the rectangles or using polygons at the moment, so for now simple animations will have to do.

As the butterfly flies it will bob up and down slowly and its wings will increase/decrease in size to simulate the wings getting closer/further as they flap.

  

**Interactions**

I can think of 2 states a butterfly will always be in at a given time:

- In Flight
- Idle

Each of these has a number of different situations in which the state might occur:

- In Flight
    - Heading towards target
    - Flying from target
- Idle
    - Reached target originally heading towards
    - Reached distance away form target originally fleeing
    - Dead

  

**Scenario**

1. The butterfly starts in the "Idle" state.
    1. A timer begins while at idle that will trigger it to choose a new target after it runs out
2. It is in the "Idle" state and heading towards its target (after timer runs out).
3. The butterfly transitions to the "In Flight" state while heading towards the target.
4. While in flight, the butterfly reaches the target and transitions back to the "Idle" state.
    1. idle timer begins

  

**Considerations**

I may need to rethink my custom rendering solution for different entity types

[[Custom Entities Rendering method]]

Custom interactions are going to be difficult and will need to think more on the possible implementations.

  

> Image credits: Microsoft Bing Image Creator
> 
> Prompt: _A lush field of flowers covered in butterflies, with the bright sun reflecting on their wings. The camera is at the flower canopy level, and the image has a tilt-shift effect._