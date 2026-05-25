# Quantifying overlap on the pitch circle

**Date:** 2026-05-25
**Context:** Side-thread from the pitch-circle diagram. Goal: a scalar that measures how much two (or more) voices' Gaussian-smeared partials overlap.

## Setup

Each voice $v$ contributes a density function on the octave circle:

$$f_v(\theta) = \sum_{n=1}^{N} \frac{1}{\sqrt{n}} \cdot \exp\!\left( -\frac{d(\theta,\,\theta_{v,n})^2}{2\sigma^2} \right)$$

where:
- $\theta_{v,n} = \big(\log_2(r_v \cdot n) \bmod 1\big) \cdot 2\pi$ — angle of voice $v$'s $n$-th partial
- $r_v$ — voice's fundamental ratio (e.g. $1$, $5/4$, $3/2$)
- $\sigma$ — Gaussian width (the slider)
- $d(\cdot, \cdot)$ — shortest angular distance on the circle
- $\frac{1}{\sqrt{n}}$ — perceptual amplitude proxy

This is exactly what's rendered on the combined wheel.

## The natural measure: pairwise inner product

$$C = \sum_{i<j} \int_0^{2\pi} f_i(\theta)\, f_j(\theta)\, d\theta$$

For each pair of voices, multiply their density functions pointwise and integrate around the circle; sum across the pairs.

**Interpretation:** how much spectral energy the auditory periphery shares between voices. At every angle where two voices both have density, the product is large; where only one (or none) has density, the product is zero. Integrating gives a single "shared-partial energy" number.

**Limits:**
- $C \to \text{max}$ when partials align perfectly (every coincidence contributes)
- $C \to 0$ when voices are spectrally disjoint
- Scale-dependent on $\sigma$ (wider $\sigma$ → larger overlaps → larger $C$)

This is the standard textbook proxy for **sensory consonance**.

## Cousin 1: integral of the squared stack

$$S = \int_0^{2\pi} \left( \sum_v f_v(\theta) \right)^{\!2} d\theta$$

Expanding the square:

$$S = \underbrace{\sum_v \int f_v^2 \, d\theta}_{\text{intrinsic per-voice}} \;+\; \underbrace{2 \sum_{i<j} \int f_i \, f_j \, d\theta}_{2C}$$

So $S = (\text{constant in }\sigma) + 2C$ — equivalent to $C$ up to an additive constant. Cheap to compute: one pass over exactly the data that's already being rendered.

## Cousin 2: Plomp-Levelt roughness

The *opposite* signal — measures **dissonance** (beating between near-but-not-coincident partials) rather than consonance.

For each cross-voice partial pair $(p_a, p_b)$, a roughness kernel $g(\Delta f, f_{\min})$ peaks when their frequency difference is roughly 25% of a critical band, decaying to zero at unison and at large separations.

$$R = \sum_{a \in i,\, b \in j,\, i \neq j} A_a A_b \cdot g\!\left( |f_a - f_b|,\, \min(f_a, f_b) \right)$$

Doesn't reduce to a circular integral; needs the actual frequencies (not just angles) to set the critical bandwidth. More perceptually accurate but more work to compute.

Sethares' dissonance curves use this.

## For the diagram

$C$ is the right one to wire into the live read-out: cheap (a single sum of products), directly tied to the visual stack, monotonic with what the eye reads as "more colour overlap = more consonance." Could show $C$ as a number under the combined wheel that updates on every toggle / $\sigma$ change.

## Refinement: skeleton vs colour fit

The symmetric sum

$$C = \int f_R\, f_3\, d\theta \;+\; \int f_R\, f_5\, d\theta \;+\; \int f_3\, f_5\, d\theta$$

treats all three voices on equal footing. But for the question we actually care about — "how does the third lock into an R+P5 frame, and does m3 differ from M3?" — the $\int f_R\, f_5$ term is **identical** for both major and minor (same R, same P5).

So the major-vs-minor difference reduces to:

$$\Delta C = \int (f_R + f_{P5}) \cdot (f_{M3} - f_{m3})\, d\theta$$

The R-P5 overlap is dead weight in that comparison. The part that *changes* is:

$$C_{\text{colour}} = \int f_{\text{third}} \cdot (f_R + f_{P5})\, d\theta$$

This isolates "how well does the third lock into the perfect-fifth skeleton."

### Two read-outs worth considering

| Read-out | Formula | What it tells you |
|---|---|---|
| Full pairwise | $C = \sum_{i<j} \int f_i f_j\, d\theta$ | Overall consonance, any voice selection |
| Skeleton consonance | $C_{\text{skel}} = \int f_R\, f_{P5}\, d\theta$ | How locked-in the R + P5 frame is on its own |
| Colour fit | $C_{\text{colour}} = \int f_{\text{third}} \cdot (f_R + f_{P5})\, d\theta$ | How the third fits the frame — m3 vs M3 contrast lives entirely here |

For triad analysis, the skeleton + colour-fit pair tells a much clearer story than the single full-pairwise number, because it factors out the constant background and exposes the part that the chord quality actually controls.
