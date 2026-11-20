# Slide 14: On bus photos BioCLIP 2 scores the name “streetcar” 0.566, above “bus” at 0.555

QUESTION 1 · BUS PHOTOS SCORED AGAINST FOUR NAMES

In the starting model a bus photo scores 0.250 against “bus” and 0.187 against “streetcar”, so it answers “bus”.

In BioCLIP 2 each of the four names measured scores higher on every one of the 1,000 vehicle photos. The right name rose least.

On a bus photo all four now score between 0.540 and 0.566, with “streetcar” highest.

The junco photo showed the same overall rise: its right name went from 0.291 to 0.717 and its highest wrong names rose too.

Bars: average cosine similarity between the 100 bus photos and each name. The model answers with the highest-scoring name.

**Method notes**

The slide shows the average score of bus photos against four vehicle names in each model.

- What was measured
  - The slide reports average cosine similarity between bus photos and four names.
  - The four names are 'bus', 'streetcar', 'rocket' and 'tank'.
- Data
  - The bars average the 100 CIFAR-100 bus test photos.
  - The statement about every photo covers all 1,000 vehicle test photos.
- Method
  - Each model encodes both the photos and the names.
  - Both models use the same OpenAI pixel scaling.
  - A model's answer for a photo is the name with the highest cosine similarity.
- Numbers
  - In the starting model bus photos score 0.250 against 'bus' and 0.187 against 'streetcar'.
  - In the starting model bus photos score 0.145 against 'rocket' and 0.131 against 'tank'.
  - In BioCLIP 2 bus photos score 0.555 against 'bus' and 0.566 against 'streetcar'.
  - In BioCLIP 2 bus photos score 0.540 against 'rocket' and 0.546 against 'tank'.
  - At a mix of 0.5 bus photos score 0.284 against 'bus' and 0.223 against 'streetcar'.
  - On all 1,000 vehicle photos BioCLIP 2 scores the right name higher than the starting model.
  - On all 1,000 photos BioCLIP 2 also scores 'rocket', 'streetcar' and 'tank' higher.
  - The junco photo's right name rose from 0.291 to 0.717 between the two models.
- Uncertainty
  - The bars are averages over 100 photos, and an average can hide differences between photos.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show which side of the model is responsible, because both changed.
  - Average scores do not give the rank of the right name within each photo.

**Speaker notes**

Here is what happens when a bus photo meets the names. In the starting model the right name scores 0.250 and the runner-up 0.187. The scores are low, but the gap between them is wide, and the gap decides the answer because the model just picks the top one. In BioCLIP 2 everything scores higher. That is true for every one of the 1,000 vehicle photos and for all four names measured: the right name, rocket, streetcar and tank. But they did not rise by the same amount. On average the right name rose least in each of the seven classes that are not themselves a rocket, streetcar or tank. For buses the four names end between 0.540 and 0.566, and streetcar is the one on top. This describes how the answer goes wrong. It does not say which side of the model is responsible, because both changed.
