# Slide 23: Through block 22, BioCLIP 2’s summary token scores higher than the starting model’s at telling alive from dead

QUESTION 2 · ALIVE OR DEAD, BLOCK BY BLOCK

91.9%

Accuracy at telling alive from dead when a classifier reads BioCLIP 2’s summary token at block 22, against 90.5% for the starting model. BioCLIP 2 is ahead at every block measured, from block 2 to block 22.

If the loss were gradual, BioCLIP 2 would fall further behind at each block. After 22 blocks it is ahead. Its final output scores 85.7%, so all of the fall happens after block 22.

Horizontal axis: image block, then the two final steps, rescaling (norm) and projection (output). Each point: a fresh alive-or-dead classifier trained on that block’s summary token and tested on 1,323 photos of 115 species held out from it.

**Method notes**

The slide shows alive-or-dead accuracy read from each model's summary token up to block 22.

- What was measured
  - The slide reports alive-or-dead accuracy read from the summary token at each block.
  - The chart shows blocks 18 to 22 and leaves blocks 23 onward for the next slide.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
- Method
  - A fresh logistic regression classifier is fitted to the tokens read at each stage.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Scores are balanced accuracy within each species, averaged over the 115 species.
  - Both models receive the same input, with the OpenAI pixel scaling.
- Numbers
  - At block 22 BioCLIP 2's summary token scores 91.9%, 91.85% unrounded.
  - At block 22 the starting model's summary token scores 90.5%, 90.48% unrounded.
  - BioCLIP 2's summary token scores 91.37%, 92.35%, 92.98%, 92.99% and 91.85% at blocks 18 to 22.
  - The starting model's summary token scores 89.08%, 89.26%, 89.14%, 89.23%, 90.48% at 18 to 22.
  - BioCLIP 2 is ahead at every block measured, from block 2 to block 22.
  - At block 2 the summary tokens score 79.15% in BioCLIP 2 and 78.16% in the starting model.
  - BioCLIP 2's final output scores 85.7%, 85.68% unrounded.
- Uncertainty
  - Blocks 2 to 16 were read at even-numbered blocks only.
  - No interval is reported here for the gap between the two models at a single block.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show what happens after block 22.
  - A classifier reading shows what can be recovered, not what the model itself uses.
- Definitions
  - On the axis, norm is the final rescaling step and output is the final projection.

**Speaker notes**

Same method, now for alive or dead, and zoomed in on the last seven blocks. The right-hand side of the chart is empty on purpose. Up to block 22 the model trained on biology is the better of the two at this: 91.4 against 89.1 at block 18, 93.0 against 89.1 at block 20, 91.9 against 90.5 at block 22. In the earlier even-numbered blocks it is ahead as well. So the guess of a gradual loss is wrong. Whatever takes BioCLIP 2 down to 85.7% at the output has not happened yet, with two blocks to go.
