# Slide 32: BioCLIP 2 with the starting model’s last 12 blocks copied in scores 92.9% at telling alive from dead

QUESTION 3 · BIOCLIP 2 WITH STARTING-MODEL BLOCKS

The hybrid, which no one trained: BioCLIP 2’s image blocks 1 to 12 in teal, then the starting model’s blocks 13 to 24 in violet.

It scores 92.9% at telling alive from dead, where the starting model (Start) scores 91.4% and BioCLIP 2 85.7%.

It names 52.3% of species, against the starting model’s 43.2% and BioCLIP 2’s 90.6%. Both scores are closer to those of the model that supplies blocks 13 to 24.

The hybrid keeps BioCLIP 2’s patch filters, text side and the steps after block 24. 223 species; 1,323 photos of 115 species.

**Method notes**

The slide shows BioCLIP 2 with the starting model's last 12 image blocks copied in.

- What was measured
  - The slide reports naming and alive-or-dead accuracy for one hybrid model.
  - The hybrid has BioCLIP 2's image blocks 1 to 12 and the starting model's blocks 13 to 24.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - Image-model weights are held fixed during scoring.
  - The alive-or-dead classifier is refitted to each hybrid model's output.
  - The five-photo naming references are rebuilt for each hybrid model.
  - Every model in the comparison is given the OpenAI pixel scaling.
  - The hybrid keeps BioCLIP 2's patch filters, text side and the steps after block 24.
- Numbers
  - The hybrid scores 92.9% at alive or dead, 92.90% unrounded.
  - The starting model scores 91.4% and BioCLIP 2 85.7%, 91.41% and 85.68% unrounded.
  - The hybrid names 52.3% of species photos, 52.34% unrounded.
  - The starting model names 43.2% and BioCLIP 2 90.6%, 43.21% and 90.63% unrounded.
  - The opposite hybrid, on the previous slide, names 76.6% and scores 87.7%.
  - The hybrid names 88.90% of vehicle photos from example photos.
- Uncertainty
  - The hybrid's naming has a 95% interval of 49.69% to 54.86% across species.
  - With C fixed at 1 the hybrid scores 91.47% at alive or dead.
  - No interval was computed for the gap between the hybrid and the starting model.
  - The hybrid's 92.9% is therefore read as at least as good as 91.4%, not as better.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The hybrid model was not trained as a whole.
  - One pair of hybrids does not show which of blocks 13 to 24 matter most.

**Speaker notes**

Now swap the other way. Keep BioCLIP 2’s first 12 blocks and finish with the starting model’s last 12. Nobody trained this model either. On alive or dead it scores 92.9%, where the starting model scores 91.4% and BioCLIP 2 85.7%. The intervals have not been compared here, so read 92.9% against 91.4% as at least as good. Naming is back down at 52.3%. Put this next to the previous slide: the starting model with BioCLIP 2’s last 12 blocks named 76.6% and scored 87.7% on alive-or-dead. In both hybrids the scores follow whichever model supplies blocks 13 to 24.
