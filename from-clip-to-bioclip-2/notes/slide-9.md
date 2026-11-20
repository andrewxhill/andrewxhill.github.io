# Slide 9: 159 photos are labelled alive or dead correctly by the starting model alone, and 59 by BioCLIP 2 alone

QUESTION 1 · PHOTO BY PHOTO

All 1,323 test photos, by which model’s classifier labels them correctly

656 photos recorded as alive

667 photos recorded as dead

The 159 photos only the starting model gets right split evenly: 78 alive animals and 81 dead ones. Of the 59 only BioCLIP 2 gets right, 39 are dead animals and 20 alive. Counting every photo equally, the starting model is right on 92.4% and BioCLIP 2 on 84.8%; counting each of the 115 species equally gives 92.1% and 85.7%.

Right means the classifier agrees with the alive-or-dead label recorded by the iNaturalist contributor. 115 species, each tested by a classifier trained without that species.

**Method notes**

The slide counts the 1,323 test photos by which model's classifier labels them correctly.

- What was measured
  - The slide counts photos on which each model's alive-or-dead classifier is right.
  - A classifier is right when it agrees with the label recorded by the contributor.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
- Method
  - Each species is tested by a classifier fitted without that species.
  - The classifiers are those of the first study, each with its own model's pixel scaling.
  - Pixel scaling and model weights therefore both differ between the two classifiers.
  - A classifier predicts dead when its score for a photo is above zero.
- Numbers
  - Both classifiers are right on 1,063 photos and both are wrong on 42.
  - Only the starting model's classifier is right on 159 photos.
  - Only BioCLIP 2's classifier is right on 59 photos.
  - Of 656 alive photos, both classifiers are right on 539 and both are wrong on 19.
  - Of 656 alive photos, only the starting model is right on 78 and only BioCLIP 2 on 20.
  - Of 667 dead photos, both classifiers are right on 524 and both are wrong on 23.
  - Of 667 dead photos, only the starting model is right on 81 and only BioCLIP 2 on 39.
  - Counting photos equally, the starting model is right on 92.4% and BioCLIP 2 on 84.8%.
  - Counting the 115 species equally gives 92.1% and 85.7%.
  - The Common Hedgehog has the most disagreements, 7 of its 12 photos.
  - Of the 7 hedgehog disagreements, 4 favour the starting model and 3 favour BioCLIP 2.
- Uncertainty
  - The counts are exact for the 1,323 test photos and carry no interval.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The counts do not show why a classifier misses a given photo.
  - The counts do not separate the effect of pixel scaling from the effect of the weights.

**Speaker notes**

A percentage hides what is happening to individual photos, so here is the same result as a count. Both classifiers agree with the label on 1,063 photos and both miss 42. The two middle slices are where the models differ: 159 photos that only the starting model gets right and 59 that only BioCLIP 2 gets right. The starting model’s extra wins are not concentrated in one label; they are half alive and half dead. The species with the most photos on which the two classifiers disagree is the common hedgehog, 7 of its 12 photos. The next two slides show what these photos look like.
