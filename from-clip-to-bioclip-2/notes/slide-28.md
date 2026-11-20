# Slide 28: Block 23’s weight change needs 514 directions to hold 90% of it, close to the 523 of a random change

QUESTION 2 · WEIGHT CHANGE, ALL 24 BLOCKS

141 of 1,024

Directions (pairs of an input and an output pattern) needed to hold 90% of the change to block 1’s attention query weights. A small, targeted edit needs few. A random change of the same size needs 523.

From block 8 on the count is 481 to 515, close to a random change. Blocks 23 and 24 need 514 and 506, like every other late block.

Horizontal axis: image block, 1 to 24. Bars: directions needed for 90% of the squared change to the attention query weights, which set what each token looks for. On the text side every block needs 376 to 387 directions, against 391 or 392 for a random change.

**Method notes**

The slide counts the directions needed to hold 90% of the weight change in each block.

- What was measured
  - Each bar is the number of directions that hold 90% of a block's squared weight change.
  - The weights compared are the attention query weights of the 24 image blocks.
- Data
  - The count uses the stored weights of the two models and no photos.
  - Each query weight matrix is 1,024 by 1,024, so at most 1,024 directions exist.
- Method
  - The change is BioCLIP 2's query weights minus the starting model's.
  - The change is split into directions ranked from strongest to weakest.
  - The count is the fewest directions whose squared strengths add up to 90% of the total.
  - The comparison is a random matrix of the same shape and the same total squared size.
- Numbers
  - Block 1 needs 141 of 1,024 directions.
  - Blocks 2 to 7 need 184, 174, 312, 374, 433 and 458 directions.
  - From block 8 on the count runs from 481 to 515.
  - Blocks 23 and 24 need 514 and 506 directions.
  - A random change of the same size needs 523 directions, 522 or 523 in each block.
  - The attention key weights need 157 directions in block 1 and the value weights 189.
  - The attention output weights need 465 to 518 directions across the 24 blocks.
  - On the text side the query weights need 376 to 387 directions per block.
  - On the text side a random change of the same size needs 391 or 392 directions.
- Uncertainty
  - The counts are exact properties of the two weight files, with no sampling.
  - The random comparison uses one random matrix per block.
- Not shown
  - Nothing in the bar for block 23 marks the block where the summary token loses 4.2 points.
  - A direction count does not show what a weight change does to any test score.
- Definitions
  - A direction is a pair of an input pattern and an output pattern of a weight matrix.
  - A small, targeted edit to a weight matrix needs few directions.

**Speaker notes**

The same count for every block. Take the difference between the two models’ attention query weights and ask how many independent directions are needed to capture 90% of it. If fine-tuning were a small edit, the answer would be a handful. In the first block it is 141; by block 7 it is 458; from block 8 on it is 481 to 515 out of 1,024, against 523 for noise of the same size. The point for this question is on the right-hand side. Block 23 is where the summary token loses 4.2 points, and nothing about its bar marks it out. The attention key and value weights behave the same way.
