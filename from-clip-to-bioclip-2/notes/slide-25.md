# Slide 25: BioCLIP 2’s patch tokens still tell alive from dead at block 24: 91.0%, against 87.0% from its summary token

QUESTION 2 · THE PATCH TOKENS

91.0%

Accuracy at telling alive from dead read from the average of BioCLIP 2’s 256 patch tokens at block 24.

After block 23 BioCLIP 2 still holds what is needed to tell alive from dead. The summary token, the one token that becomes the output, carries less of it.

Solid lines: summary token. Dotted lines: average of the 256 patch tokens, one per patch of the photo. The same 1,323 photos and kind of classifier for all four lines. After block 24 come the final rescaling (norm) and projection (output).

**Method notes**

The slide compares alive-or-dead readings from the summary token and from the patch tokens.

- What was measured
  - The slide reports alive-or-dead accuracy read two ways at each stage in both models.
  - One reading uses the summary token and the other the average of the 256 patch tokens.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
  - The same 1,323 photos are used for all four lines.
- Method
  - A fresh logistic regression classifier is fitted to the tokens read at each stage.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Scores are balanced accuracy within each species, averaged over the 115 species.
  - Both models receive the same input, with the OpenAI pixel scaling.
  - The patch reading at a numbered block is a simple average of its 256 patch vectors.
  - At the output, each patch vector is rescaled, then averaged, then projected.
- Numbers
  - BioCLIP 2's patch tokens score 91.0% at block 24, 91.00% unrounded.
  - BioCLIP 2's summary token scores 87.0% at block 24, 87.02% unrounded.
  - BioCLIP 2's patch tokens score 91.57% at block 22 and 91.16% at block 23.
  - BioCLIP 2's summary token scores 91.85% at block 22 and 87.65% at block 23.
  - The starting model's patch tokens score 90.56%, 91.03% and 91.77% at blocks 22 to 24.
  - The starting model's summary token scores 90.48%, 90.63% and 91.36% at blocks 22 to 24.
  - After rescaling BioCLIP 2's patch tokens score 90.88% and after projection 89.83%.
  - After rescaling the starting model's patch tokens score 91.93%, after projection 90.68%.
- Uncertainty
  - At the output the patch reading beats the summary by 4.14 points, interval 1.75 to 6.45.
  - No interval is reported for the gap between the two readings at block 24 itself.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show why the summary token carries less than the patch tokens.
  - A classifier reading shows what can be recovered, not what the model itself uses.

**Speaker notes**

Now use the second way of reading a block. The dotted teal line is the average of BioCLIP 2’s 256 patch tokens. It does not drop at block 23. It reads 91.6 at block 22, 91.2 at 23 and 91.0 at 24, right alongside the starting model. So BioCLIP 2 has not lost the ability to see whether an animal is alive. The patch tokens still hold it. What changed is what the summary token collects from them. From block 23 on that token reports alive-or-dead less well, and the patch tokens beside it do not. In the starting model the two lines stay together all the way to the end.
