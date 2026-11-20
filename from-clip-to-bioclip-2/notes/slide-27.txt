# Slide 27: 57.7% of block 1’s weight change falls where the starting model’s strongest patterns meet; in block 24, 9.04%

QUESTION 2 · THE WEIGHT CHANGE AS A PICTURE

Each picture is one block’s attention query weights in BioCLIP 2 minus the same weights in the starting model. These weights set what each token looks for. White is no change.

Any table of weights can be split into ranked pairs of an input pattern and an output pattern, called directions. Columns are the starting model’s input patterns, rows its output patterns, strongest first.

The outlined corner, where the strongest patterns meet, is a sixteenth of the picture, so a change spread evenly would put 6.25% there. Block 1’s change puts 57.7% there. Block 24’s puts 9.04% there and shows a faint diagonal: a slightly larger change where an input pattern meets its own output pattern.

Each picture is 256 × 256 cells; a cell averages the size of the change over 4 × 4 of the starting model’s directions. Both pictures share one colour scale. Percentages are shares of the squared change.

**Method notes**

The slide draws the change in attention query weights for block 1 and block 24.

- What was measured
  - Each picture is one block's query weights in BioCLIP 2 minus the starting model's.
  - The percentage is the share of squared change inside the outlined corner.
- Data
  - The pictures use the stored weights of the two models and no photos.
  - Each query weight matrix is 1,024 by 1,024.
- Method
  - The starting model's query matrix is split into ranked input and output patterns.
  - Columns are the starting model's input patterns and rows its output patterns.
  - Patterns are ordered strongest first on both axes.
  - Each picture has 256 by 256 cells.
  - Each cell averages the size of the change over 4 by 4 of the starting model's directions.
  - Both pictures share one colour scale, with white for no change.
  - The outlined corner covers the first 256 directions on each axis.
- Numbers
  - Block 1 puts 57.7% of its squared change in the outlined corner, 57.67% unrounded.
  - Block 24 puts 9.04% of its squared change in the same corner.
  - The corner is a sixteenth of the picture, so an even spread would put 6.25% there.
  - The first 64 directions per axis hold 12.8% of block 1's change and 1.10% of block 24's.
  - For block 1, 141 directions hold 90% of the squared change.
  - For block 24, 506 directions hold 90% of the squared change.
  - A random matrix of the same size and total squared change needs 523 directions.
- Uncertainty
  - The figures are exact properties of the two weight files, with no sampling.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The pictures do not show what effect the weight change has on any test score.
  - The pictures cover the query weights of two of the 24 blocks.
- Definitions
  - Query weights turn a token into the vector used to score attention.
  - A direction is a pair of an input pattern and an output pattern of a weight matrix.
  - Directions are ranked by how strongly the matrix acts along them.

**Speaker notes**

The third way to look is at the weights themselves. Earlier we drew the first-layer filters as pictures. This is the same idea for one matrix inside a block: take BioCLIP 2’s weights, subtract the starting model’s, and draw what is left. The axes are chosen so that structure would be visible. Any weight matrix can be broken into directions, pairs of an input pattern and an output pattern, ranked by how strongly the matrix acts along them. The picture is laid out in the starting model’s own directions, strongest first. In block 1 the change is organised: a dark band over the starting model’s strongest input patterns, darkest at the top left. In block 24 the change is an even wash with a faint diagonal, where each input pattern meets its own output pattern. Counted another way, 141 directions hold 90% of block 1’s change; block 24 needs 506, and a random matrix of the same size needs 523.
