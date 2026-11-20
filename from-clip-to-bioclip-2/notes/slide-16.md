# Slide 16: The 8 photos the starting model rates most like a dead moose are all dead animals; BioCLIP 2’s are mostly kangaroos

QUESTION 1 · WHAT EACH MODEL TREATS AS ALIKE

The photo we ask about: a Moose, dead.

Starting model · 8 of 8 are dead animals, none is a moose

Weights mixed, 0.75 BioCLIP 2 · 4 of 8 are dead, 1 is a moose

BioCLIP 2 · 5 kangaroos, 2 moose and a wombat; 3 of the 8 are dead

Most similar first, from other photographers only. iNaturalist photos, CC BY and CC BY-NC, cropped; credits on the last slide.

**Method notes**

The slide shows the eight photos each of three models rates most like a dead moose photo.

- What was measured
  - The slide shows which photos each model rates as most similar to one chosen photo.
  - The counts are how many of the eight are dead animals and how many are moose.
- Data
  - The chosen photo is an iNaturalist photo of a Moose recorded as dead.
  - The photos are licensed CC BY or CC BY-NC and are cropped.
- Method
  - Each model ranks the other photos by similarity of image vectors to the chosen photo.
  - Photos by the same photographer as the chosen photo are excluded.
  - The eight shown are the nearest eight with a display licence that passed visual review.
  - The starting model row uses the starting model's own pixel scaling.
  - The 0.75 mix and BioCLIP 2 rows use the OpenAI pixel scaling.
- Numbers
  - In the starting model 8 of the 8 most similar photos are dead animals and none is a moose.
  - In the 0.75 mix 4 of the 8 most similar photos are dead and 1 is a moose.
  - In BioCLIP 2 the 8 most similar photos are 5 kangaroos, 2 moose and a wombat.
  - In BioCLIP 2 3 of the 8 most similar photos are dead and 5 are alive.
- Uncertainty
  - The slide shows one chosen photo and carries no interval.
- Not shown
  - One photo does not establish the pattern, which the next slide counts over 1,323 photos.

**Speaker notes**

For the starting model, "a dead animal on the ground" is the strongest thing about this photo, whatever the species. BioCLIP 2’s eight are five kangaroos, two moose and a wombat, and five of the eight are alive. This is one example of what the next slide counts across all 1,323 photos.
