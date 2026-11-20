# Slide 24: Between blocks 22 and 23, BioCLIP 2’s summary token becomes 4.2 points worse at telling alive from dead

QUESTION 2 · BLOCK 22 TO BLOCK 23

−4.2 points

BioCLIP 2’s summary token at telling alive from dead: 91.85% at block 22, 87.65% at block 23 (95% interval −6.38 to −2.33). That is 4.2 of the 6.2 points lost between block 22 and the output. Another 1.7 is lost at the final projection.

71.9% → 87.3%

Species naming from the same token at the same step. It rose more one block earlier, from 42.5% to 71.9%, while the alive-or-dead score moved from 93.0% to 91.9%.

Horizontal axis: image block 18 to 24, then the two final steps, rescaling (norm) and projection (output). Shaded: the step from block 22 to block 23. Over that step the starting model changes by +0.15 points at telling alive from dead and its species naming rises 15 points.

**Method notes**

The slide shows the drop in BioCLIP 2's alive-or-dead reading between blocks 22 and 23.

- What was measured
  - The top panel reports alive-or-dead accuracy read from the summary token at each stage.
  - The bottom panel reports species naming read from the same summary token.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
  - The naming panel uses 3,734 photos of 223 species, including all 1,323 test photos.
- Method
  - A fresh logistic regression classifier is fitted to the tokens read at each stage.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Scores are balanced accuracy within each species, averaged over the 115 species.
  - Both models receive the same input, with the OpenAI pixel scaling.
  - Naming uses five example photos per species, averaged over 20 draws.
- Numbers
  - BioCLIP 2's summary token scores 91.85% at block 22 and 87.65% at block 23.
  - The change from block 22 to 23 is -4.20 points, shown as -4.2.
  - BioCLIP 2 loses 6.2 points from block 22 to the output, 91.85% to 85.68%.
  - From block 23 to block 24 BioCLIP 2's summary token changes by -0.63 points.
  - From block 24 to the rescaling step BioCLIP 2's summary token changes by +0.35 points.
  - At the final projection BioCLIP 2's summary token changes by -1.69 points, shown as 1.7.
  - BioCLIP 2's summary token scores 87.02% at block 24 and 87.37% after rescaling.
  - BioCLIP 2's naming from the same token rises from 71.9% to 87.3%, 71.91% and 87.26%.
  - One block earlier BioCLIP 2's naming rose from 42.5% to 71.9%, 42.46% and 71.91%.
  - Over that earlier step the alive-or-dead reading moved from 93.0% to 91.9%.
  - The starting model changes by +0.15 points at alive or dead from block 22 to 23.
  - The starting model's naming rises 15 points at block 23, from 20.7% to 35.7%.
- Uncertainty
  - The 95% interval on BioCLIP 2's change from block 22 to 23 is -6.38 to -2.33 points.
  - With C fixed at 1 the same change is -4.92 points, interval -7.23 to -2.78.
  - The starting model's change of +0.15 points has an interval of -1.31 to +1.44.
  - The change from block 23 to 24 has an interval of -2.84 to +1.58 points.
  - The change at the final projection has an interval of -3.37 to -0.04 points.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show why the drop happens at block 23.
  - A rise in naming does not by itself explain the drop, as the earlier step shows.
  - A classifier reading shows what can be recovered, not what the model itself uses.
- Definitions
  - On the axis, norm is the final rescaling step and output is the final projection.

**Speaker notes**

Here is the rest of the chart. Top panel: BioCLIP 2’s line runs above the starting model’s, and then between block 22 and block 23 it drops 4.2 points in a single step and does not recover. The interval on that drop is −6.4 to −2.3, and it is still there with the classifier’s settings held fixed. It is not the whole loss. From block 22 to the output BioCLIP 2 loses 6.2 points: 4.2 here, 0.6 from block 23 to 24, and 1.7 at the final projection, with a small rise at the rescaling step in between. Bottom panel, same token: naming goes from 71.9% to 87.3% at this step. But naming rose more one block earlier, from 42.5% to 71.9%, and alive-or-dead only moved from 93.0% to 91.9% then. So a jump in naming does not by itself bring a drop of this size. The starting model makes a 15-point naming jump at block 23 too, from 20.7% to 35.7%, and its alive-or-dead score does not move.
