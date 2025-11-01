# Performance One-Pager

To summarize, my game is a 2D action platformer inspired by games like Mega Man X and Gunvolt. The main gameplay loop revolves around getting to the end of a level while optimizing time, damage taken, and combos to achieve a rank. Responsive inputs and a consistent framerate are essential to games like this, as the player is constantly moving and weaving to achieve optimal play. Three performance concerns that I have are maintaining a consistent framerate, collision detection, and object pooling.

## Framerate

Framerate must remain consistent so that the player’s immersion isn’t broken. Having jitters when performing precise jumps, dashes, or attacks is very noticeable. To solve any issues that may arise from this, games like Celeste and Mega Man X utilize a fixed-timestep system, where no matter the strength of the machine they are running on, the game’s logic runs on a constant time interval that doesn’t change. For example, whether a game is running at 60 or 120 fps, inputs and simulation are updated at 60 fps to keep things consistent. In my own game, I don’t think framerate will be an issue, but implementing consistent game logic based on a constant time interval would help ensure stability as well.

## Collision Detecting

Games like this often have situations where many hitboxes must be accounted for—coming from the player, enemies, or the level itself. To make sure this doesn’t affect performance, games like Celeste and Hollow Knight divide a level or section into different cells so that any object checks collisions only within the section it’s in. This technique, called spatial partitioning, drastically reduces the number of comparisons that need to happen. In my game, I plan to section off areas of my levels into different rooms. Some will be traditional one-screen rooms while others will scroll, but this approach in general will reduce CPU usage.

## Object Pooling

A similar problem arises with frequent object creation and destruction. Things like enemies, projectiles, and hitboxes are constantly being spawned and removed. If not handled correctly, this could result in memory fragmentation, where space isn’t reused efficiently, and garbage collection spikes. The common solution in 2D action games is object pooling, where instead of constantly spawning and removing objects, many games spawn a pool of these objects at the start and reuse them depending on the gameplay situation. This avoids new allocations, improves framerate, and prevents runtime stalls. I’d like to implement this with enemies, enemy projectiles, and player projectiles in my game, as those are the main objects I could see being constantly spawned and removed.
