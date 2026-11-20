# Slide 2: The two models are two files of 427,616,513 numbers, laid out the same way

THE TWO MODELS

BioCLIP 2’s authors did not start from random weights. They loaded the LAION-2B CLIP ViT-L/14 weights and kept training them on organism photos. Nothing was added or removed, so each number in one file has a partner in the other.

Starting model

LAION-2B CLIP ViT-L/14

Trained on about 2.3 billion image–caption pairs from the web.

BioCLIP 2

The same network, trained further

214 million organism images with their taxonomic names, plus 26 million general web photos and captions mixed back in, so it would not forget everything else.

A mix

Any mix of the two

For every number, mix the two values: α parts BioCLIP 2 and 1 − α parts the starting model. α = 0 is the starting model and α = 1 is BioCLIP 2. Each mix is a working model.

Sources: LAION-2B CLIP model card; Gu et al. 2025, BioCLIP 2.

**Method notes**

The slide introduces the two models and the idea of mixing their weights.

- What was measured
  - The slide describes the two models and reports no test result.
  - BioCLIP 2 was trained starting from the starting model's weights, not from random weights.
  - No weights were added or removed, so the two files of weights line up one to one.
- Numbers
  - Each model is a file of 427,616,513 numbers.
  - The starting model was trained on about 2.3 billion image and caption pairs from the web.
  - BioCLIP 2 was trained further on 214 million organism images with taxonomic names.
  - BioCLIP 2's training mixed in 26 million general web photos and captions.
- Not shown
  - The slide does not show that every mix works well, only that every mix can be run.
  - The share alpha is a share of weights and is not an amount of training.
- Definitions
  - A mix sets every weight to alpha parts BioCLIP 2 and 1 minus alpha parts starting model.
  - A mix of alpha 0 is the starting model and a mix of alpha 1 is BioCLIP 2.
  - Mixing two models' weights by a share alpha is weight interpolation (Wortsman et al., 2022).
  - Weight interpolation is possible because one model was trained from the other.

**Speaker notes**

The mixing trick is weight interpolation, as in WiSE-FT (Wortsman et al. 2022). It works here because the two models share an architecture and one was trained from the other. Alpha is a share of weights.
