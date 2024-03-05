> [!important]  
> If objects reside on different layers and cannot interact with one another, organize them in such a way that collisions are only checked between objects on the same layer.  

  

This is probably the quickest way I can improve performance by at least a little bit.

I have a Type component I can give to entities that will indicate to the engine to generate and render them in certain ways based on their Type. tree, flower, grass, rock are types I have right now.

Some of these types have collisions (tree & rock), others don’t. The rocks need to be collided with by other entities including other rocks, but trees don’t need to check for collisions with other trees (*maybe eventually, but not important now).

I have a Collidable component and I have a Moveable component, so maybe I could simply check for collisions as such:

1. If an entity has both the Collidable and Moveable components, we should check for collisions with all other Collidable entities.
2. If an entity has the Collidable component but not the Moveable component, we only need to check for collisions with other Collidable entities that also lack the Moveable component.

> [!important]  
> We use these rules to optimize collision detection and improve performance. By selectively checking collisions based on the presence or absence of the Moveable component, we can reduce unnecessary calculations and focus only on relevant entities. This helps to streamline the collision detection process and make it more efficient.