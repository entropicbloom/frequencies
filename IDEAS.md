# Ideas: future directions

Running list of things to explore. Add freely; prune when done or abandoned.

## Pitch-circle diagram

*The three numbered ideas below were suggested by Claude (Opus 4.7), 2026-05-25, in response to "is there anything you'd like to steer this project toward?"*

### 1. Audibility (Web Audio)

Synthesize the actual partial stack when a voice is clicked. Each Gaussian peak becomes a sine at that pitch with amplitude 1/√n (or whatever the chosen envelope is).

- σ maps onto something physical: either the **decay envelope** of each harmonic (sharp partial = narrow time-domain pulse = wide spectrum) or **unison detuning spread** (multiple sines per partial, normally distributed around the centre frequency).
- Closes the eye–ear loop: the user can *hear* the difference between m3 and M3 in the same UI where they see it.
- Makes "minor sounds sad" testable rather than asserted.

### 2. The comma made visible

Overlay 12-TET partial positions as faint grey ticks behind the just-intonation Gaussians.

- The ~14-cent angular gap at the M3 (between the JI 5/4 and the ET 400-cent third) would visually *be* the syntonic comma.
- Other commas show up too: P5 (Pythagorean vs ET ~2¢), m3 (~16¢), m7, etc.
- Teaches *why* equal temperament is a compromise: the diagram answers a question before you ask it.

### 3. Scalar dissonance read-out

Integrate Σ (stack_height)² around the ring → one number per chord configuration.

- Compare major / minor / dom7 / m7♭5 / cluster quantitatively.
- Visual and number always synced: toggle a voice and watch both update.
- Could also expose Σ stack_height (linear) for a "total energy" reading vs Σ height² (concentration).
- Bonus: plot the number as a function of σ to see how "dissonance" depends on perceptual sharpness.

## Backlog (not yet specified)

- Other chord families with their own coincidence fingerprints (dom7, dim, aug, m7♭5, sus2/4)
- Non-octave tunings (Bohlen-Pierce, Wendy Carlos alpha/beta/gamma) on the same wheel
- A "scrolling" mode: ring rotates while audio plays, partials light up as they sound
- Comparison view: two chords side by side with their stacked-Gaussian profiles
