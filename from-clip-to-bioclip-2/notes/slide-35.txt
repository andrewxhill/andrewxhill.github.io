# Slide 35: Reading the patch tokens makes BioCLIP 2 better at telling alive from dead without lowering its naming

QUESTION 3 · ALL THE VARIANTS COMPARED

Right is better naming, up is better at telling alive from dead. The grey line is the weight mix from the starting model (Start) to BioCLIP 2. Dark points are block swaps between the two models; the hollow point swaps only the final steps.

Every weight change that raises the alive-or-dead score by more than a point lowers naming. Swapping blocks 23 and 24 gives 87.4% naming and 89.7% alive or dead; the 0.75 mix, 86.6% and 90.1%.

The teal diamond changes no weight. Patch tokens give 89.6% on alive or dead; the summary token still names 90.6%.

Final steps: rescaling and projection. 223 species; 1,323 photos of 115 held-out species. Unlabelled grey dots are mixes of 0.1, 0.25 and 0.9. The diamond pairs naming from the summary token with the alive-or-dead score from the patch tokens of the same unchanged model.

**Method notes**

The slide plots every variant by species naming and alive-or-dead accuracy.

- What was measured
  - Each point is one model variant, placed by naming accuracy and alive-or-dead accuracy.
  - The variants are weight mixes, block swaps and the patch-token reading.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - The grey line joins the weight mixes from the starting model to BioCLIP 2.
  - Dark points are BioCLIP 2 with the named parts copied from the starting model.
  - The diamond pairs naming from the summary token with alive or dead from patch tokens.
  - Both readings at the diamond come from the same unchanged BioCLIP 2.
  - Every variant is given the OpenAI pixel scaling.
- Numbers
  - The starting model sits at 43.2% naming and 91.4% alive or dead.
  - BioCLIP 2 sits at 90.6% naming and 85.7% alive or dead.
  - The 0.5 mix sits at 72.7% naming and 92.2% alive or dead.
  - The 0.75 mix sits at 86.6% naming and 90.1% alive or dead.
  - The mixes of 0.1, 0.25 and 0.9 name 49.6%, 58.0% and 90.2%.
  - The mixes of 0.1, 0.25 and 0.9 score 91.4%, 92.4% and 86.3% at alive or dead.
  - BioCLIP 2 with the starting model's blocks 23 and 24 sits at 87.4% and 89.7%.
  - Adding the final steps to the two-block swap gives 87.2% and 90.5%.
  - BioCLIP 2 with the starting model's block 24 sits at 89.45% and 88.56%.
  - BioCLIP 2 with the starting model's final steps sits at 91.04% and 86.03%.
  - BioCLIP 2 with the starting model's blocks 13 to 24 sits at 52.3% and 92.9%.
  - The starting model with BioCLIP 2's blocks 13 to 24 sits at 76.6% and 87.7%.
  - The diamond sits at 90.6% naming and 89.6% alive or dead.
- Uncertainty
  - Points close together on the chart may not differ beyond their intervals.
  - The alive-or-dead score of BioCLIP 2 has a 95% interval of 83.28% to 87.87%.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The chart covers two skills and does not show vehicle naming.
  - The diamond is two readings from one model and needs the patch tokens to be kept.

**Speaker notes**

Put everything that needs no training on one map. The two parents are the coloured dots: the starting model top left, BioCLIP 2 bottom right. The grey line is the weight mix from the first question. It bows upward, which is why the mix of 0.5 has 72.7% naming with no alive-or-dead loss. Further along, the mix of 0.75 has 86.6% naming and 90.1% alive-or-dead. The dark dots are block swaps. The two-block swap lands close to the 0.75 mix, at 87.4% and 89.7%, and adding the final steps moves it to 87.2% and 90.5%. Two different recipes, averaging every weight or replacing two blocks outright, arrive at about the same place, to the left of BioCLIP 2. The diamond is different in kind. Nothing in the model changes, so naming stays at 90.6%, and alive-or-dead read from the patch tokens is 89.6%. It is two readings from one model, so it needs the patch tokens kept at inference time. It is the only point that gains more than a point on alive or dead without giving up naming.
