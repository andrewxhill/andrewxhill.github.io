# Slide 4: Training on organism photos changed the first-layer filters by 20% and the text side’s word table by 88%

THE FIRST-LAYER FILTERS, DRAWN AS PICTURES

Starting model

BioCLIP 2

Difference, shown 4× brighter

Each tile is one 14 × 14 pixel filter that reads a patch of the photo. Tiles are ordered by how much they changed. Training changed these filters by 20% of their original size.

**Method notes**

The slide draws the first-layer filters of both models and the difference between them.

- What was measured
  - The slide compares the first-layer patch filters of the two models as pictures.
  - A change's size is the norm of the weight difference over the norm of the starting weights.
- Data
  - The pictures use the stored weights of the two models and no photos.
  - The first layer has 1,024 filters, each covering a 14 by 14 pixel patch in colour.
- Method
  - Each tile colours the weights of one filter.
  - Tiles are ordered by how much each filter changed, largest squared change first.
  - The two model grids share one colour scale and the difference grid has a second scale.
  - The difference grid is shown four times brighter.
- Numbers
  - The first-layer filters changed by 20% of their original size, 0.201 unrounded.
  - The text side's word table changed by 88% of its original size, 0.877 unrounded.
  - Across all image-side weights the relative change is 0.22.
  - Across all text-side weights the relative change is 0.28.
- Uncertainty
  - The change figures are exact properties of the two weight files, with no sampling.
- Not shown
  - The slide does not show what effect the filter change has on any test score.
  - The word table is described by one number and is not drawn.
  - The slide does not show that the word-table change causes any later result.
- Definitions
  - A first-layer filter is the set of weights that reads one patch of pixels.
  - The word table is the text side's list of one vector per token.

**Speaker notes**

This is the patch-embedding layer, the only weights in a vision transformer that can be drawn directly as small images. The stripes and blobs are edge and colour detectors. They still look alike by eye; the change is 20% by size. The change is relative L2 norm of the difference over the norm of the start: 0.20 for these filters, 0.88 for the text side’s word table.
