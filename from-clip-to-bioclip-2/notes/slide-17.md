# Slide 17: In BioCLIP 2, 59% of a photo’s most similar photos share its alive-or-dead label, down from 81%

QUESTION 1 · EACH PHOTO’S MOST SIMILAR PHOTOS

81% → 59%

For each photo, take the eight photos a model rates most similar. In the starting model, 81% share its alive-or-dead label. In BioCLIP 2, 59% do, nine points above chance.

The share of the same species rises from 24% to 79%. A classifier still tells alive from dead from BioCLIP 2’s 768 numbers (85.7%), but photos with the same label are now only slightly more likely to be rated similar.

Horizontal axis: BioCLIP 2’s share of every weight (0 is the starting model). All 1,323 alive-or-dead test photos, similar photos by other photographers only.

**Method notes**

The slide counts how often a photo's eight most similar photos share its label or species.

- What was measured
  - The slide reports the share of a photo's eight most similar photos with the same label.
  - The slide also reports the share of the eight that are the same species.
- Data
  - The count covers all 1,323 alive-or-dead test photos.
  - Each photo has eight most similar photos, giving 10,584 comparisons per model.
- Method
  - Each model ranks photos by similarity of image vectors, with no classifier involved.
  - Similar photos by the same photographer as the chosen photo are excluded.
  - The figures on the slide give every mix the OpenAI pixel scaling.
- Numbers
  - In the starting model 81% of similar photos share the label, 81.39% unrounded.
  - In BioCLIP 2 59% of similar photos share the label, 59.10% unrounded.
  - The same-species share rises from 24% to 79%, 24.38% and 79.00% unrounded.
  - Chance for sharing the alive-or-dead label is 50%, 49.95% unrounded.
  - Chance for sharing the species is 0.86%.
  - At a mix of 0.5 the label share is 73.35% and the same-species share is 53.00%.
  - At a mix of 0.75 the label share is 65.16% and the same-species share is 71.46%.
  - With its own pixel scaling the starting model's two shares are 82.24% and 25.51%.
  - A classifier still reads alive or dead from BioCLIP 2's 768 numbers at 85.7%.
- Uncertainty
  - No interval is reported for the neighbour shares.
- Not shown
  - The neighbour shares do not show why BioCLIP 2 groups photos by species.
- Definitions
  - A photo's most similar photos are those whose image vectors are closest to its own.

**Speaker notes**

This needs no classifier at all, only distances between embeddings, and it agrees with the classifier result. The starting model rates dead animals of different species as similar to each other. BioCLIP 2 rates photos of the same species as most similar, and what is left of the alive-or-dead signal is weaker across species.
