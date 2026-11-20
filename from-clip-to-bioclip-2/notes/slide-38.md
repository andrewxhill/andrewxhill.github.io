# Slide 38: Three methods beat the starting model at naming and BioCLIP 2 at telling alive from dead, with no retraining

LOOKING BACK · KEEPING BOTH SKILLS

All three use only the two finished models

Naming the species (scale 0 to 100%)

Telling alive animals from dead ones (scale 84% to 94%)

Each weight is the average of the two models’ values.

BioCLIP 2 unchanged: the summary token names the species and the patch tokens tell alive from dead.

BioCLIP 2 with the starting model’s image blocks 23 and 24.

Averaging the weights of a general model and a model trained from it is a known technique (Wortsman et al., 2022). Here the averaged model also keeps the starting model’s score at telling alive animals from dead ones, a task BioCLIP 2’s training never targeted.

Naming: 223 species, five example photos of each. Alive or dead: 1,323 photos of 115 held-out species.

**Method notes**

Three methods combine the two skills with no retraining, shown beside the two models.

- What was measured
  - The table reports species naming and alive-or-dead accuracy for five models.
  - The five models are the two finished models and three variants made from the two.
- Data
  - Naming uses 223 species with five example photos of each.
  - Alive or dead uses 1,323 photos of 115 species held out from the classifier.
- Method
  - Averaging the weights sets each weight to the average of the two models' values.
  - Reading two tokens leaves BioCLIP 2 unchanged.
  - With two tokens the summary token names species and the patch tokens tell alive from dead.
  - Exchanging two blocks gives BioCLIP 2 the starting model's image blocks 23 and 24.
  - Every row of the table is given the OpenAI pixel scaling.
- Numbers
  - The starting model names 43.2% and scores 91.4% at alive or dead.
  - BioCLIP 2 names 90.6% and scores 85.7% at alive or dead.
  - Averaging the weights gives 72.7% naming and 92.2% alive or dead.
  - Reading two tokens gives 90.6% naming and 89.6% alive or dead.
  - Exchanging two blocks gives 87.4% naming and 89.7% alive or dead.
  - The starting model names 45.5% on other slides, where its own pixel scaling is used.
- Uncertainty
  - The two-block gain of 4.06 points at alive or dead has an interval of 1.66 to 6.38.
  - The patch-token gain of 3.91 points has an interval of 1.57 to 6.23.
  - The averaged model's 92.2% has an interval of 90.5% to 94.0%.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The table does not show how the three methods behave for other pairs of models.
  - The table covers two skills only.
- Definitions
  - Averaging a general model with a model trained from it follows Wortsman et al. (2022).

**Speaker notes**

Here are the three options side by side, with the two finished models as reference rows. The starting model names 43.2% of species and scores 91.4% on alive or dead. BioCLIP 2 names 90.6% and scores 85.7%. Option one: average every weight, half and half. You get 72.7% naming and 92.2% on alive or dead, so a large part of the naming gain with none of the loss. Option two changes no weight at all: read the summary token for naming, 90.6%, and the patch tokens for alive or dead, 89.6%. Option three: give BioCLIP 2 the starting model’s blocks 23 and 24, for 87.4% and 89.7%. None of these needs a training run. Weight averaging between a general model and a model trained from it is the technique in Wortsman and colleagues’ 2022 paper on robust fine-tuning. What these numbers add is that it holds for alive or dead, a task the training never aimed at.
