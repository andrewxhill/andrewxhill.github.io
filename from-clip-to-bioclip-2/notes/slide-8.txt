# Slide 8: BioCLIP 2 scores 85.7% at telling alive animals from dead ones; the starting model scores 92.1%

QUESTION 1 · ALIVE OR DEAD

92.1% → 85.7%

Balanced accuracy (the average of accuracy on alive photos and on dead ones), worked out for each of 115 held-out species and then averaged: starting model, then BioCLIP 2.

A simple classifier reads “alive” or “dead” from the model’s 768 numbers. For species it was trained on, the score stays near 91%. The score falls only for species it was not trained on.

Horizontal axis: BioCLIP 2’s share of every weight, from 0, the starting model, to 1, BioCLIP 2. 95% interval on the change: −9.5 to −3.4 points. Every mix is given BioCLIP 2’s adjustment of pixel values, so the starting model scores 91.4% here.

**Method notes**

The slide shows alive-or-dead accuracy for seven mixes, for seen and held-out species.

- What was measured
  - The slide reports how well a classifier reads alive or dead from a model's 768 numbers.
  - One line covers species the classifier was trained on.
  - The other line covers species held out from the classifier.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
  - The 115 species belong to 60 families.
- Method
  - The classifier is logistic regression fitted to a frozen model's image vector.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Accuracy on alive photos and accuracy on dead photos are averaged within each species.
  - The reported score is the mean of the 115 species scores, with each species weighted equally.
  - The two headline figures give each model its own pixel scaling.
  - The curve gives every mix the OpenAI pixel scaling, which BioCLIP 2 expects.
- Numbers
  - On held-out species the starting model scores 92.1%, 92.14% unrounded.
  - On held-out species BioCLIP 2 scores 85.7%, 85.68% unrounded.
  - On the curve the starting model scores 91.4% on held-out species, 91.41% unrounded.
  - The held-out curve reads 91.41%, 91.43%, 92.39%, 92.23%, 90.10%, 86.25% and 85.68%.
  - The seen-species curve reads 91.99%, 92.27%, 92.97%, 93.91%, 92.53%, 91.37% and 91.16%.
  - The seven curve points are mixes of 0, 0.1, 0.25, 0.5, 0.75, 0.9 and 1.
- Uncertainty
  - The 95% interval on the change from 92.1% to 85.7% is -9.5 to -3.4 points.
  - The starting model's 92.14% has a 95% interval of 90.06% to 93.95% across species.
  - BioCLIP 2's 85.68% has a 95% interval of 83.28% to 87.87% across species.
  - Intervals come from resampling species 2,000 times and taking the middle 95% of results.
  - With C fixed at 1 the two models score 88.97% and 83.89% on held-out species.
- Not shown
  - The slide does not show why the score falls for held-out species.
  - Adult-or-juvenile and female-or-male tests showed a similar widening gap of about 5 points.
  - The adult-or-juvenile decline did not repeat on 100 confirmation species.
- Definitions
  - Balanced accuracy is the average of accuracy on alive photos and on dead photos.
  - A held-out species is one whose photos were never used to fit the classifier tested on it.

**Speaker notes**

The classifier is logistic regression on frozen embeddings. Unseen species means the species and its photographers were held out of classifier training.
