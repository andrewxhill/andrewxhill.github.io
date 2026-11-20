# Slide 1: From CLIP to BioCLIP 2

ONE MODEL, BEFORE AND AFTER BIOLOGY TRAINING

BioCLIP 2 began as a general image–text model and was trained further on 214 million organism photos. It now names species twice as well. Both models have the same layout of 428 million weights, so each weight in one has a partner in the other and the two can be compared directly. Three questions follow: what did BioCLIP 2 get worse at, where in the network does it get worse, and can one model keep the naming without that loss?

45.5%

Starting model: species named correctly, given five example photos of each of 223 species

90.6%

The same test after BioCLIP 2’s training

**Method notes**

The cover states the comparison and the headline naming result, 45.5% against 90.6%.

- What was measured
  - The explainer compares the starting model with BioCLIP 2, which was trained from it.
  - The headline measurement is the share of species photos named correctly.
  - Naming is tested by giving a model five example photos of each of 223 species.
- Numbers
  - The starting model names 45.5% of species photos correctly, 45.49% unrounded.
  - BioCLIP 2 names 90.6% of species photos correctly, 90.63% unrounded.
  - BioCLIP 2 was trained further on 214 million organism photos.
  - Each model has 427,616,513 weights, which the cover rounds to 428 million.
  - Training also replayed 26 million general image and text pairs.
- Definitions
  - The starting model is the LAION-2B CLIP ViT-L/14 model.
  - A weight is one learned number in a model.
  - The two models share one layout, so each weight in one has a partner in the other.

**Speaker notes**

The starting model is LAION-2B CLIP ViT-L/14. BioCLIP 2 is the same architecture after training on TreeOfLife-200M with 26 million general image–text pairs replayed. Naming here is nearest class mean from five example photos per species, scored on 223 species of iNaturalist photos. The rest of the talk is three questions, each with a guess first and then the measurements.
