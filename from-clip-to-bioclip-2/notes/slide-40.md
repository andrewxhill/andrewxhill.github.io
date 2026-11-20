# Slide 40: Further training on organism photos raised the share of species photos named correctly from 45.5% to 90.6%.

TO TAKE AWAY

Much of what looked forgotten was still inside BioCLIP 2: it still tells vehicles apart from example photos (86.7%), and its patch tokens still tell alive animals from dead ones (89.6%).

Three methods combined the two skills with no retraining: average the two models’ weights, read BioCLIP 2’s patch tokens, or exchange two blocks.

If you have a general model and a model trained from it, try all three on your own pair, and test a skill the training never targeted.

**Method notes**

The closing slide restates the naming gain, the retained knowledge and the three methods.

- What was measured
  - The slide summarises the explainer and reports no new measurement.
- Numbers
  - Further training raised species naming from 45.5% to 90.6%.
  - Named from example photos, vehicles fell 4.8 points.
  - BioCLIP 2's patch tokens tell alive from dead at 91.0% at block 24.
  - BioCLIP 2's summary token reads 85.7% at the output.
  - The three methods are weight averaging, reading patch tokens and exchanging two blocks.
- Not shown
  - The results come from one pair of models and may not hold for another pair.
- Scope of the measurements
  - The slide lists four limits on what the measurements cover.
  - The slide states the limits of the study and reports no new measurement.
  - Every number comes from one starting model and one model trained from it.
  - Alive or dead was measured on 1,323 photos of 115 species.
  - The skill outside biology was naming ten classes of vehicle.
  - Attention was checked on eight photos.
  - No second pair of models was measured.
  - Skills other than the two tested may behave differently.
  - Classifiers fitted to each block's tokens show what can be read at that block.
  - Block swaps show what changes when blocks are exchanged.
  - Neither the classifiers nor the swaps show why training produced the step at block 23.
  - On all eight photos BioCLIP 2 took more of its attention from a quarter of the patches.
  - The attention concentration figures were computed once and not independently checked.

**Speaker notes**

Three things to take with you. One: training the starting model further on organism photos took species naming from 45.5% to 90.6%. Two: part of what looked forgotten was still there. Named from example photos, vehicles fell only 4.8 points, and its patch tokens tell alive from dead at 89.6% through the same final steps where the summary token reads 85.7%. Three: you can get more of both skills out of the two finished models with no training run: average the weights, read the patch tokens, or exchange blocks 23 and 24. If you have a general model and something trained from it, try all three. Pick a skill the training never aimed at and measure it before and after.
