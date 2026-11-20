# Slide 36: Six measurements placed on the model, from block 1 to where photos meet names

LOOKING BACK · THE WHOLE MODEL

Top row: the image side. Bottom row: the text side. The fewer directions hold a weight change, the more ordered the change is. Telling alive animals from dead ones was tested on 1,323 photos of 115 species that the test’s classifier never saw.

**Method notes**

The slide marks six earlier measurements on a diagram of the whole model.

- What was measured
  - The slide places six earlier results where each was measured in the model.
  - The slide reports no new measurement.
- Data
  - Alive or dead was tested on 1,323 photos of 115 species the classifier never saw.
  - Species naming used five example photos of each of 223 species.
  - Vehicle naming used 1,000 CIFAR-100 photos of ten vehicle classes.
- Numbers
  - In block 1, 141 directions hold 90% of the weight change.
  - In blocks 8 to 24 about 500 directions hold 90% of the change, 481 to 515 by block.
  - A random change of the same size needs 523 directions.
  - At block 23 BioCLIP 2's summary token becomes 4.2 points worse at alive or dead.
  - The patch tokens still score 91% at block 23, 91.16% unrounded.
  - Training changed the word table by 88%, 0.877 unrounded.
  - Species naming is 45.5% in the starting model and 90.6% in BioCLIP 2.
  - Vehicle naming from words is 93.0% in the starting model and 45.8% in BioCLIP 2.
- Uncertainty
  - The 95% interval on the 4.2 point fall at block 23 is -6.38 to -2.33 points.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The diagram does not show a causal link between any weight change and any score.
- Definitions
  - The fewer directions hold a weight change, the more ordered the change is.

**Speaker notes**

This is the anatomy slide from the start, drawn as one picture, and now we can write on it. Follow a photo from the left. It is cut into 256 patches, a summary token is added, and all 257 tokens pass through 24 image blocks. Only the summary token goes on through the final rescaling and projection to become 768 numbers. A name takes the lower route through the word table and the text blocks, and the two lists meet in a cosine score. Now the six marks. In block 1 the weight change is organised: 141 directions hold 90% of it. From block 8 on it looks like a random change. At block 23 the summary token loses 4.2 points on alive or dead in one step, while the patch tokens beside it still score 91%. On the text side the word table changed by 88%. At the image output, species naming goes from 45.5% to 90.6%. And where photos meet names, vehicles named from words fall from 93.0% to 45.8%.
