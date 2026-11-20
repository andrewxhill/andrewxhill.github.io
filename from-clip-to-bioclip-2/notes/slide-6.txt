# Slide 6: BioCLIP 2 names 90.6% of photos of 223 species correctly, up from the starting model’s 45.5%

WHAT TRAINING IMPROVED

+45 points

Give the model five example photos of each species, then ask it to name new photos. BioCLIP 2 gets 9 in 10 right.

Each model expects pixel values adjusted in its own way (input scaling). The 45.5% and 90.6% give each model its own. The curve uses BioCLIP 2’s for every mix, so the starting model scores 43.2% on it.

Horizontal axis: BioCLIP 2’s share of every weight, from 0, the starting model (Start), to 1, BioCLIP 2. iNaturalist photos, 223 species. Each mix names more photos correctly than the one before it.

**Method notes**

The slide shows species naming accuracy for seven mixes from the starting model to BioCLIP 2.

- What was measured
  - The slide reports the share of species photos named correctly from five example photos.
  - The curve reports the same score for seven mixes of the two models' weights.
- Data
  - The naming test uses 3,734 iNaturalist test photos of 223 species.
  - The 223 species belong to 89 families.
  - Example photos and test photos are different photos.
- Method
  - Each species is represented by the average image vector of five example photos.
  - A test photo is given the species whose average vector is closest in direction.
  - Naming accuracy is averaged over 20 random draws of the five example photos.
  - Each of the 223 species has equal weight in the naming score.
  - The naming method is known as nearest class mean.
  - The two headline figures give each model its own pixel scaling.
  - The curve gives every mix the OpenAI pixel scaling, which BioCLIP 2 expects.
- Numbers
  - The starting model names 45.5% correctly with its own pixel scaling, 45.49% unrounded.
  - BioCLIP 2 names 90.6% of photos correctly, 90.63% unrounded.
  - The gain shown as +45 points is 45.14 points unrounded.
  - On the curve the starting model scores 43.2%, 43.21% unrounded.
  - The curve reads 43.21%, 49.61%, 58.04%, 72.65%, 86.62%, 90.24% and 90.63%.
  - The seven curve points are mixes of 0, 0.1, 0.25, 0.5, 0.75, 0.9 and 1.
- Uncertainty
  - The starting model's 45.49% has a 95% interval of 42.75% to 48.11% across species.
  - BioCLIP 2's 90.63% has a 95% interval of 89.34% to 91.91% across species.
  - The 95% interval on the gain across species families is 41.9 to 48.5 points.
  - Intervals come from resampling species 2,000 times and taking the middle 95% of results.
- Not shown
  - The slide does not show naming from words, only naming from example photos.
  - The slide covers 223 species and does not show other species.
- Definitions
  - A mix of 0.5 sets every weight to the average of the two models' values.
  - Input scaling is the adjustment of pixel values that each model expects.

**Speaker notes**

Naming is nearest class mean: average the embeddings of five example photos per species, then assign each test photo to the closest average. Twenty draws of the five examples. The 95% interval on the gain across species families is 41.9 to 48.5 points.
