# Slide 19: BioCLIP 2 got worse at telling alive from dead and at naming vehicles from words, which fell from 93.0% to 45.8%

QUESTION 1 · ANSWER

Species naming rose from 45.5% to 90.6%. With every weight averaged between the two models, naming is 72.7% and telling alive from dead is no worse than in the starting model.

Worse at one question about animals

Accuracy at telling alive animals from dead ones fell from 92.1% to 85.7% in species the classifier had not seen. On 159 photos only the starting model is right, among them a robin on its back on tarmac.

Worse at matching vehicle photos to words

Vehicle photos named correctly from words fell from 93.0% to 45.8%. Named from example photos they fall 4.8 points, to 86.7%. On bus photos BioCLIP 2 scores “streetcar” above “bus”.

Similar photos are now mostly the same species

A photo’s most similar photos are the same species 79% of the time, up from 24%. They share its alive-or-dead label 59% of the time, down from 81%.

**Method notes**

The slide answers question 1 with the alive-or-dead, vehicle and similar-photo results.

- What was measured
  - The slide gathers the three checks of question 1 and reports no new measurement.
- Data
  - Alive or dead was tested on 1,323 photos of 115 species held out from the classifier.
  - Vehicle naming was tested on 1,000 CIFAR-100 photos of ten vehicle classes.
  - Species naming was tested on 3,734 photos of 223 species.
- Numbers
  - Species naming rose from 45.5% to 90.6%.
  - At the 0.5 mix naming is 72.7% and alive-or-dead accuracy is 92.2%.
  - Alive-or-dead accuracy fell from 92.1% to 85.7% on species the classifier had not seen.
  - Only the starting model is right on 159 photos.
  - Vehicle photos named correctly from words fell from 93.0% to 45.8%.
  - Named from example photos, vehicles fall 4.8 points, to 86.7%.
  - On bus photos BioCLIP 2 scores 'streetcar' at 0.566 and 'bus' at 0.555.
  - A photo's most similar photos are the same species 79% of the time, up from 24%.
  - A photo's most similar photos share its label 59% of the time, down from 81%.
- Uncertainty
  - The 95% interval on the alive-or-dead change is -9.5 to -3.4 points.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show where in the network the alive-or-dead loss arises.
  - Two tested skills do not establish what else BioCLIP 2 became worse at.

**Speaker notes**

Put the three checks together. BioCLIP 2 got worse in two places. One is inside biology: a property that cuts across species, alive or dead, is harder to read from BioCLIP 2’s output than from the starting model’s. The other is outside biology, and it is specific: named from example photos vehicles fall 4.8 points, and what fails is matching photos to everyday words. The neighbour counts say the same thing without any classifier: BioCLIP 2 rates photos of the same species as most alike. And remember the mix of 0.5, with 72.7% naming and no alive-or-dead loss. The loss does not grow evenly as the mix moves towards BioCLIP 2. The next question asks whether it is spread evenly through the network.
