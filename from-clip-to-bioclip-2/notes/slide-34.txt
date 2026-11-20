# Slide 34: Read from its patch tokens, an unchanged BioCLIP 2 tells alive from dead with 89.6% accuracy, up from 85.7%

QUESTION 3 · READING THE PATCH TOKENS

89.6%

Accuracy at telling alive from dead when a classifier reads the average of BioCLIP 2’s block-24 patch tokens, passed through BioCLIP 2’s own final steps. That is 3.9 points above the summary token (95% interval 1.6 to 6.2).

The summary token still names 90.6% of species photos. One run of an unchanged BioCLIP 2 produces both results.

Final steps: rescaling and projection. Read straight after block 24, before the final steps, the same patch tokens score 91.0%.

**Method notes**

The slide reads alive or dead from BioCLIP 2's patch tokens passed through its final steps.

- What was measured
  - The slide compares two readings of one unchanged BioCLIP 2 at alive or dead.
  - One reading uses the summary token and the other the average of the 256 patch tokens.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
- Method
  - The block-24 patch tokens are averaged, then rescaled, then projected to 768 numbers.
  - Both routes use the same photos, the same weights and BioCLIP 2's own final steps.
  - The same kind of logistic regression classifier is fitted to each route's 768 numbers.
  - Each classifier is tested on species and photographers held out from its fitting.
  - The classifier's penalty setting, C, is tuned on selection photos.
- Numbers
  - The patch route scores 89.6%, 89.59% unrounded.
  - The summary token scores 85.7%, 85.68% unrounded.
  - The patch route is 3.9 points above the summary token, 3.91 unrounded.
  - Rescaling each patch token before averaging gives 89.8%, 89.83% unrounded.
  - The patch tokens score 91.0% when read straight after block 24, before the final steps.
  - The summary token still names 90.6% of species photos.
  - The starting model's summary token scores 91.4% on the same alive-or-dead test.
- Uncertainty
  - The 3.9 point gain has a 95% interval of 1.6 to 6.2 points, 1.57 to 6.23 unrounded.
  - The patch route's 89.59% has a 95% interval of 87.32% to 91.70% across species.
  - With C fixed at 1 the patch route scores 87.60% and the summary token 83.89%.
  - The two orders of rescaling and averaging differ by -0.23 points, interval -0.86 to +0.41.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show that patch tokens help with properties other than alive or dead.
  - The patch route needs the patch tokens to be kept when the model is run.

**Speaker notes**

The last option changes nothing in the model at all. Question 2 found that the patch tokens still hold alive-or-dead after block 23. Normally they are thrown away. Instead, average them, and send that average through the same final steps the summary token goes through. A classifier on that vector scores 89.6%, against 85.7% from the usual output. The gain is 3.9 points with an interval of 1.6 to 6.2. Doing the rescaling before the averaging gives 89.8%, so the order barely matters. Read directly at block 24, before the final steps, the patch tokens score 91.0%. And since nothing was modified, the summary token is still there for naming at the full 90.6%. For anyone who already runs BioCLIP 2 and cares about a property like alive or dead, this is the cheapest thing on the table: keep the patch tokens and read them.
