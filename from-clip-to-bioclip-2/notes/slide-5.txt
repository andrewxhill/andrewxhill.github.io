# Slide 5: BioCLIP 2 scores a junco photo’s right name 0.717, up from 0.291, and its four highest wrong names higher too

ONE PHOTO SCORED AGAINST SPECIES NAMES

Dark-eyed Junco (Junco hyemalis), as the model sees it: 224 × 224 pixels. Photo (c) jessicaturtle, CC BY-NC, cropped.

Starting model

The right name scores highest, by a small margin. A lizard and a seal come next.

Halfway mix

The right name’s lead widens. A bird moves into second place.

BioCLIP 2

All five top names are now birds.

Scores are the cosine of the angle between photo and name (1 is a perfect match). The halfway mix averages every weight of the two models. The nine other names were drawn at random from the 223 species.

**Method notes**

The slide scores one junco photo against ten species names in three models.

- What was measured
  - The slide reports cosine similarity between one photo and each of ten species names.
  - The three models are the starting model, the halfway mix and BioCLIP 2.
- Data
  - The photo is one iNaturalist photo of a Dark-eyed Junco, licensed CC BY-NC.
  - The photo and the nine other names were drawn at random.
  - The nine other names come from the 223 species of the naming test.
- Method
  - Each name is given to the text side as the phrase 'a photo of a' plus the scientific name.
  - The score is the cosine between the photo's vector and the name's vector.
  - The starting model's score uses the starting model's own pixel scaling.
  - The halfway mix and BioCLIP 2 use the OpenAI pixel scaling.
  - The halfway mix averages every weight of the two models.
- Numbers
  - The right name, Junco hyemalis, scores 0.291 in the starting model, 0.2914 unrounded.
  - The right name scores 0.499 in the halfway mix.
  - The right name scores 0.717 in BioCLIP 2, 0.7172 unrounded.
  - The starting model's next four names score 0.248, 0.232, 0.229 and 0.218.
  - The halfway mix's next four names score 0.322, 0.261, 0.247 and 0.232.
  - BioCLIP 2's next four names score 0.592, 0.562, 0.560 and 0.558.
  - The starting model's runner-up is Zootoca vivipara, the viviparous lizard.
  - The starting model's third name is Phoca vitulina, the harbour seal.
  - BioCLIP 2's runner-up is Coccyzus americanus, the yellow-billed cuckoo.
  - All five of BioCLIP 2's top names are birds.
- Uncertainty
  - The scores describe a single photo, so no interval applies.
  - Only the top five scores per model were recorded for the ten-name list.
  - The right name ranks first in all three models.
  - The right name also ranks first against a second list of ten closely related names.
- Not shown
  - One photo does not establish how often either model ranks the right name first.
  - The slide does not show which side of the model raised the scores.
- Definitions
  - A cosine score of 1 would be a perfect match between a photo and a name.
  - Pixel scaling is the adjustment of pixel values that a model expects at its input.

**Speaker notes**

Zootoca vivipara is the viviparous lizard, Phoca vitulina the harbour seal, Grallina cyanoleuca the magpie-lark, Coccyzus americanus the yellow-billed cuckoo, Branta canadensis the Canada goose, Nycticorax nycticorax the black-crowned night heron. The photo and the nine other names were drawn at random.
