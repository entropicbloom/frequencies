# Pitch circles and harmonic priors

*2026-05-24*

A follow-on to the [musical-geometries](2026-05-22-musical-geometries.md) session. Same question — *what mathematical object captures the felt difference between major and minor?* — pushed further into octave-wrapped geometry and predictive-processing framings.

## What's in here

New / modified diagrams:

- **`diagrams/prime-lattice.html`** — a printable 5-limit lattice diagram of the (3, 5) plane. Built fresh at the start of the session, then extended in two ways:
  - Added a 4th column so the major-scale 2nd (D = 9/8) sits on the visible grid alongside the other six scale tones.
  - Replaced note-name labels (C, D, E, …) with **interval abbreviations** (R, M2, M3, P4, A4, P5, M6, m2, m3, m6, m7, M7). The lattice now reads key-agnostically: it's a map of *intervals*, not of one specific key.

- **`diagrams/pitch-circle.html`** — new. Octave-wrapped chromagram: log₂(frequency) mod 1 wraps each frequency to an angle on a circle. Two circles side by side (major vs minor). Each chord tone draws an inward "comb" of 16 partials — tick length and opacity shrink with partial number. Behind the ticks, **coincidence wedges** in warm accent mark every angle where 2+ voices share a partial, with width proportional to coincidence strength; triple coincidences are tagged `×3`.

## The arc of the conversation

We started with a small question — *why primes?* — and unpacked the lattice step by step from frequency ratios, through octave equivalence, to prime coordinates and triad-as-L-shape. Then four threads emerged.

### 1. Lattice distance vs harmonic-series distance

The lattice has its own step-count metric; the harmonic series has another. The classic compromise is **Tenney distance = log(p · q)**, which roughly captures both "how high in the series do we climb?" and "how spread are the two notes within the series?" — but these are genuinely separable measures. 9/8 vs 9/5 was the worked example: same max-harmonic (9), very different spread (1 vs 4), different lattice step-counts (2 vs 3), different Tenney heights (72 vs 45). No single number is "the" distance — each captures a different psychoacoustic intuition.

### 2. The major scale on the (3, 5) plane

Six of the seven diatonic scale tones sit inside the 3×3 patch. D = 9/8 needs two fifths (two steps along the 3-axis), so the diagram was extended one column. With that extension, **primes 2, 3, 5 alone generate every interval in the standard major and minor scales** — the definition of 5-limit just intonation. Caveat: 5-limit gives multiple paths to most notes (e.g., D = 9/8 *or* 10/9, differing by the syntonic comma); real music sometimes needs both.

### 3. The major / minor asymmetry, again

The lattice has perfect mirror symmetry — flip (b, c) → (−b, −c) and major triads turn into minor triads, indistinguishably. But the harmonic series has *no* mirror symmetry; it only multiplies upward. So the same operation that's free on the lattice (negative exponent of 5, say) is costly in the series:

- Major triad = **4 : 5 : 6** — three adjacent low partials of one fundamental.
- Minor triad = **10 : 12 : 15** — non-adjacent higher partials, with 11/13/14 missing.

This is Partch's **otonal vs utonal** distinction. Negative exponents in the lattice correspond exactly to going "down" the harmonic series of a higher fundamental — which forces a re-expression with all-positive (but larger) integers when you anchor at the bass. The lattice treats + and − symmetrically; the harmonic series does not. That single asymmetry is the root cause.

### 4. Predictive processing: two views of what the brain is doing

A natural reframing in terms of generative models. The brain's strong prior is *"incoming pitched sound = harmonic series of some fundamental(s)."* Two ways the prior can fit:

- **View 1 — one series, chord embedded.** Hypothesise a single hidden fundamental; the chord notes are its partials. Major fits cleanly (4, 5, 6 — adjacent); minor fits badly (10, 12, 15 with gaps the model predicts and the input doesn't deliver). Corresponds to the **`harmonic-alignment.html`** diagram. Stumpf / Terhardt tradition: virtual pitch, harmonic-template matching.

- **View 2 — three series, partials align.** Each chord tone is its own source with its own overtone stack; the brain measures how much those stacks coincide. Lower coincidence partials = more fusion. Corresponds to **`harmonic-overlap.html`**. Helmholtz / Plomp-Levelt tradition: consonance as the absence of beating between partials.

These are **not mathematically equivalent**. View 1 over-predicts — for real chords, partials of the virtual fundamental like 7f, 9f, 11f, 13f aren't physically there. View 2 only predicts what each note's overtone series actually generates, which is a sparser subset. Both views rank major as more consonant than minor (correlated predictions), but they're different generative models with different error profiles. Modern psychoacoustics treats both as contributing transducers.

Subtle: View 1's over-prediction is *worse* for minor than for major (because 10:12:15 leaves bigger gaps than 4:5:6), so it discriminates the two more sharply. View 2 distinguishes them more weakly — by the height of the lowest pairwise coincidence rather than by gap structure.

## The pitch circle (what the new diagram contributes)

The pitch circle is a direct geometric translation of View 2 with octave equivalence built in. log₂(f) mod 1 collapses the helix of pitch onto a single octave-circle; each note's partials become a fixed pattern of angles on it.

What it makes visible:

- For the **major triad**, the three voices land on five reinforced angles (R+P5 strong, R+M3 strong, R+M3+P5 triple at M7, and two thinner pair-coincidences at M2 and A4).
- For the **minor triad**, only two angles are reinforced — both triples (R+m3+P5 at P5, R+m3+P5 at M2). The m3 fundamental itself sits at ~94° with *no other voice's low partials reaching it*. It contributes the chord's character but is geometrically isolated.

The asymmetry is now legible as **band density**: major has many medium bands distributed around the circle; minor has fewer, more concentrated bands and a lonely m3.

## Where it lands

The 22nd's session ended with the integer-ratio lattice as the structural skeleton of pitch relations, and a list of physical/psychophysical transducers through which the brain might be sensitive to that skeleton. Today's session sharpened two of those transducers into rival generative models, showed they're related but not identical, and built a geometric object (the pitch circle) that visualises one of them — View 2 — with the octave-folding built in.

What's still open from the 22nd is also still open now: whether the *qualia* of brightness vs shadow reduces to harmonic-template fit, partial-alignment density, or something neither captures. The pitch circle is a better picture of the second; it doesn't settle the question.
