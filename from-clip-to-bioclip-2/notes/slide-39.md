# Slide 39: Could several specialist models share the same first 12 blocks?

LOOKING AHEAD

What the measurements showed

A hybrid’s two scores follow the model that supplies image blocks 13 to 24. With the starting model’s last 12 blocks, BioCLIP 2 scores 92.9% on telling alive animals from dead ones and names 52.3% of species photos. With BioCLIP 2’s last 12, the starting model scores 87.7% and names 76.6%. Neither combination was trained.

The summary token can name species only in the late blocks. Neither model names 1 photo in 10 from any block up to block 16.

BioCLIP 2’s patch tokens can still tell alive animals from dead ones. They score 91.0% at block 24.

Open questions, not yet measured

1. Could one shared lower half carry several specialist upper halves, for birds, plants or satellite images, with one chosen for each photo?

2. Could training be changed so the summary token keeps the information the patch tokens still carry?

3. Does the summary token’s score also fall at one block in other models trained from CLIP?

4. How specialised can the trained model be before averaging the weights stops giving both skills?

**Method notes**

The slide lists four open questions, none of which has been measured.

- What was measured
  - The slide restates three measured results and poses four questions that are untested.
- Numbers
  - BioCLIP 2 with the starting model's last 12 blocks scores 92.9% at alive or dead.
  - BioCLIP 2 with the starting model's last 12 blocks names 52.3% of species photos.
  - The starting model with BioCLIP 2's last 12 blocks scores 87.7% and names 76.6%.
  - Neither model names 1 photo in 10 from any block up to block 16.
  - BioCLIP 2's patch tokens score 91.0% at alive or dead at block 24.
- Not shown
  - No test was run of several expert upper halves sharing one lower half.
  - No test was run of training that makes the summary token keep the patch information.
  - No other model trained from CLIP was read block by block.
  - No test was run of how specialised a model can be before weight averaging stops working.
  - The birds, plants and satellite images in the diagram are illustrations only.

**Speaker notes**

This is the part I find most exciting, and none of it has been measured. Start from what we did see. When we exchanged the last 12 image blocks between the two models, both scores followed those blocks: BioCLIP 2 with the starting model’s last 12 scored 92.9% on alive or dead and named 52.3% of species, and the starting model with BioCLIP 2’s last 12 named 76.6%. So both hybrids run, the species skill is built late, and BioCLIP 2’s patch tokens still hold alive or dead. Could one lower half serve several upper halves, one for birds, one for plants, one for satellite images, with the right one chosen per photo? Could training tell the summary token to keep what the patch tokens hold? Does the block-23 step appear in other models trained from CLIP? How specialised can the specialist get before averaging stops working? Each is a test someone could run.
