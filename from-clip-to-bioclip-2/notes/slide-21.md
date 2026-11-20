# Slide 21: Every block holds 257 tokens: 256 patch tokens and 1 summary token

QUESTION 2 · WHAT A BLOCK HOLDS

A token is a list of 1,024 numbers. Each patch token describes one 14 × 14 pixel patch of the photo. The summary token describes no patch of its own. In every block it reads from the patch tokens through attention.

After block 24 only the summary token goes on, through two final steps: a rescaling step and a final projection. They turn it into the model’s 768 output numbers.

So any block can be read two ways: from its summary token, or from the average of its 256 patch tokens.

The image side cuts a 224 × 224 pixel photo into a 16 by 16 grid of patches, 256 in all. The summary token is often called the class token.

**Method notes**

The slide explains the 257 tokens a block holds and the two ways a block can be read.

- What was measured
  - The slide describes the model's structure and reports no test result.
- Numbers
  - Every block holds 257 tokens, 256 patch tokens and 1 summary token.
  - Each token is a list of 1,024 numbers.
  - The image side cuts a 224 by 224 pixel photo into a 16 by 16 grid of patches.
  - Each patch is 14 by 14 pixels.
  - Two final steps turn the summary token into the model's 768 output numbers.
- Definitions
  - A patch token describes one 14 by 14 pixel patch of the photo.
  - The summary token describes no patch and reads from the patch tokens through attention.
  - The summary token is often called the class token.
  - Only the summary token is passed on after block 24.
  - The two final steps are a rescaling step and a final projection.
  - A block can be read from its summary token or from the average of its 256 patch tokens.

**Speaker notes**

One piece of anatomy is needed before reading the blocks. At every block the model holds 257 tokens. 256 of them belong to patches of the photo, and they keep local detail: this patch is fur, this patch is tarmac. The last one, the summary token, has no patch. Its job is to collect what matters from the others, and it is the only token that reaches the output. That gives two readings of any block. Reading the summary token asks what the model is about to report. Averaging the patch tokens asks what the model still knows at that depth, reported or not. Keep that distinction; it decides the answer to this question.
