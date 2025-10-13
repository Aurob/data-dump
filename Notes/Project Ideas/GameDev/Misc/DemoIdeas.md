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