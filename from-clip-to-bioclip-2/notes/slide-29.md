# Slide 29: Two-thirds of BioCLIP 2’s fall at telling alive from dead happens at block 23, in its summary token

QUESTION 2 · ANSWER

On all eight photos checked, BioCLIP 2’s summary token at block 24 takes a larger share of its attention from its 64 most-attended patches: 89.6% against 73.4% on the junco photo.

Late in the network, and mostly in one step

The loss does not build up block by block. Through block 22, BioCLIP 2 tells alive from dead better than the starting model at every block measured. Between blocks 22 and 23 its summary token falls 4.2 points, of the 6.2 it loses between block 22 and the output.

Only in the summary token

At block 24 the average of the patch tokens scores 91.0% and the summary token 87.0%. BioCLIP 2 still holds the information. The token that becomes the output carries less of it.

Block 23’s weights changed like any late block’s

Nothing in the weights marks block 23 out. The fall appears only when each block’s tokens are tested.

**Method notes**

The slide answers question 2: most of the fall happens at block 23, in the summary token.

- What was measured
  - The slide gathers the results of question 2 and reports no new measurement.
- Data
  - The block readings use 1,323 photos of 115 species held out from the classifiers.
  - The attention shares were checked on eight photos.
  - The weight comparison uses the stored weights of the two models.
- Numbers
  - BioCLIP 2's summary token falls 4.2 points between blocks 22 and 23, 4.20 unrounded.
  - BioCLIP 2 loses 6.2 points between block 22 and the output, 91.85% to 85.68%.
  - The 4.2 points are about two-thirds of the 6.2 points.
  - The final projection takes another 1.7 points, 1.69 unrounded.
  - At block 24 the patch tokens score 91.0% and the summary token 87.0%.
  - On the junco BioCLIP 2 puts 89.6% of block-24 attention on its 64 most-attended patches.
  - On the junco the starting model puts 73.4% on its own 64 most-attended patches.
  - The weight change in blocks 23 and 24 is spread over 514 and 506 directions.
  - A random change of the same size is spread over 523 directions.
- Uncertainty
  - The 95% interval on the fall at block 23 is -6.38 to -2.33 points.
  - The 89.6% and 73.4% attention shares were computed once and not independently checked.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show why training produced the step at block 23.
  - Naming rose more at block 22 than at block 23 without a comparable drop.
  - The starting model gains naming at block 23 without losing alive-or-dead accuracy.

**Speaker notes**

So the guess was wrong. The loss is not spread across 24 blocks. Two-thirds of it happens at one block, in one of 257 tokens, and the final projection takes another 1.7 points. The patch tokens still score 91%. What we have not shown is why. Naming rises at block 23, but it rose more at block 22 without a comparable drop, and the starting model gains naming at block 23 without losing anything. If the loss were everywhere, the only fix would be to train again. A loss that sits in the last two blocks and in one token leaves other things to try.
