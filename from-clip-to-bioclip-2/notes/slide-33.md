# Slide 33: BioCLIP 2 tells alive from dead 4.1 points better with the starting model’s blocks 23 and 24 swapped in

QUESTION 3 · SWAPPING BLOCKS 23 AND 24

Teal cells are BioCLIP 2’s, violet cells the starting model’s. With blocks 23 and 24 replaced, the alive-or-dead score rises to 89.74% (95% interval on the change +1.66 to +6.38) and naming falls 3.21 points. In the last row the starting model loses 1.6 points, less than the 4.2 BioCLIP 2 loses at its own block 23.

Final steps: rescaling and projection. Naming: 223 species. Alive or dead: 1,323 photos of 115 held-out species.

**Method notes**

The slide tests small swaps around blocks 23 and 24 between the two models.

- What was measured
  - The slide reports naming and alive-or-dead accuracy for BioCLIP 2 with small swaps.
  - Each row copies named parts from one model into the other and changes nothing else.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - Image-model weights are held fixed during scoring.
  - The alive-or-dead classifier is refitted to each hybrid model's output.
  - The five-photo naming references are rebuilt for each hybrid model.
  - Every model in the comparison is given the OpenAI pixel scaling.
  - The final steps are the rescaling step and the projection after block 24.
- Numbers
  - BioCLIP 2 unchanged names 90.63% and scores 85.68% at alive or dead.
  - With the starting model's blocks 23 and 24, BioCLIP 2 names 87.42% and scores 89.74%.
  - The two-block swap changes naming by -3.21 points and alive or dead by +4.06 points.
  - With the starting model's block 24 only, BioCLIP 2 names 89.45% and scores 88.56%.
  - The block-24 swap changes naming by -1.2 points and alive or dead by +2.9 points.
  - With the starting model's final steps only, BioCLIP 2 names 91.04% and scores 86.03%.
  - With blocks 23, 24 and the final steps swapped, BioCLIP 2 names 87.22% and scores 90.51%.
  - The starting model with BioCLIP 2's blocks 23 and 24 names 40.60% and scores 89.79%.
  - The starting model loses 1.6 points at alive or dead with BioCLIP 2's blocks 23 and 24.
  - The starting model unchanged names 43.21% and scores 91.41% on the same tests.
- Uncertainty
  - The +4.06 point gain has a 95% interval of +1.66 to +6.38 points.
  - The -3.21 point naming change has a 95% interval of -3.89 to -2.57 points.
  - With C fixed at 1 the two-block gain is 3.93 points, interval 1.12 to 6.57.
  - Vehicle naming changes by +0.58 points with the two-block swap, interval -0.82 to +1.88.
  - No interval is reported for the other rows of the table.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The swap does not show why blocks 23 and 24 lower the alive-or-dead reading.
  - The 1.6 points lost in the starting model are fewer than the 4.2 lost inside BioCLIP 2.
  - Blocks 23 and 24 therefore do not carry the whole effect into another model.

**Speaker notes**

Question 2 found that most of the loss happens at block 23. So make the smallest swap that covers it: leave 22 blocks of BioCLIP 2 alone and replace only blocks 23 and 24 with the starting model’s. Alive-or-dead rises from 85.68% to 89.74%. The interval on that gain is +1.66 to +6.38. Naming falls 3.21 points, from 90.63% to 87.42%. Read the other rows as checks. Block 24 alone raises alive-or-dead accuracy by 2.9 points and lowers naming by 1.2. The final steps alone give 91.04% and 86.03%, so they are not where the fix is. Blocks 23 and 24 with the final steps give 87.22% and 90.51%. The last row runs the swap the other way. Put BioCLIP 2’s blocks 23 and 24 into the starting model and it loses 1.6 points of alive-or-dead, and its naming goes from 43.21% to 40.60%. That is less than the 4.2 points those blocks cost inside BioCLIP 2, so the two blocks do not carry the whole effect with them.
