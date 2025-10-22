Thinking about how I can separate the engine and the "game" from my game project.
The engine is written in C++, but uses HTML/JS for UI and other features like sound/file loading/scene editing.
"games" are just config files that get converted into JSON and passed to C++. JS is used to fetch the config before passing to c++, this allows me to update configs and test without needing to compile. 

The engine technically doesn't need JS for the frontend, I am able to compile to desktop, but I would have to decouple all JS related things.
Right now the engine is all-in-one engine+game+editor. If I wanted to make a standalone game I could simplify to just the engine+game. There would not be an option to load configs at runtime, but multiple configs/scenes could be included in the build and available to that instance of the game.
Also I could add an import feature, I know I can update the engine at runtie, so loading a new scene should be doable.

Locked doors should show a symbol/text
 - right now the door color changes, but if I want a texture that won't work

Make the cursor a hand/grab when the cursor is within a certain radius around the player and hovered on an interactable/hoverable entity
 - should not be able to interact with things beyond the player interaction radius.
   - but hover is fine at any distance for things like tooltip info

Need a way to carry things and move them around
 - maybe also something like a rope to pull things and connect things
Dragging also needed

Locked portals should not by default destroy the key entity
 - make it optional

proximity audio 

A way to make entities "stick" to each other
 - like for moving entities, like a 'weld' tool in gmod
 - but also just logically, like to link 2 entities in some way.
   - right now this is done through entity references stored within components
     - but I want a more generalized way, so entities are grouped directly without a component
       - but also a "Group" component might also work
         - vector of entities an entity is grouped to
         - or vector of groups? So like A and B can be grouped, A and C as well, but not B and C. So just because B and C is in A's list does not mean C is in B's or B in C.
 - for now most important to just get blueprint entities to "stick"
   - the "blueprint" will be considered the group
   - will need a toggle to enable/disable so I can still move individuls
 - will be useful when destroying a grouped entity like a tree along with the trunk colliding entity.

"FLoating" on water is important to implement

interior entities still need work visually, maybe scrap the auto-wall render and just manually place entities for walls and build a bp.

need a component or some kind of logic to switch scenese other than shift+>/<

need to re-add the optional zoom limits

LIGHTING

slides in the editor is using the wrong parsing format
 - its trying to use id:value,id:value
 - valid is just value,value,value

consider resetting each scene when its started, right now it retains whatever state the registry was in before switching

redbean doesn't auto-resolve index.html, causes 404 on /web
 - might need to rethink overall web-layout
Need a scene explorer on the web
 - or in game
 - consider a way to compile a full scene or multiple

Thinking about stairs and ladders and multifloor buildings
 - it works now via portals and interiors, but visually it is not obvious that 3 stacked interiors are a 3 story building
 - a staircase or ladder or elevator etc would just be a normal portal, on collision the entity will be transferred to the next room
   - but visually might want to do a bit more
     - stairs/ladders the entity will be "locked" into a single movement like ladders straight up and down, stairs at an angle, and only on reaching the end of the visual will the portal activate
     
Try to get the js side of the engine orthogonal to the c++ side. Create a general API so that it can be compiled for desktop too.
 - but also just as a way to slim down the engine in general. Web will still be the primary target