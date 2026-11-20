# Slide 37: The word “forgetting” covers three different results in BioCLIP 2

LOOKING BACK · FORGETTING

A model trained further on new data usually gets worse at things it could do before; researchers call this catastrophic forgetting. In BioCLIP 2 the scores fell in three different ways.

93.0% → 45.8%

Named from words, most vehicle photos now get a wrong name

The ten vehicle names became less alike: average similarity fell from 0.774 to 0.662. Every name measured scores higher on every vehicle photo than before. The right name rose least, so “rocket”, “streetcar” or “tank” often scores highest.

91.5% → 86.7%

Named from example photos, the same vehicle photos score 4.8 points lower

Each photo is compared with five example photos of each vehicle, with no words involved. The image side still separates the ten vehicles.

85.7%

89.6%

BioCLIP 2’s patch tokens still tell alive animals from dead ones

The starting model scores 91.4%. BioCLIP 2’s summary token, the one token that becomes the output, scores 85.7%. Its patch tokens score 89.6% passed through the same last steps of the model, and 91.0% read straight after block 24.

In two of the three, the model still held most of what the lower score suggested was lost.

**Method notes**

The slide separates three different results that the word forgetting could cover.

- What was measured
  - The slide sets three earlier results side by side and reports no new measurement.
- Data
  - The vehicle results use 1,000 CIFAR-100 photos of ten vehicle classes.
  - The alive-or-dead results use 1,323 photos of 115 held-out species.
- Numbers
  - Named from words, vehicle photos fall from 93.0% correct to 45.8%.
  - The average similarity between the ten vehicle names fell from 0.774 to 0.662.
  - Each of the four names measured scores higher on every vehicle photo in BioCLIP 2.
  - Named from five example photos, the same vehicles fall from 91.5% to 86.7%.
  - The fall from example photos is 4.8 points, 4.77 unrounded.
  - The starting model scores 91.4% at alive or dead.
  - BioCLIP 2's summary token scores 85.7% at alive or dead.
  - BioCLIP 2's patch tokens score 89.6% passed through the same final steps.
  - BioCLIP 2's patch tokens score 91.0% read straight after block 24.
- Uncertainty
  - The patch-token gain of 3.9 points has a 95% interval of 1.6 to 6.2 points.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show which side of the model causes the wrong vehicle names.
  - Three results from one pair of models do not describe forgetting in general.
- Definitions
  - Catastrophic forgetting is a model getting worse at earlier skills after further training.

**Speaker notes**

Forgetting is the word everyone reaches for. Train a model further and it usually gets worse at old things; the literature calls that catastrophic forgetting. But look at what we measured, because it is three different things. First, vehicles named from words: 93.0% down to 45.8%. The names did not blur into each other. They became less alike, 0.774 to 0.662, and what goes wrong is that every name scores higher on every photo and rocket, streetcar or tank often comes out on top. Second, the same photos named from five example photos, with no words: 91.5% to 86.7%. Third, alive or dead: the summary token reads 85.7%, but the patch tokens of the same model give 89.6% through the same final steps, and 91.0% read directly at block 24. So in two of the three cases the score fell and most of the knowledge was still there.
