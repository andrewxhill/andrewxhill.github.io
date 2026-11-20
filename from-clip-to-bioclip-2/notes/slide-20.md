# Slide 20: Where in the network does BioCLIP 2 get worse at telling alive from dead?

QUESTION 2

A natural guess: a little in every block. Training changed the weights of all 24 image blocks, so BioCLIP 2 should fall a little further behind the starting model at each block, from the first to the last.

Read each block

Stop the model after a block, take the tokens it holds there, and test them the same way as the final output.

Watch the attention

See which patches of the photo the summary token, the one token that becomes the output, draws on in the last blocks.

Look at the weights

Subtract the starting model’s weights from BioCLIP 2’s, block by block, and see whether any block’s change stands out.

**Method notes**

The slide poses the second question and names three ways of looking inside the network.

- What was measured
  - The second question is where in the network BioCLIP 2 gets worse at alive or dead.
  - The slide states a guess and reports no result.
  - The guess is a small loss at every one of the 24 image blocks.
- Method
  - The first method stops the model after a block and tests the tokens held there.
  - The second method records which patches the summary token draws on in the last blocks.
  - The third method subtracts the starting model's weights from BioCLIP 2's, block by block.
- Numbers
  - The image side changed by about a fifth of its size overall, 0.22 as a relative change.

**Speaker notes**

Training changed every block, so a gradual loss is the reasonable expectation. There are three ways to look inside. The first is the most direct: treat the output of every block as if it were the final answer and run the same tests on it.
