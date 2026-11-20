# Slide 18: Averaging the two models’ weights gives 72.7% on species naming and 92.2% at telling alive from dead

QUESTION 1 · MIXING THE TWO MODELS’ WEIGHTS

72.7%

Species naming at a mix of 0.5, where every weight is the average of the two models’ values. That is 62% of the way from 43.2% to 90.6%.

92.2%

Telling alive from dead at the same mix; the starting model scores 91.4%. Past 0.5 it falls: 90.1% at 0.75, 86.3% at 0.9.

Naming vehicles from words is 92.8% correct at this mix.

Horizontal axis: BioCLIP 2’s share of every weight (0 is the starting model). 223 species; 1,323 photos of 115 held-out species.

**Method notes**

The slide puts the naming curve and the alive-or-dead curve on the same axes.

- What was measured
  - The slide reports species naming and alive-or-dead accuracy at seven weight mixes.
  - The highlighted point is the mix of 0.5, where every weight is the two models' average.
- Data
  - The naming test uses 3,734 iNaturalist test photos of 223 species.
  - The alive-or-dead test uses 1,323 photos of 115 held-out species.
- Method
  - Naming uses five example photos per species, averaged over 20 draws.
  - Alive or dead uses a logistic regression classifier tested on held-out species.
  - Every mix on both curves is given the OpenAI pixel scaling.
- Numbers
  - At a mix of 0.5 naming is 72.7%, 72.65% unrounded.
  - The naming value at 0.5 is 62% of the way from 43.2% to 90.6%.
  - At a mix of 0.5 alive-or-dead accuracy is 92.2%, 92.23% unrounded.
  - The starting model scores 91.4% on alive or dead, 91.41% unrounded.
  - Naming by mix reads 43.2%, 49.6%, 58.0%, 72.7%, 86.6%, 90.2% and 90.6%.
  - Alive or dead by mix reads 91.4%, 91.4%, 92.4%, 92.2%, 90.1%, 86.3% and 85.7%.
  - Naming vehicles from words is 92.8% correct at 0.5 and 83.6% at 0.75.
- Uncertainty
  - The alive-or-dead interval at a mix of 0 is 89.5% to 93.2%.
  - The alive-or-dead interval at a mix of 0.5 is 90.5% to 94.0%.
  - The two intervals overlap, so the 0.5 mix shows no loss and no proven gain.
  - The naming value at 0.5 has a 95% interval of 70.28% to 74.89% across species.
  - Intervals come from resampling species 2,000 times and taking the middle 95% of results.
- Not shown
  - The slide does not show why the alive-or-dead score holds until 0.5 and then falls.

**Speaker notes**

This is the earlier alive-or-dead curve with the naming curve drawn on the same axes. Follow them from left to right. Naming climbs at every step: 43.2, 49.6, 58.0, 72.7, 86.6, 90.2, 90.6. Alive-or-dead does not move for the first half: 91.4, 91.4, 92.4, 92.2. Then it goes to 90.1 at a mix of 0.75, 86.3 at 0.9 and 85.7 at the end. So the two changes do not happen over the same mixes. A model halfway between the two has 62% of the naming gain and no alive-or-dead loss. Vehicle naming from words is also intact at this mix, 92.8%, and falls to 83.6% at 0.75. The intervals at 0 and at 0.5 overlap (89.5 to 93.2 against 90.5 to 94.0), so the safe reading at 0.5 is that nothing has been lost yet.
