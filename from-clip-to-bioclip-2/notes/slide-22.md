# Slide 22: Up to block 16, neither model can name 1 species photo in 10 from its summary token

QUESTION 2 · SPECIES NAMING, BLOCK BY BLOCK

14% → 91%

BioCLIP 2’s species naming read from its summary token at block 18 and at block 24. The starting model goes from 5% to 43% over the same blocks.

Up to block 16 neither model names 1 photo in 10 from its summary token.

Horizontal axis: image block, 2 to 24. Each point is read afresh from that block’s summary token, the token that becomes the output. Start is the starting model. These scores come from a separate run of the naming test, so the block-24 values differ from other slides by under a point.

**Method notes**

The slide shows species naming read from each block's summary token in both models.

- What was measured
  - The slide reports species naming accuracy read from the summary token at each block.
  - Each point is read afresh from the summary token at one block.
- Data
  - The naming test uses 3,734 iNaturalist test photos of 223 species.
  - Readings are taken at the even-numbered image blocks from 2 to 24.
- Method
  - Each species is represented by the average vector of five example photos.
  - A test photo is given the species whose average vector is closest in direction.
  - Naming accuracy is averaged over 20 draws, with each species weighted equally.
  - The block-by-block scorer first centres and rescales vectors using example photos only.
  - The second scorer makes the endpoints differ from other slides by under a point.
  - Both models are given the OpenAI pixel scaling.
- Numbers
  - BioCLIP 2's naming from the summary token is 14% at block 18, 14.30% unrounded.
  - BioCLIP 2's naming from the summary token is 91% at block 24, 90.59% unrounded.
  - The starting model's naming is 5% at block 18 and 43% at block 24.
  - The starting model's unrounded figures are 4.99% at block 18 and 43.03% at block 24.
  - At block 22 BioCLIP 2 reads 72% and the starting model 21%, 71.91% and 20.70% unrounded.
  - At block 16 BioCLIP 2 reads 6.20% and the starting model 2.57%.
  - At block 20 BioCLIP 2 reads 30.28% and the starting model 9.42%.
  - Up to block 16 neither model's summary token names 1 photo in 10.
  - The block-by-block scorer gives BioCLIP 2 90.76% and the starting model 44.06% at the output.
- Uncertainty
  - No interval is reported for the block-by-block naming readings.
- Not shown
  - A reading shows what can be recovered at a block, not how the model uses the block.
  - The chart does not show alive-or-dead accuracy, which the next slides cover.
- Definitions
  - Reading a block means taking the tokens held after that block and testing them directly.

**Speaker notes**

Start with naming, because it shows how the method works. Read each block’s summary token and ask how well species can be named from it. Both models sit under 10% until block 16. At block 18 BioCLIP 2 is at 14% and the starting model at 5%; at 22 it is 72% against 21%; at 24, 91% against 43%. So the species skill is built in the last third of the network in both models, and training made the same late blocks do far more of it. If a cost of that training shows up late too, that would fit. The next slide runs the same reading for alive or dead.
