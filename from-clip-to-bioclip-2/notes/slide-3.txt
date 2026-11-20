# Slide 3: A photo and a name each become 768 numbers

HOW THE MODEL READS A PHOTO AND A NAME

The model scores a photo against a name by the cosine of the angle between their two lists of numbers (cosine similarity). A small angle means a match.

Photo, 224 × 224 pixels

Cut into 256 patches of 14 × 14 pixels.

257 tokens, 1,024 wide

One per patch, plus one summary token (often called the class token) for the whole photo.

24 image blocks

Each block lets tokens read each other (attention), then reworks each one separately (a small feed-forward network, MLP).

768 numbers

The summary token after a final reshaping to 768 numbers (the projection).

Name, up to 77 tokens

Looked up in the word table of 49,408 token vectors.

Tokens, 768 wide

One per word piece, with its position added.

12 text blocks

The same two steps as the image blocks.

768 numbers

The end-of-text token after the same kind of final reshaping.

Image side: 303,966,208 numbers. Text side: 123,650,304. One more number sets the scale of the scores. Together: 427,616,513.

**Method notes**

The slide shows how a photo and a name each become a list of 768 numbers.

- What was measured
  - The slide counts the parts of the model and reports no test result.
  - The count of weights per part comes from the model's stored weights.
- Numbers
  - A photo enters the model at 224 by 224 pixels.
  - The photo is cut into 256 patches of 14 by 14 pixels.
  - The image side holds 257 tokens, each 1,024 numbers wide.
  - The 257 tokens are 256 patch tokens plus one summary token.
  - The image side has 24 blocks and the text side has 12 blocks.
  - A name can be up to 77 tokens long.
  - The word table holds 49,408 token vectors.
  - Text tokens are 768 numbers wide.
  - The image side has 303,966,208 weights and the text side has 123,650,304.
  - One further weight sets the scale of the scores, giving 427,616,513 in total.
  - The MLP layers of the 24 image blocks hold 201 million weights.
  - The attention layers of the 24 image blocks hold 101 million weights.
  - The patch filters at the front of the image side hold 602 thousand weights.
- Not shown
  - The slide does not show which parts changed during BioCLIP 2's training.
- Definitions
  - Cosine similarity is the cosine of the angle between two lists of numbers.
  - A cosine similarity near 1 means a photo and a name match closely.
  - A token is a list of numbers that stands for one patch or one word piece.
  - The summary token stands for the whole photo and is often called the class token.
  - Attention is the step in a block where tokens read from each other.
  - The MLP is a small feed-forward network that reworks each token separately.
  - The projection is the final reshaping of the summary token to 768 numbers.

**Speaker notes**

Two thirds of the image side's parameters sit in the MLP layers of the 24 blocks: 201 million, against 101 million in attention. The patch filters at the very front are only 602 thousand.
