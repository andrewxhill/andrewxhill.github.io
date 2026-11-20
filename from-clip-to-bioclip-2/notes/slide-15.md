# Slide 15: Of the 8 photos each model rates most like a robin photo, BioCLIP 2 picks 7 robins and the starting model 1

QUESTION 1 · WHAT EACH MODEL TREATS AS ALIKE

The photo we ask about: a European Robin, small and far away, which the starting model usually misnames.

Starting model · 1 of 8 is a robin

Weights mixed, 0.75 BioCLIP 2 · 6 of 8 are robins

BioCLIP 2 · 7 of 8 are robins

Most similar first, from other photographers only. iNaturalist photos, CC BY and CC BY-NC, cropped; credits on the last slide.

**Method notes**

The slide shows the eight photos each of three models rates most like one robin photo.

- What was measured
  - The slide shows which photos each model rates as most similar to one chosen photo.
  - The count under each row is how many of the eight photos are European Robins.
- Data
  - The chosen photo is an iNaturalist photo of a European Robin, small in the frame.
  - The photos are licensed CC BY or CC BY-NC and are cropped.
- Method
  - Each model ranks the other photos by similarity of image vectors to the chosen photo.
  - Photos by the same photographer as the chosen photo are excluded.
  - The eight shown are the nearest eight with a display licence that passed visual review.
  - The starting model row uses the starting model's own pixel scaling.
  - The 0.75 mix and BioCLIP 2 rows use the OpenAI pixel scaling.
- Numbers
  - In the starting model 1 of the 8 most similar photos is a robin.
  - In the 0.75 mix 6 of the 8 most similar photos are robins.
  - In BioCLIP 2 7 of the 8 most similar photos are robins.
  - From five examples the starting model names the chosen photo correctly in 1 of 20 draws.
  - From five examples BioCLIP 2 names the chosen photo correctly in 20 of 20 draws.
- Uncertainty
  - The slide shows one chosen photo and carries no interval.
- Not shown
  - One photo does not establish how often the pattern holds across photos.
  - The rows after review can differ from the nearest eight in the full set of photos.

**Speaker notes**

The starting model groups this photo with other small birds in green foliage: similar scenes. BioCLIP 2 groups it with robins in quite different scenes: the same species. With five examples per species, the starting model names this photo correctly in 1 of 20 draws; BioCLIP 2 in 20 of 20.
