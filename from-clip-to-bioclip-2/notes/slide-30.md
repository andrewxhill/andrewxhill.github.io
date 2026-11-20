# Slide 30: Can one model name species like BioCLIP 2 and tell alive from dead like the starting model?

QUESTION 3

A natural guess: only by training BioCLIP 2 again with telling alive from dead added as a goal, because the same weights produce both scores.

Swap blocks

Both models have the same 24 image blocks in the same layout. Copy some blocks from one model into the other and test the result.

Mix weights

Average every weight of the two models and test the result.

Read a different token

Leave BioCLIP 2 untouched and test its patch tokens in place of its summary token.

**Method notes**

The slide poses the third question and names three methods that need no training.

- What was measured
  - The third question is whether one model can keep both skills.
  - The two skills are naming species like BioCLIP 2 and telling alive from dead.
  - The slide states a guess and reports no result.
  - The guess is that only retraining BioCLIP 2 with an added goal could keep both.
- Method
  - Swapping blocks copies some of the 24 image blocks from one model into the other.
  - Mixing weights averages every weight of the two models.
  - Reading a different token tests BioCLIP 2's patch tokens in place of its summary token.
  - All three methods use the two finished models with no training.

**Speaker notes**

Everything on the next slides is done with the two finished models and no training at all. That is only possible because one was trained from the other, so their blocks still fit together.
