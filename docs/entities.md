# Entity Systems

Entities are represented as simple JavaScript objects within global arrays (`cars`, `peds`, `particles`, `decals`).

## The Player
- **State**: Can be on foot or in a vehicle.
- **Movement**: 
  - On foot: 8-way movement, walking and sprinting capabilities.
  - In vehicle: Standard acceleration, braking, reversing, and steering mechanics. Includes a grip/drift model where lateral velocity is preserved longer when the handbrake is applied.
- **Interactions**: Pressing `E` near a car allows the player to enter it. If the car is occupied, a carjacking occurs (driver is ejected and flees).
- **Health**: Regenerates slowly when out of combat. Reaching 0 health triggers a "Wasted" state, respawning the player without their car and resetting heat.

## Pedestrians (`peds`)
- **Behavior**: Spawn dynamically around the player. They wander aimlessly until frightened.
- **Reactions**: They enter a `flee` state when hearing fast cars, witnessing explosions, or being near a player with a wanted level.
- **Vulnerability**: Can be run over by cars or killed by explosions, triggering visual particle/decal effects and raising the player's wanted level.

## Traffic (`cars` with `mode='traffic'`)
- **Spawning**: Dynamically spawn out of the player's immediate sight but within a certain radius.
- **Navigation**: They move along defined lanes (`rc(k)` road centerlines +/- lane offsets) and make randomized turn decisions at intersections.
- **Obstacle Avoidance**: Raycast-style obstacle detection slows them down to avoid rear-ending other cars, hitting pedestrians, or running over the player.
- **Despawning**: Removed from the game once they drive too far from the player.

## Police (`cars` with `mode='police'`)
- **Spawning**: Spawn dynamically outside the player's view based on the current Wanted Level (`stars()`).
- **AI**: Aggressively track the player's position. They attempt to ram the player's vehicle or run over the player when on foot. 
- **Fleeing**: If the player loses their wanted level, existing police cars switch to a flee state and drive away to despawn.
