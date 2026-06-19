# Game Systems & Mechanics

## Wanted System (Heat)
- **Heat Metric**: Actions like running over pedestrians, carjacking, hitting police cars, or destroying vehicles generate `heat`. 
- **Stars**: The HUD displays up to 5 stars, calculated as `Math.floor(heat / 100)`. Higher stars increase the maximum number of simultaneous police units chasing the player.
- **Cooling Off**: If the player avoids the police for 5 seconds (`lastSeenT`), the heat begins to passively decrease. Hiding out of sight will eventually clear the wanted level.

## Damage & Combat
- **Vehicular Combat**: Ramming other cars deals damage based on relative velocity. If a car's health drops low enough, it catches fire and eventually explodes.
- **Explosions**: Deal area-of-effect damage, blowing up nearby cars, killing pedestrians, and damaging the player. An exploding car will forcefully eject the player if they are driving it.
- **Particles**: Generates sparks, smoke, and fire particles during collisions and damage states.

## Audio Synthesizer
Instead of loading external sound files, Sunset City features a built-in procedural audio engine using the Web Audio API.
- **Engine Sounds**: Uses filtered sawtooth and square oscillators. Pitch scales dynamically with vehicle speed.
- **Tire Skids**: Uses filtered white noise.
- **Sirens**: Triangle oscillator modulating pitch based on time.
- **Impacts & Explosions**: Generated using exponential frequency envelopes (thumps) and low-pass filtered noise bursts.

## Rendering
- **Main View**: Renders the world from a top-down perspective, translating and scaling the canvas context to center the camera on the player.
- **Parallax Effect**: Building roofs and tree canopies are drawn with a slight offset relative to the camera position, creating a convincing pseudo-3D parallax effect without WebGL.
- **Minimap**: Renders the map to an offscreen 196x196 canvas upon boot. During the game loop, this static map is blitted to the minimap canvas, and dynamic entities (police, player) are drawn on top.
- **Vignette & Grade**: Handled via a CSS overlay (`#vig`) to provide atmosphere and color grading.

## Controls
- `WASD` / `Arrow Keys`: Walk / Drive
- `Space`: Handbrake / Drift
- `Shift`: Sprint (On Foot)
- `E`: Enter / Exit / Jack Vehicle
- `M`: Mute Audio
