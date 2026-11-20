# Slide 31: The starting model with BioCLIP 2’s last 12 blocks copied in names 76.6% of species photos, up from 43%

QUESTION 3 · SWAPPING BLOCKS

43% → 77%

Species naming when the starting model keeps its first 12 image blocks and takes BioCLIP 2’s last 12. No one trained this combination. That is 33 of the 47 points between the two models.

Accuracy at telling alive from dead falls as naming rises. With BioCLIP 2’s last 6 blocks the starting model loses 1.8 points. With the last 18 it scores 84.2%, below BioCLIP 2’s 85.7%.

Horizontal axis: image blocks taken from BioCLIP 2, counted from the output end. 223 species; 1,323 photos of 115 species.

**Method notes**

The slide shows both scores as more of BioCLIP 2's last blocks go into the starting model.

- What was measured
  - The slide reports naming and alive-or-dead accuracy for the starting model with swaps.
  - Each swap replaces the starting model's last 6, 12, 18 or all 24 image blocks.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - Image-model weights are held fixed during scoring.
  - The alive-or-dead classifier is refitted to each hybrid model's output.
  - The five-photo naming references are rebuilt for each hybrid model.
  - Every model in the comparison is given the OpenAI pixel scaling.
  - Blocks are counted from the output end of the image side.
  - The swaps of 6, 12 and 18 blocks keep the starting model's filters and final steps.
  - The last point swaps the whole image side, including patch filters and final projection.
- Numbers
  - Naming reads 43.2%, 53.6%, 76.6%, 86.1% and 90.6% for 0, 6, 12, 18 and 24 blocks.
  - The unrounded naming values are 43.21%, 53.57%, 76.63%, 86.14% and 90.63%.
  - Alive or dead reads 91.4%, 89.6%, 87.7%, 84.2% and 85.7% for the same swaps.
  - The unrounded alive-or-dead values are 91.41%, 89.63%, 87.69%, 84.15% and 85.68%.
  - With BioCLIP 2's last 12 blocks naming rises 33 of the 47 points between the models.
  - With BioCLIP 2's last 6 blocks the starting model loses 1.8 points at alive or dead.
  - With BioCLIP 2's last 18 blocks the score of 84.2% is below BioCLIP 2's 85.7%.
- Uncertainty
  - Naming with the last 12 blocks has a 95% interval of 74.81% to 78.42% across species.
  - With C fixed at 1 alive or dead reads 88.06%, 87.15%, 84.60%, 81.39% and 83.89%.
  - No interval is reported for the alive-or-dead differences between swaps.
- Not shown
  - None of the hybrid models was trained as a whole.
  - The slide does not show which individual blocks carry the change.
- Definitions
  - A hybrid is a model built by copying some blocks from one model into the other.

**Speaker notes**

Start with the plain version of the swap. Take the starting model and replace its last 6, 12 or 18 image blocks with BioCLIP 2’s. You might expect a model stitched together like that to produce nonsense. It does not. Naming goes 43.2, 53.6, 76.6, 86.1, 90.6 as more of BioCLIP 2’s blocks go in. Alive or dead goes 91.4, 89.6, 87.7, 84.2, 85.7. The last point swaps the whole image side including patch filters and final projection. None of these hybrids was trained as a whole, and each one works. With the last 18 blocks swapped, alive-or-dead is 84.2%, lower than BioCLIP 2 itself.
