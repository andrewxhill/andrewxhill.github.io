# From CLIP to BioCLIP 2

Method notes for each slide of the explainer at andrewxhill.com/from-clip-to-bioclip-2/.

Andrew Hill

## Slide 1: From CLIP to BioCLIP 2

ONE MODEL, BEFORE AND AFTER BIOLOGY TRAINING

BioCLIP 2 began as a general image–text model and was trained further on 214 million organism photos. It now names species twice as well. Both models have the same layout of 428 million weights, so each weight in one has a partner in the other and the two can be compared directly. Three questions follow: what did BioCLIP 2 get worse at, where in the network does it get worse, and can one model keep the naming without that loss?

45.5%

Starting model: species named correctly, given five example photos of each of 223 species

90.6%

The same test after BioCLIP 2’s training

**Method notes**

The cover states the comparison and the headline naming result, 45.5% against 90.6%.

- What was measured
  - The explainer compares the starting model with BioCLIP 2, which was trained from it.
  - The headline measurement is the share of species photos named correctly.
  - Naming is tested by giving a model five example photos of each of 223 species.
- Numbers
  - The starting model names 45.5% of species photos correctly, 45.49% unrounded.
  - BioCLIP 2 names 90.6% of species photos correctly, 90.63% unrounded.
  - BioCLIP 2 was trained further on 214 million organism photos.
  - Each model has 427,616,513 weights, which the cover rounds to 428 million.
  - Training also replayed 26 million general image and text pairs.
- Definitions
  - The starting model is the LAION-2B CLIP ViT-L/14 model.
  - A weight is one learned number in a model.
  - The two models share one layout, so each weight in one has a partner in the other.

**Speaker notes**

The starting model is LAION-2B CLIP ViT-L/14. BioCLIP 2 is the same architecture after training on TreeOfLife-200M with 26 million general image–text pairs replayed. Naming here is nearest class mean from five example photos per species, scored on 223 species of iNaturalist photos. The rest of the talk is three questions, each with a guess first and then the measurements.

## Slide 2: The two models are two files of 427,616,513 numbers, laid out the same way

THE TWO MODELS

BioCLIP 2’s authors did not start from random weights. They loaded the LAION-2B CLIP ViT-L/14 weights and kept training them on organism photos. Nothing was added or removed, so each number in one file has a partner in the other.

Starting model

LAION-2B CLIP ViT-L/14

Trained on about 2.3 billion image–caption pairs from the web.

BioCLIP 2

The same network, trained further

214 million organism images with their taxonomic names, plus 26 million general web photos and captions mixed back in, so it would not forget everything else.

A mix

Any mix of the two

For every number, mix the two values: α parts BioCLIP 2 and 1 − α parts the starting model. α = 0 is the starting model and α = 1 is BioCLIP 2. Each mix is a working model.

Sources: LAION-2B CLIP model card; Gu et al. 2025, BioCLIP 2.

**Method notes**

The slide introduces the two models and the idea of mixing their weights.

- What was measured
  - The slide describes the two models and reports no test result.
  - BioCLIP 2 was trained starting from the starting model's weights, not from random weights.
  - No weights were added or removed, so the two files of weights line up one to one.
- Numbers
  - Each model is a file of 427,616,513 numbers.
  - The starting model was trained on about 2.3 billion image and caption pairs from the web.
  - BioCLIP 2 was trained further on 214 million organism images with taxonomic names.
  - BioCLIP 2's training mixed in 26 million general web photos and captions.
- Not shown
  - The slide does not show that every mix works well, only that every mix can be run.
  - The share alpha is a share of weights and is not an amount of training.
- Definitions
  - A mix sets every weight to alpha parts BioCLIP 2 and 1 minus alpha parts starting model.
  - A mix of alpha 0 is the starting model and a mix of alpha 1 is BioCLIP 2.
  - Mixing two models' weights by a share alpha is weight interpolation (Wortsman et al., 2022).
  - Weight interpolation is possible because one model was trained from the other.

**Speaker notes**

The mixing trick is weight interpolation, as in WiSE-FT (Wortsman et al. 2022). It works here because the two models share an architecture and one was trained from the other. Alpha is a share of weights.

## Slide 3: A photo and a name each become 768 numbers

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

## Slide 4: Training on organism photos changed the first-layer filters by 20% and the text side’s word table by 88%

THE FIRST-LAYER FILTERS, DRAWN AS PICTURES

Starting model

BioCLIP 2

Difference, shown 4× brighter

Each tile is one 14 × 14 pixel filter that reads a patch of the photo. Tiles are ordered by how much they changed. Training changed these filters by 20% of their original size.

**Method notes**

The slide draws the first-layer filters of both models and the difference between them.

- What was measured
  - The slide compares the first-layer patch filters of the two models as pictures.
  - A change's size is the norm of the weight difference over the norm of the starting weights.
- Data
  - The pictures use the stored weights of the two models and no photos.
  - The first layer has 1,024 filters, each covering a 14 by 14 pixel patch in colour.
- Method
  - Each tile colours the weights of one filter.
  - Tiles are ordered by how much each filter changed, largest squared change first.
  - The two model grids share one colour scale and the difference grid has a second scale.
  - The difference grid is shown four times brighter.
- Numbers
  - The first-layer filters changed by 20% of their original size, 0.201 unrounded.
  - The text side's word table changed by 88% of its original size, 0.877 unrounded.
  - Across all image-side weights the relative change is 0.22.
  - Across all text-side weights the relative change is 0.28.
- Uncertainty
  - The change figures are exact properties of the two weight files, with no sampling.
- Not shown
  - The slide does not show what effect the filter change has on any test score.
  - The word table is described by one number and is not drawn.
  - The slide does not show that the word-table change causes any later result.
- Definitions
  - A first-layer filter is the set of weights that reads one patch of pixels.
  - The word table is the text side's list of one vector per token.

**Speaker notes**

This is the patch-embedding layer, the only weights in a vision transformer that can be drawn directly as small images. The stripes and blobs are edge and colour detectors. They still look alike by eye; the change is 20% by size. The change is relative L2 norm of the difference over the norm of the start: 0.20 for these filters, 0.88 for the text side’s word table.

## Slide 5: BioCLIP 2 scores a junco photo’s right name 0.717, up from 0.291, and its four highest wrong names higher too

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

## Slide 6: BioCLIP 2 names 90.6% of photos of 223 species correctly, up from the starting model’s 45.5%

WHAT TRAINING IMPROVED

+45 points

Give the model five example photos of each species, then ask it to name new photos. BioCLIP 2 gets 9 in 10 right.

Each model expects pixel values adjusted in its own way (input scaling). The 45.5% and 90.6% give each model its own. The curve uses BioCLIP 2’s for every mix, so the starting model scores 43.2% on it.

Horizontal axis: BioCLIP 2’s share of every weight, from 0, the starting model (Start), to 1, BioCLIP 2. iNaturalist photos, 223 species. Each mix names more photos correctly than the one before it.

**Method notes**

The slide shows species naming accuracy for seven mixes from the starting model to BioCLIP 2.

- What was measured
  - The slide reports the share of species photos named correctly from five example photos.
  - The curve reports the same score for seven mixes of the two models' weights.
- Data
  - The naming test uses 3,734 iNaturalist test photos of 223 species.
  - The 223 species belong to 89 families.
  - Example photos and test photos are different photos.
- Method
  - Each species is represented by the average image vector of five example photos.
  - A test photo is given the species whose average vector is closest in direction.
  - Naming accuracy is averaged over 20 random draws of the five example photos.
  - Each of the 223 species has equal weight in the naming score.
  - The naming method is known as nearest class mean.
  - The two headline figures give each model its own pixel scaling.
  - The curve gives every mix the OpenAI pixel scaling, which BioCLIP 2 expects.
- Numbers
  - The starting model names 45.5% correctly with its own pixel scaling, 45.49% unrounded.
  - BioCLIP 2 names 90.6% of photos correctly, 90.63% unrounded.
  - The gain shown as +45 points is 45.14 points unrounded.
  - On the curve the starting model scores 43.2%, 43.21% unrounded.
  - The curve reads 43.21%, 49.61%, 58.04%, 72.65%, 86.62%, 90.24% and 90.63%.
  - The seven curve points are mixes of 0, 0.1, 0.25, 0.5, 0.75, 0.9 and 1.
- Uncertainty
  - The starting model's 45.49% has a 95% interval of 42.75% to 48.11% across species.
  - BioCLIP 2's 90.63% has a 95% interval of 89.34% to 91.91% across species.
  - The 95% interval on the gain across species families is 41.9 to 48.5 points.
  - Intervals come from resampling species 2,000 times and taking the middle 95% of results.
- Not shown
  - The slide does not show naming from words, only naming from example photos.
  - The slide covers 223 species and does not show other species.
- Definitions
  - A mix of 0.5 sets every weight to the average of the two models' values.
  - Input scaling is the adjustment of pixel values that each model expects.

**Speaker notes**

Naming is nearest class mean: average the embeddings of five example photos per species, then assign each test photo to the closest average. Twenty draws of the five examples. The 95% interval on the gain across species families is 41.9 to 48.5 points.

## Slide 7: What did BioCLIP 2 get worse at?

QUESTION 1

A natural guess: only subjects far from biology. Training on organism photos made BioCLIP 2 better at naming species, and it should be no worse at any other question about animals.

Check 1: a question about animals that BioCLIP 2 was not trained on

Is the animal in the photo alive or dead? BioCLIP 2 was trained to match photos to taxonomic names, so its training did not target this.

Check 2: a subject outside biology

Ten kinds of vehicle, from bicycle to rocket, named from words and from example photos.

Check 3: which photos each model treats as alike

Pick one photo and ask each model which other photos it rates as most similar.

**Method notes**

The slide poses the first question and names three checks used to answer it.

- What was measured
  - The first question is what BioCLIP 2 became worse at.
  - The slide states a guess and reports no result.
  - The guess is that BioCLIP 2 is worse only on subjects far from biology.
- Method
  - Check 1 asks whether the animal in a photo is alive or dead.
  - BioCLIP 2's training matched photos to taxonomic names and never asked alive or dead.
  - Check 2 names ten kinds of vehicle from words and from example photos.
  - Check 3 asks which other photos each model rates as most similar to a chosen photo.

**Speaker notes**

Before looking at any result, say the guess out loud. Most people expect a specialist model to be at least as good as the generalist on anything about animals, and to lose only on things like cars and furniture. The next slides test that with one biology question that was never a training target, one subject outside biology, and a look at which photos each model puts side by side.

## Slide 8: BioCLIP 2 scores 85.7% at telling alive animals from dead ones; the starting model scores 92.1%

QUESTION 1 · ALIVE OR DEAD

92.1% → 85.7%

Balanced accuracy (the average of accuracy on alive photos and on dead ones), worked out for each of 115 held-out species and then averaged: starting model, then BioCLIP 2.

A simple classifier reads “alive” or “dead” from the model’s 768 numbers. For species it was trained on, the score stays near 91%. The score falls only for species it was not trained on.

Horizontal axis: BioCLIP 2’s share of every weight, from 0, the starting model, to 1, BioCLIP 2. 95% interval on the change: −9.5 to −3.4 points. Every mix is given BioCLIP 2’s adjustment of pixel values, so the starting model scores 91.4% here.

**Method notes**

The slide shows alive-or-dead accuracy for seven mixes, for seen and held-out species.

- What was measured
  - The slide reports how well a classifier reads alive or dead from a model's 768 numbers.
  - One line covers species the classifier was trained on.
  - The other line covers species held out from the classifier.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
  - The 115 species belong to 60 families.
- Method
  - The classifier is logistic regression fitted to a frozen model's image vector.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Accuracy on alive photos and accuracy on dead photos are averaged within each species.
  - The reported score is the mean of the 115 species scores, with each species weighted equally.
  - The two headline figures give each model its own pixel scaling.
  - The curve gives every mix the OpenAI pixel scaling, which BioCLIP 2 expects.
- Numbers
  - On held-out species the starting model scores 92.1%, 92.14% unrounded.
  - On held-out species BioCLIP 2 scores 85.7%, 85.68% unrounded.
  - On the curve the starting model scores 91.4% on held-out species, 91.41% unrounded.
  - The held-out curve reads 91.41%, 91.43%, 92.39%, 92.23%, 90.10%, 86.25% and 85.68%.
  - The seen-species curve reads 91.99%, 92.27%, 92.97%, 93.91%, 92.53%, 91.37% and 91.16%.
  - The seven curve points are mixes of 0, 0.1, 0.25, 0.5, 0.75, 0.9 and 1.
- Uncertainty
  - The 95% interval on the change from 92.1% to 85.7% is -9.5 to -3.4 points.
  - The starting model's 92.14% has a 95% interval of 90.06% to 93.95% across species.
  - BioCLIP 2's 85.68% has a 95% interval of 83.28% to 87.87% across species.
  - Intervals come from resampling species 2,000 times and taking the middle 95% of results.
  - With C fixed at 1 the two models score 88.97% and 83.89% on held-out species.
- Not shown
  - The slide does not show why the score falls for held-out species.
  - Adult-or-juvenile and female-or-male tests showed a similar widening gap of about 5 points.
  - The adult-or-juvenile decline did not repeat on 100 confirmation species.
- Definitions
  - Balanced accuracy is the average of accuracy on alive photos and on dead photos.
  - A held-out species is one whose photos were never used to fit the classifier tested on it.

**Speaker notes**

The classifier is logistic regression on frozen embeddings. Unseen species means the species and its photographers were held out of classifier training.

## Slide 9: 159 photos are labelled alive or dead correctly by the starting model alone, and 59 by BioCLIP 2 alone

QUESTION 1 · PHOTO BY PHOTO

All 1,323 test photos, by which model’s classifier labels them correctly

656 photos recorded as alive

667 photos recorded as dead

The 159 photos only the starting model gets right split evenly: 78 alive animals and 81 dead ones. Of the 59 only BioCLIP 2 gets right, 39 are dead animals and 20 alive. Counting every photo equally, the starting model is right on 92.4% and BioCLIP 2 on 84.8%; counting each of the 115 species equally gives 92.1% and 85.7%.

Right means the classifier agrees with the alive-or-dead label recorded by the iNaturalist contributor. 115 species, each tested by a classifier trained without that species.

**Method notes**

The slide counts the 1,323 test photos by which model's classifier labels them correctly.

- What was measured
  - The slide counts photos on which each model's alive-or-dead classifier is right.
  - A classifier is right when it agrees with the label recorded by the contributor.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
- Method
  - Each species is tested by a classifier fitted without that species.
  - The classifiers are those of the first study, each with its own model's pixel scaling.
  - Pixel scaling and model weights therefore both differ between the two classifiers.
  - A classifier predicts dead when its score for a photo is above zero.
- Numbers
  - Both classifiers are right on 1,063 photos and both are wrong on 42.
  - Only the starting model's classifier is right on 159 photos.
  - Only BioCLIP 2's classifier is right on 59 photos.
  - Of 656 alive photos, both classifiers are right on 539 and both are wrong on 19.
  - Of 656 alive photos, only the starting model is right on 78 and only BioCLIP 2 on 20.
  - Of 667 dead photos, both classifiers are right on 524 and both are wrong on 23.
  - Of 667 dead photos, only the starting model is right on 81 and only BioCLIP 2 on 39.
  - Counting photos equally, the starting model is right on 92.4% and BioCLIP 2 on 84.8%.
  - Counting the 115 species equally gives 92.1% and 85.7%.
  - The Common Hedgehog has the most disagreements, 7 of its 12 photos.
  - Of the 7 hedgehog disagreements, 4 favour the starting model and 3 favour BioCLIP 2.
- Uncertainty
  - The counts are exact for the 1,323 test photos and carry no interval.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The counts do not show why a classifier misses a given photo.
  - The counts do not separate the effect of pixel scaling from the effect of the weights.

**Speaker notes**

A percentage hides what is happening to individual photos, so here is the same result as a count. Both classifiers agree with the label on 1,063 photos and both miss 42. The two middle slices are where the models differ: 159 photos that only the starting model gets right and 59 that only BioCLIP 2 gets right. The starting model’s extra wins are not concentrated in one label; they are half alive and half dead. The species with the most photos on which the two classifiers disagree is the common hedgehog, 7 of its 12 photos. The next two slides show what these photos look like.

## Slide 10: Eight photos the starting model labels correctly as alive or dead and BioCLIP 2 labels wrongly

QUESTION 1 · PHOTOS BIOCLIP 2 GETS WRONG

Top row. A dead robin on its back on tarmac, a dead hare on tarmac, a dead red squirrel on a lawn and a dead young robin on paving tiles. BioCLIP 2’s classifier calls all four alive.

Bottom row. A live red squirrel on a tree trunk, two live ovenbirds among leaves and a live hedgehog on grass at night. It calls all four dead.

The starting model’s classifier gets all eight right.

Eight of the 159 photos only the starting model gets right: the largest disagreements between the two classifiers among photos with a display licence. The word under each photo is the status its contributor recorded. iNaturalist photos, cropped; credits on the last slide.

**Method notes**

The slide shows eight photos that only the starting model's classifier labels correctly.

- What was measured
  - The slide shows examples from the 159 photos only the starting model gets right.
  - The word under each photo is the alive-or-dead status its contributor recorded.
- Data
  - The eight photos are iNaturalist test photos, cropped to the models' input.
  - Four photos are recorded as dead and four as alive.
  - The dead animals are two European Robins, a Brown Hare and an American Red Squirrel.
  - The alive animals are a Eurasian Red Squirrel, two Ovenbirds and a Common Hedgehog.
- Method
  - Photos are ranked by the gap between the two classifiers' signed distances from the boundary.
  - A distance counts as positive when the classifier leans towards the recorded label.
  - Only photos with a display licence are shown.
  - Photos showing graphic injury or decomposition were skipped.
  - The eight photos shown are the eight highest-ranked photos that could be displayed.
- Numbers
  - BioCLIP 2's classifier calls the four dead animals alive.
  - BioCLIP 2's classifier calls the four alive animals dead.
  - The starting model's classifier labels all eight photos correctly.
  - The eight photos are 8 of 159.
- Uncertainty
  - Eight photos are examples and are not a random sample of the 159.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The photos show what a miss looks like and do not show why the classifier misses.
  - The slide does not show which parts of a photo either classifier relies on.

**Speaker notes**

Look at the top row first. A robin on its back on a road, a hare on its side on tarmac, a squirrel on a lawn, a fledgling on tiles. BioCLIP 2’s classifier says alive for all four. The bottom row goes the other way: a squirrel climbing a trunk, two ovenbirds perched in foliage and a hedgehog on grass are called dead. These are eight photos out of 159, chosen because the two classifiers disagree on them most. They show what a miss looks like. They do not say why the classifier misses.

## Slide 11: Eight photos BioCLIP 2 labels correctly as alive or dead and the starting model labels wrongly

QUESTION 1 · PHOTOS THE STARTING MODEL GETS WRONG

Top row. A dead gecko on a tree trunk, a dead hedgehog beside long grass, a dead hedgehog on gravel and a dead junco on a window ledge.

Bottom row. A dead owl in a cardboard box, a dead skunk on a road, live wapiti on a clifftop and a live dog asleep on the ground.

The starting model’s classifier calls the six dead animals alive and the two live ones dead. BioCLIP 2’s classifier gets all eight right.

Eight of the 59 photos only BioCLIP 2 gets right: the largest disagreements between the two classifiers among photos with a display licence. The word under each photo is the status its contributor recorded. iNaturalist photos, cropped; credits on the last slide.

**Method notes**

The slide shows eight photos that only BioCLIP 2's classifier labels correctly.

- What was measured
  - The slide shows examples from the 59 photos only BioCLIP 2 gets right.
  - The word under each photo is the alive-or-dead status its contributor recorded.
- Data
  - The eight photos are iNaturalist test photos, cropped to the models' input.
  - Six photos are recorded as dead and two as alive.
  - The dead animals are a Moorish Gecko, two Common Hedgehogs and a Dark-eyed Junco.
  - The other dead animals are a Great Horned Owl and a Striped Skunk.
  - The alive animals are Wapiti on a clifftop and a sleeping Domestic Dog.
- Method
  - Photos are ranked by the gap between the two classifiers' signed distances from the boundary.
  - A distance counts as positive when the classifier leans towards the recorded label.
  - Only photos with a display licence are shown.
  - Photos showing graphic injury or decomposition were skipped.
  - The eight photos shown are the eight highest-ranked photos that could be displayed.
- Numbers
  - The starting model's classifier calls the six dead animals alive.
  - The starting model's classifier calls the two alive animals dead.
  - BioCLIP 2's classifier labels all eight photos correctly.
  - The eight photos are 8 of 59, against 159 photos going the other way.
- Uncertainty
  - Eight photos are examples and are not a random sample of the 59.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The photos do not show why the starting model's classifier misses.

**Speaker notes**

The disagreement runs both ways. Here BioCLIP 2’s classifier is right and the starting model’s is wrong: a gecko on a trunk, two hedgehogs, a junco on a window ledge, an owl in a box, a skunk seen through a windscreen, wapiti on the horizon, and a sleeping dog that the starting model reads as dead. There are 59 of these against 159 going the other way.

## Slide 12: Given ten vehicle names to choose from, BioCLIP 2 calls 83% of motorcycle photos “rocket”

QUESTION 1 · NAMING VEHICLES

93.0% → 45.8%

Vehicle photos named correctly from words, starting model then BioCLIP 2. The model compares each photo with ten phrases such as “a photo of a bus” and picks the closest.

91.5% → 86.7%

The same photos named with no words involved: the model is given five example photos of each vehicle. The score falls 4.8 points.

Violet and teal bars: the share of each vehicle’s 100 test photos that each model names correctly from words. Copper bars: the share BioCLIP 2 gives its most common wrong name. Ten vehicle classes from a standard set of small labelled photos (CIFAR-100), enlarged to 224 pixels.

**Method notes**

The slide shows how often each model names ten kinds of vehicle correctly from words.

- What was measured
  - The slide reports the share of vehicle photos given the right name out of ten names.
  - The slide also reports the wrong name BioCLIP 2 gives most often for each vehicle.
- Data
  - The photos are ten vehicle classes from CIFAR-100, a standard set of small labelled photos.
  - Each vehicle class has 100 test photos, 1,000 in all.
  - The small photos are enlarged to 224 pixels.
- Method
  - Naming from words compares each photo with ten phrases such as 'a photo of a bus'.
  - The model's answer is the phrase with the highest cosine similarity to the photo.
  - Naming from example photos uses five example photos per vehicle and no words.
  - Naming from example photos is averaged over 20 draws of the five examples.
  - Both models use the same OpenAI pixel scaling in the figures on the slide.
- Numbers
  - From words the starting model names 93.0% of vehicle photos and BioCLIP 2 names 45.8%.
  - From example photos the two models name 91.5% and 86.7%, 91.46% and 86.69% unrounded.
  - The fall from example photos is 4.8 points, 4.77 unrounded.
  - Rocket: starting model 99%, BioCLIP 2 100%.
  - Streetcar: starting model 68%, BioCLIP 2 96%, with rocket the top wrong name at 3%.
  - Tank: starting model 98%, BioCLIP 2 83%, with rocket the top wrong name at 14%.
  - Bicycle: starting model 96%, BioCLIP 2 71%, with rocket the top wrong name at 22%.
  - Tractor: starting model 95%, BioCLIP 2 29%, with tank the top wrong name at 48%.
  - Bus: starting model 88%, BioCLIP 2 24%, with streetcar the top wrong name at 50%.
  - Pickup truck: starting model 97%, BioCLIP 2 21%, with streetcar the top wrong name at 32%.
  - Lawn mower: starting model 98%, BioCLIP 2 14%, with rocket the top wrong name at 52%.
  - Train: starting model 92%, BioCLIP 2 12%, with streetcar the top wrong name at 38%.
  - Motorcycle: starting model 99%, BioCLIP 2 8%, with rocket the top wrong name at 83%.
  - With its own pixel scaling the starting model names 95.6% of vehicle photos from words.
- Uncertainty
  - Each per-class percentage rests on 100 photos.
  - The per-class table was computed independently from saved image and text vectors.
  - No interval is reported for the vehicle scores from words.
- Not shown
  - The slide does not show which side of the model causes the wrong names.
  - Ten vehicle classes do not establish how BioCLIP 2 names other everyday objects.

**Speaker notes**

Now the check outside biology. There are two ways to ask a model like this what is in a photo. One uses words: compare the photo with the text “a photo of a bus”, “a photo of a tractor” and so on. The other uses no words: show five example photos of each class and pick the nearest group. From example photos BioCLIP 2 falls 4.8 points, 91.5% to 86.7%. From words it falls from 93.0% to 45.8%. And the errors are not scattered. Read down the copper bars: 83% of motorcycles are called rocket, 52% of lawn mowers are called rocket, 50% of buses and 38% of trains are called streetcar, 48% of tractors are called tank. Rocket, streetcar and tank photos are still named correctly, because those three names win almost everything.

## Slide 13: In BioCLIP 2 the ten vehicle names are less similar to each other: 0.662 on average, down from 0.774

QUESTION 1 · THE VEHICLE NAMES COMPARED WITH EACH OTHER

Each cell compares two vehicle names by cosine similarity, where 1 means the model treats the two names as identical. Darker is more alike.

A natural guess: the text side forgot these words, so it now gives “bus” and “streetcar” almost the same numbers.

The grids show the opposite. In BioCLIP 2 almost every cell is lighter. “Bus” and “streetcar” are still each other’s closest name, at 0.741, down from 0.863.

Columns follow the same order as the rows. The grey diagonal is each name with itself. Colour runs from white at a similarity of 0.5 to full copper at 0.95. Names were given as “a photo of a bus” and so on.

**Method notes**

The slide compares the ten vehicle names with each other in each model's text side.

- What was measured
  - The slide reports cosine similarity between the text vectors of pairs of vehicle names.
  - The comparison uses the text side only and involves no photos.
- Data
  - The ten names are the ten vehicle classes, each given as 'a photo of a bus' and so on.
  - The average covers the 90 ordered pairs of different vehicle names.
- Method
  - Each grid cell is the cosine similarity between two names' text vectors.
  - Cell colour runs from white at a similarity of 0.5 to full copper at 0.95.
  - The grey diagonal is each name compared with itself.
- Numbers
  - The average similarity between different vehicle names is 0.774 in the starting model.
  - The average similarity between different vehicle names is 0.662 in BioCLIP 2.
  - At a mix of 0.5 the average similarity is 0.668.
  - The names 'bus' and 'streetcar' have similarity 0.863 in the starting model.
  - The names 'bus' and 'streetcar' have similarity 0.741 in BioCLIP 2.
  - The name 'streetcar' stays the closest name to 'bus' in all three models.
  - Training changed the text side's word table by 88%, 0.877 unrounded.
- Uncertainty
  - The name similarities are exact for the ten phrases and carry no interval.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show that the word-table change is the reason for the wrong names.
  - Similarity between names does not by itself show how photos score against names.

**Speaker notes**

The obvious explanation for the last slide is that the text side has forgotten what these words mean, and bus, streetcar and train now get almost the same numbers. That would show up here as a darker grid. It is the other way round. The average similarity between different vehicle names goes down, from 0.774 to 0.662, and it is already 0.668 at a mix of 0.5, where naming from words still works. The words are further apart than before, and each name’s nearest neighbour is still a sensible one: bus with streetcar, bicycle with motorcycle, lawn mower with tractor. We saw earlier that the word table changed by 88%. That is a fact about the text side; this slide does not show it is the reason. The next slide looks at the photos against the names.

## Slide 14: On bus photos BioCLIP 2 scores the name “streetcar” 0.566, above “bus” at 0.555

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

## Slide 15: Of the 8 photos each model rates most like a robin photo, BioCLIP 2 picks 7 robins and the starting model 1

QUESTION 1 · WHAT EACH MODEL TREATS AS ALIKE

The photo we ask about: a European Robin, small and far away, which the starting model usually misnames.

Starting model · 1 of 8 is a robin

Weights mixed, 0.75 BioCLIP 2 · 6 of 8 are robins

BioCLIP 2 · 7 of 8 are robins

Most similar first, from other photographers only. iNaturalist photos, CC BY and CC BY-NC, cropped; credits on the last slide.

**Method notes**

The slide shows the eight photos each of three models rates most like one robin photo.

- What was measured
  - The slide shows which photos each model rates as most similar to one chosen photo.
  - The count under each row is how many of the eight photos are European Robins.
- Data
  - The chosen photo is an iNaturalist photo of a European Robin, small in the frame.
  - The photos are licensed CC BY or CC BY-NC and are cropped.
- Method
  - Each model ranks the other photos by similarity of image vectors to the chosen photo.
  - Photos by the same photographer as the chosen photo are excluded.
  - The eight shown are the nearest eight with a display licence that passed visual review.
  - The starting model row uses the starting model's own pixel scaling.
  - The 0.75 mix and BioCLIP 2 rows use the OpenAI pixel scaling.
- Numbers
  - In the starting model 1 of the 8 most similar photos is a robin.
  - In the 0.75 mix 6 of the 8 most similar photos are robins.
  - In BioCLIP 2 7 of the 8 most similar photos are robins.
  - From five examples the starting model names the chosen photo correctly in 1 of 20 draws.
  - From five examples BioCLIP 2 names the chosen photo correctly in 20 of 20 draws.
- Uncertainty
  - The slide shows one chosen photo and carries no interval.
- Not shown
  - One photo does not establish how often the pattern holds across photos.
  - The rows after review can differ from the nearest eight in the full set of photos.

**Speaker notes**

The starting model groups this photo with other small birds in green foliage: similar scenes. BioCLIP 2 groups it with robins in quite different scenes: the same species. With five examples per species, the starting model names this photo correctly in 1 of 20 draws; BioCLIP 2 in 20 of 20.

## Slide 16: The 8 photos the starting model rates most like a dead moose are all dead animals; BioCLIP 2’s are mostly kangaroos

QUESTION 1 · WHAT EACH MODEL TREATS AS ALIKE

The photo we ask about: a Moose, dead.

Starting model · 8 of 8 are dead animals, none is a moose

Weights mixed, 0.75 BioCLIP 2 · 4 of 8 are dead, 1 is a moose

BioCLIP 2 · 5 kangaroos, 2 moose and a wombat; 3 of the 8 are dead

Most similar first, from other photographers only. iNaturalist photos, CC BY and CC BY-NC, cropped; credits on the last slide.

**Method notes**

The slide shows the eight photos each of three models rates most like a dead moose photo.

- What was measured
  - The slide shows which photos each model rates as most similar to one chosen photo.
  - The counts are how many of the eight are dead animals and how many are moose.
- Data
  - The chosen photo is an iNaturalist photo of a Moose recorded as dead.
  - The photos are licensed CC BY or CC BY-NC and are cropped.
- Method
  - Each model ranks the other photos by similarity of image vectors to the chosen photo.
  - Photos by the same photographer as the chosen photo are excluded.
  - The eight shown are the nearest eight with a display licence that passed visual review.
  - The starting model row uses the starting model's own pixel scaling.
  - The 0.75 mix and BioCLIP 2 rows use the OpenAI pixel scaling.
- Numbers
  - In the starting model 8 of the 8 most similar photos are dead animals and none is a moose.
  - In the 0.75 mix 4 of the 8 most similar photos are dead and 1 is a moose.
  - In BioCLIP 2 the 8 most similar photos are 5 kangaroos, 2 moose and a wombat.
  - In BioCLIP 2 3 of the 8 most similar photos are dead and 5 are alive.
- Uncertainty
  - The slide shows one chosen photo and carries no interval.
- Not shown
  - One photo does not establish the pattern, which the next slide counts over 1,323 photos.

**Speaker notes**

For the starting model, "a dead animal on the ground" is the strongest thing about this photo, whatever the species. BioCLIP 2’s eight are five kangaroos, two moose and a wombat, and five of the eight are alive. This is one example of what the next slide counts across all 1,323 photos.

## Slide 17: In BioCLIP 2, 59% of a photo’s most similar photos share its alive-or-dead label, down from 81%

QUESTION 1 · EACH PHOTO’S MOST SIMILAR PHOTOS

81% → 59%

For each photo, take the eight photos a model rates most similar. In the starting model, 81% share its alive-or-dead label. In BioCLIP 2, 59% do, nine points above chance.

The share of the same species rises from 24% to 79%. A classifier still tells alive from dead from BioCLIP 2’s 768 numbers (85.7%), but photos with the same label are now only slightly more likely to be rated similar.

Horizontal axis: BioCLIP 2’s share of every weight (0 is the starting model). All 1,323 alive-or-dead test photos, similar photos by other photographers only.

**Method notes**

The slide counts how often a photo's eight most similar photos share its label or species.

- What was measured
  - The slide reports the share of a photo's eight most similar photos with the same label.
  - The slide also reports the share of the eight that are the same species.
- Data
  - The count covers all 1,323 alive-or-dead test photos.
  - Each photo has eight most similar photos, giving 10,584 comparisons per model.
- Method
  - Each model ranks photos by similarity of image vectors, with no classifier involved.
  - Similar photos by the same photographer as the chosen photo are excluded.
  - The figures on the slide give every mix the OpenAI pixel scaling.
- Numbers
  - In the starting model 81% of similar photos share the label, 81.39% unrounded.
  - In BioCLIP 2 59% of similar photos share the label, 59.10% unrounded.
  - The same-species share rises from 24% to 79%, 24.38% and 79.00% unrounded.
  - Chance for sharing the alive-or-dead label is 50%, 49.95% unrounded.
  - Chance for sharing the species is 0.86%.
  - At a mix of 0.5 the label share is 73.35% and the same-species share is 53.00%.
  - At a mix of 0.75 the label share is 65.16% and the same-species share is 71.46%.
  - With its own pixel scaling the starting model's two shares are 82.24% and 25.51%.
  - A classifier still reads alive or dead from BioCLIP 2's 768 numbers at 85.7%.
- Uncertainty
  - No interval is reported for the neighbour shares.
- Not shown
  - The neighbour shares do not show why BioCLIP 2 groups photos by species.
- Definitions
  - A photo's most similar photos are those whose image vectors are closest to its own.

**Speaker notes**

This needs no classifier at all, only distances between embeddings, and it agrees with the classifier result. The starting model rates dead animals of different species as similar to each other. BioCLIP 2 rates photos of the same species as most similar, and what is left of the alive-or-dead signal is weaker across species.

## Slide 18: Averaging the two models’ weights gives 72.7% on species naming and 92.2% at telling alive from dead

QUESTION 1 · MIXING THE TWO MODELS’ WEIGHTS

72.7%

Species naming at a mix of 0.5, where every weight is the average of the two models’ values. That is 62% of the way from 43.2% to 90.6%.

92.2%

Telling alive from dead at the same mix; the starting model scores 91.4%. Past 0.5 it falls: 90.1% at 0.75, 86.3% at 0.9.

Naming vehicles from words is 92.8% correct at this mix.

Horizontal axis: BioCLIP 2’s share of every weight (0 is the starting model). 223 species; 1,323 photos of 115 held-out species.

**Method notes**

The slide puts the naming curve and the alive-or-dead curve on the same axes.

- What was measured
  - The slide reports species naming and alive-or-dead accuracy at seven weight mixes.
  - The highlighted point is the mix of 0.5, where every weight is the two models' average.
- Data
  - The naming test uses 3,734 iNaturalist test photos of 223 species.
  - The alive-or-dead test uses 1,323 photos of 115 held-out species.
- Method
  - Naming uses five example photos per species, averaged over 20 draws.
  - Alive or dead uses a logistic regression classifier tested on held-out species.
  - Every mix on both curves is given the OpenAI pixel scaling.
- Numbers
  - At a mix of 0.5 naming is 72.7%, 72.65% unrounded.
  - The naming value at 0.5 is 62% of the way from 43.2% to 90.6%.
  - At a mix of 0.5 alive-or-dead accuracy is 92.2%, 92.23% unrounded.
  - The starting model scores 91.4% on alive or dead, 91.41% unrounded.
  - Naming by mix reads 43.2%, 49.6%, 58.0%, 72.7%, 86.6%, 90.2% and 90.6%.
  - Alive or dead by mix reads 91.4%, 91.4%, 92.4%, 92.2%, 90.1%, 86.3% and 85.7%.
  - Naming vehicles from words is 92.8% correct at 0.5 and 83.6% at 0.75.
- Uncertainty
  - The alive-or-dead interval at a mix of 0 is 89.5% to 93.2%.
  - The alive-or-dead interval at a mix of 0.5 is 90.5% to 94.0%.
  - The two intervals overlap, so the 0.5 mix shows no loss and no proven gain.
  - The naming value at 0.5 has a 95% interval of 70.28% to 74.89% across species.
  - Intervals come from resampling species 2,000 times and taking the middle 95% of results.
- Not shown
  - The slide does not show why the alive-or-dead score holds until 0.5 and then falls.

**Speaker notes**

This is the earlier alive-or-dead curve with the naming curve drawn on the same axes. Follow them from left to right. Naming climbs at every step: 43.2, 49.6, 58.0, 72.7, 86.6, 90.2, 90.6. Alive-or-dead does not move for the first half: 91.4, 91.4, 92.4, 92.2. Then it goes to 90.1 at a mix of 0.75, 86.3 at 0.9 and 85.7 at the end. So the two changes do not happen over the same mixes. A model halfway between the two has 62% of the naming gain and no alive-or-dead loss. Vehicle naming from words is also intact at this mix, 92.8%, and falls to 83.6% at 0.75. The intervals at 0 and at 0.5 overlap (89.5 to 93.2 against 90.5 to 94.0), so the safe reading at 0.5 is that nothing has been lost yet.

## Slide 19: BioCLIP 2 got worse at telling alive from dead and at naming vehicles from words, which fell from 93.0% to 45.8%

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

## Slide 20: Where in the network does BioCLIP 2 get worse at telling alive from dead?

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

## Slide 21: Every block holds 257 tokens: 256 patch tokens and 1 summary token

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

## Slide 22: Up to block 16, neither model can name 1 species photo in 10 from its summary token

QUESTION 2 · SPECIES NAMING, BLOCK BY BLOCK

14% → 91%

BioCLIP 2’s species naming read from its summary token at block 18 and at block 24. The starting model goes from 5% to 43% over the same blocks.

Up to block 16 neither model names 1 photo in 10 from its summary token.

Horizontal axis: image block, 2 to 24. Each point is read afresh from that block’s summary token, the token that becomes the output. Start is the starting model. These scores come from a separate run of the naming test, so the block-24 values differ from other slides by under a point.

**Method notes**

The slide shows species naming read from each block's summary token in both models.

- What was measured
  - The slide reports species naming accuracy read from the summary token at each block.
  - Each point is read afresh from the summary token at one block.
- Data
  - The naming test uses 3,734 iNaturalist test photos of 223 species.
  - Readings are taken at the even-numbered image blocks from 2 to 24.
- Method
  - Each species is represented by the average vector of five example photos.
  - A test photo is given the species whose average vector is closest in direction.
  - Naming accuracy is averaged over 20 draws, with each species weighted equally.
  - The block-by-block scorer first centres and rescales vectors using example photos only.
  - The second scorer makes the endpoints differ from other slides by under a point.
  - Both models are given the OpenAI pixel scaling.
- Numbers
  - BioCLIP 2's naming from the summary token is 14% at block 18, 14.30% unrounded.
  - BioCLIP 2's naming from the summary token is 91% at block 24, 90.59% unrounded.
  - The starting model's naming is 5% at block 18 and 43% at block 24.
  - The starting model's unrounded figures are 4.99% at block 18 and 43.03% at block 24.
  - At block 22 BioCLIP 2 reads 72% and the starting model 21%, 71.91% and 20.70% unrounded.
  - At block 16 BioCLIP 2 reads 6.20% and the starting model 2.57%.
  - At block 20 BioCLIP 2 reads 30.28% and the starting model 9.42%.
  - Up to block 16 neither model's summary token names 1 photo in 10.
  - The block-by-block scorer gives BioCLIP 2 90.76% and the starting model 44.06% at the output.
- Uncertainty
  - No interval is reported for the block-by-block naming readings.
- Not shown
  - A reading shows what can be recovered at a block, not how the model uses the block.
  - The chart does not show alive-or-dead accuracy, which the next slides cover.
- Definitions
  - Reading a block means taking the tokens held after that block and testing them directly.

**Speaker notes**

Start with naming, because it shows how the method works. Read each block’s summary token and ask how well species can be named from it. Both models sit under 10% until block 16. At block 18 BioCLIP 2 is at 14% and the starting model at 5%; at 22 it is 72% against 21%; at 24, 91% against 43%. So the species skill is built in the last third of the network in both models, and training made the same late blocks do far more of it. If a cost of that training shows up late too, that would fit. The next slide runs the same reading for alive or dead.

## Slide 23: Through block 22, BioCLIP 2’s summary token scores higher than the starting model’s at telling alive from dead

QUESTION 2 · ALIVE OR DEAD, BLOCK BY BLOCK

91.9%

Accuracy at telling alive from dead when a classifier reads BioCLIP 2’s summary token at block 22, against 90.5% for the starting model. BioCLIP 2 is ahead at every block measured, from block 2 to block 22.

If the loss were gradual, BioCLIP 2 would fall further behind at each block. After 22 blocks it is ahead. Its final output scores 85.7%, so all of the fall happens after block 22.

Horizontal axis: image block, then the two final steps, rescaling (norm) and projection (output). Each point: a fresh alive-or-dead classifier trained on that block’s summary token and tested on 1,323 photos of 115 species held out from it.

**Method notes**

The slide shows alive-or-dead accuracy read from each model's summary token up to block 22.

- What was measured
  - The slide reports alive-or-dead accuracy read from the summary token at each block.
  - The chart shows blocks 18 to 22 and leaves blocks 23 onward for the next slide.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
- Method
  - A fresh logistic regression classifier is fitted to the tokens read at each stage.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Scores are balanced accuracy within each species, averaged over the 115 species.
  - Both models receive the same input, with the OpenAI pixel scaling.
- Numbers
  - At block 22 BioCLIP 2's summary token scores 91.9%, 91.85% unrounded.
  - At block 22 the starting model's summary token scores 90.5%, 90.48% unrounded.
  - BioCLIP 2's summary token scores 91.37%, 92.35%, 92.98%, 92.99% and 91.85% at blocks 18 to 22.
  - The starting model's summary token scores 89.08%, 89.26%, 89.14%, 89.23%, 90.48% at 18 to 22.
  - BioCLIP 2 is ahead at every block measured, from block 2 to block 22.
  - At block 2 the summary tokens score 79.15% in BioCLIP 2 and 78.16% in the starting model.
  - BioCLIP 2's final output scores 85.7%, 85.68% unrounded.
- Uncertainty
  - Blocks 2 to 16 were read at even-numbered blocks only.
  - No interval is reported here for the gap between the two models at a single block.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show what happens after block 22.
  - A classifier reading shows what can be recovered, not what the model itself uses.
- Definitions
  - On the axis, norm is the final rescaling step and output is the final projection.

**Speaker notes**

Same method, now for alive or dead, and zoomed in on the last seven blocks. The right-hand side of the chart is empty on purpose. Up to block 22 the model trained on biology is the better of the two at this: 91.4 against 89.1 at block 18, 93.0 against 89.1 at block 20, 91.9 against 90.5 at block 22. In the earlier even-numbered blocks it is ahead as well. So the guess of a gradual loss is wrong. Whatever takes BioCLIP 2 down to 85.7% at the output has not happened yet, with two blocks to go.

## Slide 24: Between blocks 22 and 23, BioCLIP 2’s summary token becomes 4.2 points worse at telling alive from dead

QUESTION 2 · BLOCK 22 TO BLOCK 23

−4.2 points

BioCLIP 2’s summary token at telling alive from dead: 91.85% at block 22, 87.65% at block 23 (95% interval −6.38 to −2.33). That is 4.2 of the 6.2 points lost between block 22 and the output. Another 1.7 is lost at the final projection.

71.9% → 87.3%

Species naming from the same token at the same step. It rose more one block earlier, from 42.5% to 71.9%, while the alive-or-dead score moved from 93.0% to 91.9%.

Horizontal axis: image block 18 to 24, then the two final steps, rescaling (norm) and projection (output). Shaded: the step from block 22 to block 23. Over that step the starting model changes by +0.15 points at telling alive from dead and its species naming rises 15 points.

**Method notes**

The slide shows the drop in BioCLIP 2's alive-or-dead reading between blocks 22 and 23.

- What was measured
  - The top panel reports alive-or-dead accuracy read from the summary token at each stage.
  - The bottom panel reports species naming read from the same summary token.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
  - The naming panel uses 3,734 photos of 223 species, including all 1,323 test photos.
- Method
  - A fresh logistic regression classifier is fitted to the tokens read at each stage.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Scores are balanced accuracy within each species, averaged over the 115 species.
  - Both models receive the same input, with the OpenAI pixel scaling.
  - Naming uses five example photos per species, averaged over 20 draws.
- Numbers
  - BioCLIP 2's summary token scores 91.85% at block 22 and 87.65% at block 23.
  - The change from block 22 to 23 is -4.20 points, shown as -4.2.
  - BioCLIP 2 loses 6.2 points from block 22 to the output, 91.85% to 85.68%.
  - From block 23 to block 24 BioCLIP 2's summary token changes by -0.63 points.
  - From block 24 to the rescaling step BioCLIP 2's summary token changes by +0.35 points.
  - At the final projection BioCLIP 2's summary token changes by -1.69 points, shown as 1.7.
  - BioCLIP 2's summary token scores 87.02% at block 24 and 87.37% after rescaling.
  - BioCLIP 2's naming from the same token rises from 71.9% to 87.3%, 71.91% and 87.26%.
  - One block earlier BioCLIP 2's naming rose from 42.5% to 71.9%, 42.46% and 71.91%.
  - Over that earlier step the alive-or-dead reading moved from 93.0% to 91.9%.
  - The starting model changes by +0.15 points at alive or dead from block 22 to 23.
  - The starting model's naming rises 15 points at block 23, from 20.7% to 35.7%.
- Uncertainty
  - The 95% interval on BioCLIP 2's change from block 22 to 23 is -6.38 to -2.33 points.
  - With C fixed at 1 the same change is -4.92 points, interval -7.23 to -2.78.
  - The starting model's change of +0.15 points has an interval of -1.31 to +1.44.
  - The change from block 23 to 24 has an interval of -2.84 to +1.58 points.
  - The change at the final projection has an interval of -3.37 to -0.04 points.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show why the drop happens at block 23.
  - A rise in naming does not by itself explain the drop, as the earlier step shows.
  - A classifier reading shows what can be recovered, not what the model itself uses.
- Definitions
  - On the axis, norm is the final rescaling step and output is the final projection.

**Speaker notes**

Here is the rest of the chart. Top panel: BioCLIP 2’s line runs above the starting model’s, and then between block 22 and block 23 it drops 4.2 points in a single step and does not recover. The interval on that drop is −6.4 to −2.3, and it is still there with the classifier’s settings held fixed. It is not the whole loss. From block 22 to the output BioCLIP 2 loses 6.2 points: 4.2 here, 0.6 from block 23 to 24, and 1.7 at the final projection, with a small rise at the rescaling step in between. Bottom panel, same token: naming goes from 71.9% to 87.3% at this step. But naming rose more one block earlier, from 42.5% to 71.9%, and alive-or-dead only moved from 93.0% to 91.9% then. So a jump in naming does not by itself bring a drop of this size. The starting model makes a 15-point naming jump at block 23 too, from 20.7% to 35.7%, and its alive-or-dead score does not move.

## Slide 25: BioCLIP 2’s patch tokens still tell alive from dead at block 24: 91.0%, against 87.0% from its summary token

QUESTION 2 · THE PATCH TOKENS

91.0%

Accuracy at telling alive from dead read from the average of BioCLIP 2’s 256 patch tokens at block 24.

After block 23 BioCLIP 2 still holds what is needed to tell alive from dead. The summary token, the one token that becomes the output, carries less of it.

Solid lines: summary token. Dotted lines: average of the 256 patch tokens, one per patch of the photo. The same 1,323 photos and kind of classifier for all four lines. After block 24 come the final rescaling (norm) and projection (output).

**Method notes**

The slide compares alive-or-dead readings from the summary token and from the patch tokens.

- What was measured
  - The slide reports alive-or-dead accuracy read two ways at each stage in both models.
  - One reading uses the summary token and the other the average of the 256 patch tokens.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
  - The same 1,323 photos are used for all four lines.
- Method
  - A fresh logistic regression classifier is fitted to the tokens read at each stage.
  - The 115 test species are split into ten groups, with one classifier per held-out group.
  - Each classifier is fitted without the held-out species and without their photographers.
  - The classifier's penalty setting, C, is tuned on selection photos separate from test photos.
  - Scores are balanced accuracy within each species, averaged over the 115 species.
  - Both models receive the same input, with the OpenAI pixel scaling.
  - The patch reading at a numbered block is a simple average of its 256 patch vectors.
  - At the output, each patch vector is rescaled, then averaged, then projected.
- Numbers
  - BioCLIP 2's patch tokens score 91.0% at block 24, 91.00% unrounded.
  - BioCLIP 2's summary token scores 87.0% at block 24, 87.02% unrounded.
  - BioCLIP 2's patch tokens score 91.57% at block 22 and 91.16% at block 23.
  - BioCLIP 2's summary token scores 91.85% at block 22 and 87.65% at block 23.
  - The starting model's patch tokens score 90.56%, 91.03% and 91.77% at blocks 22 to 24.
  - The starting model's summary token scores 90.48%, 90.63% and 91.36% at blocks 22 to 24.
  - After rescaling BioCLIP 2's patch tokens score 90.88% and after projection 89.83%.
  - After rescaling the starting model's patch tokens score 91.93%, after projection 90.68%.
- Uncertainty
  - At the output the patch reading beats the summary by 4.14 points, interval 1.75 to 6.45.
  - No interval is reported for the gap between the two readings at block 24 itself.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show why the summary token carries less than the patch tokens.
  - A classifier reading shows what can be recovered, not what the model itself uses.

**Speaker notes**

Now use the second way of reading a block. The dotted teal line is the average of BioCLIP 2’s 256 patch tokens. It does not drop at block 23. It reads 91.6 at block 22, 91.2 at 23 and 91.0 at 24, right alongside the starting model. So BioCLIP 2 has not lost the ability to see whether an animal is alive. The patch tokens still hold it. What changed is what the summary token collects from them. From block 23 on that token reports alive-or-dead less well, and the patch tokens beside it do not. In the starting model the two lines stay together all the way to the end.

## Slide 26: On this junco photo, BioCLIP 2’s summary token at block 24 takes 89.6% of its attention from a quarter of the patches

QUESTION 2 · WHICH PATCHES THE SUMMARY TOKEN DRAWS ON

Dark-eyed Junco. Photo (c) jessicaturtle, CC BY-NC, cropped.

Each tile shows how much the summary token draws on each of the 256 patches at that block. Palest is none, copper is most.

The percentage under block 24 is the share of attention on the 64 patches that model attends to most; the starting model’s takes 73.4%. Only 28 of those 64 are the same in both models, and BioCLIP 2 puts 46.6% of its attention on the starting model’s 64.

Both models draw most on the bird’s head and shoulders. On all eight photos checked, BioCLIP 2’s top 64 patches take a larger share than the starting model’s top 64.

Each tile averages the block’s parallel attention steps (heads) and leaves out the attention the summary token pays to itself. All six tiles share one colour scale.

**Method notes**

The slide shows which patches the summary token draws on in the last three blocks.

- What was measured
  - The slide shows the summary token's attention over the 256 patches of one photo.
  - The headline figure is the share of attention on a model's 64 most-attended patches.
- Data
  - The tiles show one iNaturalist photo of a Dark-eyed Junco, licensed CC BY-NC.
  - The attention shares were checked on eight photos.
  - Three of the eight photos are the junco, a robin and a moose used on earlier slides.
  - Five of the eight are photos that only the starting model's classifier labelled correctly.
- Method
  - Each tile averages the summary token's attention weights across the block's heads.
  - Each share counts the 256 patches only and leaves out the summary token's own weight.
  - Both models are given the same OpenAI pixel scaling.
  - All six tiles share one colour scale, from palest for none to copper for most.
  - The 64 most-attended patches are chosen separately for each model at block 24.
  - The 64 patches are a quarter of the 256 and need not lie next to each other.
- Numbers
  - On the junco the starting model puts 73.4% of block-24 attention on its own top 64.
  - On the junco BioCLIP 2 puts 89.6% of block-24 attention on its own top 64 patches.
  - On the junco 28 of the 64 patches are the same in both models.
  - On the junco BioCLIP 2 puts 46.6% of its attention on the starting model's top 64.
  - Robin: starting model 73.9%, BioCLIP 2 85.2%, each on its own top 64.
  - Moose: starting model 67.2%, BioCLIP 2 73.8%, each on its own top 64.
  - Eurasian red squirrel: starting model 70.7%, BioCLIP 2 79.8%, each on its own top 64.
  - Dead robin: starting model 71.4%, BioCLIP 2 91.5%, each on its own top 64.
  - American red squirrel: starting model 73.5%, BioCLIP 2 85.6%, each on its own top 64.
  - Ovenbird: starting model 80.1%, BioCLIP 2 92.8%, each on its own top 64.
  - Brown hare: starting model 60.4%, BioCLIP 2 83.1%, each on its own top 64.
  - On all eight photos BioCLIP 2's top 64 take a larger share than the starting model's.
  - On all eight photos BioCLIP 2 gives the starting model's top 64 a smaller share.
- Uncertainty
  - The own-top-64 shares were computed once from saved head-averaged attention matrices.
  - The own-top-64 shares and the count of 28 shared patches were not independently checked.
  - The 46.6% figure is part of the second study's independently recomputed results.
  - Eight photos are a small sample and were not drawn at random.
- Not shown
  - Attention shares do not show how a patch affects an alive-or-dead prediction.
  - Testing a patch's effect would need a change to the input or model and a new prediction.
  - Traced through all 24 blocks, BioCLIP 2's share was lower on only two of eight photos.
- Definitions
  - A head is one of the parallel attention steps inside a block.
  - Attention is the step where a token draws on other tokens.

**Speaker notes**

If the summary token carries less alive-or-dead, the next thing to look at is what it reads. Attention is the step where a token draws on other tokens, and these tiles show how much the summary token draws on each patch of the junco photo in the last three blocks. For one number per model, take each model’s own 64 most-attended patches at block 24, a quarter of the photo. The starting model draws 73.4% of its image attention from its 64. BioCLIP 2 draws 89.6% from its 64. And they are mostly different patches: 28 are shared, and BioCLIP 2 puts 46.6% of its attention on the starting model’s 64. The same holds on every photo checked. Starting model against BioCLIP 2, each on its own 64: junco 73.4 and 89.6, robin 73.9 and 85.2, moose 67.2 and 73.8, red squirrel 70.7 and 79.8, dead robin 71.4 and 91.5, American red squirrel 73.5 and 85.6, ovenbird 80.1 and 92.8, brown hare 60.4 and 83.1. So at the last block BioCLIP 2’s summary token reads from a narrower and different part of the photo. In the tiles both models have their darkest region on the bird’s head; BioCLIP 2 also has a few strong single patches on the hand and the road.

## Slide 27: 57.7% of block 1’s weight change falls where the starting model’s strongest patterns meet; in block 24, 9.04%

QUESTION 2 · THE WEIGHT CHANGE AS A PICTURE

Each picture is one block’s attention query weights in BioCLIP 2 minus the same weights in the starting model. These weights set what each token looks for. White is no change.

Any table of weights can be split into ranked pairs of an input pattern and an output pattern, called directions. Columns are the starting model’s input patterns, rows its output patterns, strongest first.

The outlined corner, where the strongest patterns meet, is a sixteenth of the picture, so a change spread evenly would put 6.25% there. Block 1’s change puts 57.7% there. Block 24’s puts 9.04% there and shows a faint diagonal: a slightly larger change where an input pattern meets its own output pattern.

Each picture is 256 × 256 cells; a cell averages the size of the change over 4 × 4 of the starting model’s directions. Both pictures share one colour scale. Percentages are shares of the squared change.

**Method notes**

The slide draws the change in attention query weights for block 1 and block 24.

- What was measured
  - Each picture is one block's query weights in BioCLIP 2 minus the starting model's.
  - The percentage is the share of squared change inside the outlined corner.
- Data
  - The pictures use the stored weights of the two models and no photos.
  - Each query weight matrix is 1,024 by 1,024.
- Method
  - The starting model's query matrix is split into ranked input and output patterns.
  - Columns are the starting model's input patterns and rows its output patterns.
  - Patterns are ordered strongest first on both axes.
  - Each picture has 256 by 256 cells.
  - Each cell averages the size of the change over 4 by 4 of the starting model's directions.
  - Both pictures share one colour scale, with white for no change.
  - The outlined corner covers the first 256 directions on each axis.
- Numbers
  - Block 1 puts 57.7% of its squared change in the outlined corner, 57.67% unrounded.
  - Block 24 puts 9.04% of its squared change in the same corner.
  - The corner is a sixteenth of the picture, so an even spread would put 6.25% there.
  - The first 64 directions per axis hold 12.8% of block 1's change and 1.10% of block 24's.
  - For block 1, 141 directions hold 90% of the squared change.
  - For block 24, 506 directions hold 90% of the squared change.
  - A random matrix of the same size and total squared change needs 523 directions.
- Uncertainty
  - The figures are exact properties of the two weight files, with no sampling.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The pictures do not show what effect the weight change has on any test score.
  - The pictures cover the query weights of two of the 24 blocks.
- Definitions
  - Query weights turn a token into the vector used to score attention.
  - A direction is a pair of an input pattern and an output pattern of a weight matrix.
  - Directions are ranked by how strongly the matrix acts along them.

**Speaker notes**

The third way to look is at the weights themselves. Earlier we drew the first-layer filters as pictures. This is the same idea for one matrix inside a block: take BioCLIP 2’s weights, subtract the starting model’s, and draw what is left. The axes are chosen so that structure would be visible. Any weight matrix can be broken into directions, pairs of an input pattern and an output pattern, ranked by how strongly the matrix acts along them. The picture is laid out in the starting model’s own directions, strongest first. In block 1 the change is organised: a dark band over the starting model’s strongest input patterns, darkest at the top left. In block 24 the change is an even wash with a faint diagonal, where each input pattern meets its own output pattern. Counted another way, 141 directions hold 90% of block 1’s change; block 24 needs 506, and a random matrix of the same size needs 523.

## Slide 28: Block 23’s weight change needs 514 directions to hold 90% of it, close to the 523 of a random change

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

## Slide 29: Two-thirds of BioCLIP 2’s fall at telling alive from dead happens at block 23, in its summary token

QUESTION 2 · ANSWER

On all eight photos checked, BioCLIP 2’s summary token at block 24 takes a larger share of its attention from its 64 most-attended patches: 89.6% against 73.4% on the junco photo.

Late in the network, and mostly in one step

The loss does not build up block by block. Through block 22, BioCLIP 2 tells alive from dead better than the starting model at every block measured. Between blocks 22 and 23 its summary token falls 4.2 points, of the 6.2 it loses between block 22 and the output.

Only in the summary token

At block 24 the average of the patch tokens scores 91.0% and the summary token 87.0%. BioCLIP 2 still holds the information. The token that becomes the output carries less of it.

Block 23’s weights changed like any late block’s

Nothing in the weights marks block 23 out. The fall appears only when each block’s tokens are tested.

**Method notes**

The slide answers question 2: most of the fall happens at block 23, in the summary token.

- What was measured
  - The slide gathers the results of question 2 and reports no new measurement.
- Data
  - The block readings use 1,323 photos of 115 species held out from the classifiers.
  - The attention shares were checked on eight photos.
  - The weight comparison uses the stored weights of the two models.
- Numbers
  - BioCLIP 2's summary token falls 4.2 points between blocks 22 and 23, 4.20 unrounded.
  - BioCLIP 2 loses 6.2 points between block 22 and the output, 91.85% to 85.68%.
  - The 4.2 points are about two-thirds of the 6.2 points.
  - The final projection takes another 1.7 points, 1.69 unrounded.
  - At block 24 the patch tokens score 91.0% and the summary token 87.0%.
  - On the junco BioCLIP 2 puts 89.6% of block-24 attention on its 64 most-attended patches.
  - On the junco the starting model puts 73.4% on its own 64 most-attended patches.
  - The weight change in blocks 23 and 24 is spread over 514 and 506 directions.
  - A random change of the same size is spread over 523 directions.
- Uncertainty
  - The 95% interval on the fall at block 23 is -6.38 to -2.33 points.
  - The 89.6% and 73.4% attention shares were computed once and not independently checked.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show why training produced the step at block 23.
  - Naming rose more at block 22 than at block 23 without a comparable drop.
  - The starting model gains naming at block 23 without losing alive-or-dead accuracy.

**Speaker notes**

So the guess was wrong. The loss is not spread across 24 blocks. Two-thirds of it happens at one block, in one of 257 tokens, and the final projection takes another 1.7 points. The patch tokens still score 91%. What we have not shown is why. Naming rises at block 23, but it rose more at block 22 without a comparable drop, and the starting model gains naming at block 23 without losing anything. If the loss were everywhere, the only fix would be to train again. A loss that sits in the last two blocks and in one token leaves other things to try.

## Slide 30: Can one model name species like BioCLIP 2 and tell alive from dead like the starting model?

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

## Slide 31: The starting model with BioCLIP 2’s last 12 blocks copied in names 76.6% of species photos, up from 43%

QUESTION 3 · SWAPPING BLOCKS

43% → 77%

Species naming when the starting model keeps its first 12 image blocks and takes BioCLIP 2’s last 12. No one trained this combination. That is 33 of the 47 points between the two models.

Accuracy at telling alive from dead falls as naming rises. With BioCLIP 2’s last 6 blocks the starting model loses 1.8 points. With the last 18 it scores 84.2%, below BioCLIP 2’s 85.7%.

Horizontal axis: image blocks taken from BioCLIP 2, counted from the output end. 223 species; 1,323 photos of 115 species.

**Method notes**

The slide shows both scores as more of BioCLIP 2's last blocks go into the starting model.

- What was measured
  - The slide reports naming and alive-or-dead accuracy for the starting model with swaps.
  - Each swap replaces the starting model's last 6, 12, 18 or all 24 image blocks.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - Image-model weights are held fixed during scoring.
  - The alive-or-dead classifier is refitted to each hybrid model's output.
  - The five-photo naming references are rebuilt for each hybrid model.
  - Every model in the comparison is given the OpenAI pixel scaling.
  - Blocks are counted from the output end of the image side.
  - The swaps of 6, 12 and 18 blocks keep the starting model's filters and final steps.
  - The last point swaps the whole image side, including patch filters and final projection.
- Numbers
  - Naming reads 43.2%, 53.6%, 76.6%, 86.1% and 90.6% for 0, 6, 12, 18 and 24 blocks.
  - The unrounded naming values are 43.21%, 53.57%, 76.63%, 86.14% and 90.63%.
  - Alive or dead reads 91.4%, 89.6%, 87.7%, 84.2% and 85.7% for the same swaps.
  - The unrounded alive-or-dead values are 91.41%, 89.63%, 87.69%, 84.15% and 85.68%.
  - With BioCLIP 2's last 12 blocks naming rises 33 of the 47 points between the models.
  - With BioCLIP 2's last 6 blocks the starting model loses 1.8 points at alive or dead.
  - With BioCLIP 2's last 18 blocks the score of 84.2% is below BioCLIP 2's 85.7%.
- Uncertainty
  - Naming with the last 12 blocks has a 95% interval of 74.81% to 78.42% across species.
  - With C fixed at 1 alive or dead reads 88.06%, 87.15%, 84.60%, 81.39% and 83.89%.
  - No interval is reported for the alive-or-dead differences between swaps.
- Not shown
  - None of the hybrid models was trained as a whole.
  - The slide does not show which individual blocks carry the change.
- Definitions
  - A hybrid is a model built by copying some blocks from one model into the other.

**Speaker notes**

Start with the plain version of the swap. Take the starting model and replace its last 6, 12 or 18 image blocks with BioCLIP 2’s. You might expect a model stitched together like that to produce nonsense. It does not. Naming goes 43.2, 53.6, 76.6, 86.1, 90.6 as more of BioCLIP 2’s blocks go in. Alive or dead goes 91.4, 89.6, 87.7, 84.2, 85.7. The last point swaps the whole image side including patch filters and final projection. None of these hybrids was trained as a whole, and each one works. With the last 18 blocks swapped, alive-or-dead is 84.2%, lower than BioCLIP 2 itself.

## Slide 32: BioCLIP 2 with the starting model’s last 12 blocks copied in scores 92.9% at telling alive from dead

QUESTION 3 · BIOCLIP 2 WITH STARTING-MODEL BLOCKS

The hybrid, which no one trained: BioCLIP 2’s image blocks 1 to 12 in teal, then the starting model’s blocks 13 to 24 in violet.

It scores 92.9% at telling alive from dead, where the starting model (Start) scores 91.4% and BioCLIP 2 85.7%.

It names 52.3% of species, against the starting model’s 43.2% and BioCLIP 2’s 90.6%. Both scores are closer to those of the model that supplies blocks 13 to 24.

The hybrid keeps BioCLIP 2’s patch filters, text side and the steps after block 24. 223 species; 1,323 photos of 115 species.

**Method notes**

The slide shows BioCLIP 2 with the starting model's last 12 image blocks copied in.

- What was measured
  - The slide reports naming and alive-or-dead accuracy for one hybrid model.
  - The hybrid has BioCLIP 2's image blocks 1 to 12 and the starting model's blocks 13 to 24.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - Image-model weights are held fixed during scoring.
  - The alive-or-dead classifier is refitted to each hybrid model's output.
  - The five-photo naming references are rebuilt for each hybrid model.
  - Every model in the comparison is given the OpenAI pixel scaling.
  - The hybrid keeps BioCLIP 2's patch filters, text side and the steps after block 24.
- Numbers
  - The hybrid scores 92.9% at alive or dead, 92.90% unrounded.
  - The starting model scores 91.4% and BioCLIP 2 85.7%, 91.41% and 85.68% unrounded.
  - The hybrid names 52.3% of species photos, 52.34% unrounded.
  - The starting model names 43.2% and BioCLIP 2 90.6%, 43.21% and 90.63% unrounded.
  - The opposite hybrid, on the previous slide, names 76.6% and scores 87.7%.
  - The hybrid names 88.90% of vehicle photos from example photos.
- Uncertainty
  - The hybrid's naming has a 95% interval of 49.69% to 54.86% across species.
  - With C fixed at 1 the hybrid scores 91.47% at alive or dead.
  - No interval was computed for the gap between the hybrid and the starting model.
  - The hybrid's 92.9% is therefore read as at least as good as 91.4%, not as better.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The hybrid model was not trained as a whole.
  - One pair of hybrids does not show which of blocks 13 to 24 matter most.

**Speaker notes**

Now swap the other way. Keep BioCLIP 2’s first 12 blocks and finish with the starting model’s last 12. Nobody trained this model either. On alive or dead it scores 92.9%, where the starting model scores 91.4% and BioCLIP 2 85.7%. The intervals have not been compared here, so read 92.9% against 91.4% as at least as good. Naming is back down at 52.3%. Put this next to the previous slide: the starting model with BioCLIP 2’s last 12 blocks named 76.6% and scored 87.7% on alive-or-dead. In both hybrids the scores follow whichever model supplies blocks 13 to 24.

## Slide 33: BioCLIP 2 tells alive from dead 4.1 points better with the starting model’s blocks 23 and 24 swapped in

QUESTION 3 · SWAPPING BLOCKS 23 AND 24

Teal cells are BioCLIP 2’s, violet cells the starting model’s. With blocks 23 and 24 replaced, the alive-or-dead score rises to 89.74% (95% interval on the change +1.66 to +6.38) and naming falls 3.21 points. In the last row the starting model loses 1.6 points, less than the 4.2 BioCLIP 2 loses at its own block 23.

Final steps: rescaling and projection. Naming: 223 species. Alive or dead: 1,323 photos of 115 held-out species.

**Method notes**

The slide tests small swaps around blocks 23 and 24 between the two models.

- What was measured
  - The slide reports naming and alive-or-dead accuracy for BioCLIP 2 with small swaps.
  - Each row copies named parts from one model into the other and changes nothing else.
- Data
  - Naming is tested on 3,734 photos of 223 species.
  - Alive or dead is tested on 1,323 photos of 115 species held out from the classifier.
- Method
  - Image-model weights are held fixed during scoring.
  - The alive-or-dead classifier is refitted to each hybrid model's output.
  - The five-photo naming references are rebuilt for each hybrid model.
  - Every model in the comparison is given the OpenAI pixel scaling.
  - The final steps are the rescaling step and the projection after block 24.
- Numbers
  - BioCLIP 2 unchanged names 90.63% and scores 85.68% at alive or dead.
  - With the starting model's blocks 23 and 24, BioCLIP 2 names 87.42% and scores 89.74%.
  - The two-block swap changes naming by -3.21 points and alive or dead by +4.06 points.
  - With the starting model's block 24 only, BioCLIP 2 names 89.45% and scores 88.56%.
  - The block-24 swap changes naming by -1.2 points and alive or dead by +2.9 points.
  - With the starting model's final steps only, BioCLIP 2 names 91.04% and scores 86.03%.
  - With blocks 23, 24 and the final steps swapped, BioCLIP 2 names 87.22% and scores 90.51%.
  - The starting model with BioCLIP 2's blocks 23 and 24 names 40.60% and scores 89.79%.
  - The starting model loses 1.6 points at alive or dead with BioCLIP 2's blocks 23 and 24.
  - The starting model unchanged names 43.21% and scores 91.41% on the same tests.
- Uncertainty
  - The +4.06 point gain has a 95% interval of +1.66 to +6.38 points.
  - The -3.21 point naming change has a 95% interval of -3.89 to -2.57 points.
  - With C fixed at 1 the two-block gain is 3.93 points, interval 1.12 to 6.57.
  - Vehicle naming changes by +0.58 points with the two-block swap, interval -0.82 to +1.88.
  - No interval is reported for the other rows of the table.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The swap does not show why blocks 23 and 24 lower the alive-or-dead reading.
  - The 1.6 points lost in the starting model are fewer than the 4.2 lost inside BioCLIP 2.
  - Blocks 23 and 24 therefore do not carry the whole effect into another model.

**Speaker notes**

Question 2 found that most of the loss happens at block 23. So make the smallest swap that covers it: leave 22 blocks of BioCLIP 2 alone and replace only blocks 23 and 24 with the starting model’s. Alive-or-dead rises from 85.68% to 89.74%. The interval on that gain is +1.66 to +6.38. Naming falls 3.21 points, from 90.63% to 87.42%. Read the other rows as checks. Block 24 alone raises alive-or-dead accuracy by 2.9 points and lowers naming by 1.2. The final steps alone give 91.04% and 86.03%, so they are not where the fix is. Blocks 23 and 24 with the final steps give 87.22% and 90.51%. The last row runs the swap the other way. Put BioCLIP 2’s blocks 23 and 24 into the starting model and it loses 1.6 points of alive-or-dead, and its naming goes from 43.21% to 40.60%. That is less than the 4.2 points those blocks cost inside BioCLIP 2, so the two blocks do not carry the whole effect with them.

## Slide 34: Read from its patch tokens, an unchanged BioCLIP 2 tells alive from dead with 89.6% accuracy, up from 85.7%

QUESTION 3 · READING THE PATCH TOKENS

89.6%

Accuracy at telling alive from dead when a classifier reads the average of BioCLIP 2’s block-24 patch tokens, passed through BioCLIP 2’s own final steps. That is 3.9 points above the summary token (95% interval 1.6 to 6.2).

The summary token still names 90.6% of species photos. One run of an unchanged BioCLIP 2 produces both results.

Final steps: rescaling and projection. Read straight after block 24, before the final steps, the same patch tokens score 91.0%.

**Method notes**

The slide reads alive or dead from BioCLIP 2's patch tokens passed through its final steps.

- What was measured
  - The slide compares two readings of one unchanged BioCLIP 2 at alive or dead.
  - One reading uses the summary token and the other the average of the 256 patch tokens.
- Data
  - The alive-or-dead test uses 1,323 iNaturalist photos of 115 species.
  - Of the 1,323 test photos, 656 are recorded as alive and 667 as dead.
  - The alive-or-dead labels are annotations recorded by iNaturalist contributors.
- Method
  - The block-24 patch tokens are averaged, then rescaled, then projected to 768 numbers.
  - Both routes use the same photos, the same weights and BioCLIP 2's own final steps.
  - The same kind of logistic regression classifier is fitted to each route's 768 numbers.
  - Each classifier is tested on species and photographers held out from its fitting.
  - The classifier's penalty setting, C, is tuned on selection photos.
- Numbers
  - The patch route scores 89.6%, 89.59% unrounded.
  - The summary token scores 85.7%, 85.68% unrounded.
  - The patch route is 3.9 points above the summary token, 3.91 unrounded.
  - Rescaling each patch token before averaging gives 89.8%, 89.83% unrounded.
  - The patch tokens score 91.0% when read straight after block 24, before the final steps.
  - The summary token still names 90.6% of species photos.
  - The starting model's summary token scores 91.4% on the same alive-or-dead test.
- Uncertainty
  - The 3.9 point gain has a 95% interval of 1.6 to 6.2 points, 1.57 to 6.23 unrounded.
  - The patch route's 89.59% has a 95% interval of 87.32% to 91.70% across species.
  - With C fixed at 1 the patch route scores 87.60% and the summary token 83.89%.
  - The two orders of rescaling and averaging differ by -0.23 points, interval -0.86 to +0.41.
  - Intervals pair the two scores per species and resample the 115 species 2,000 times.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show that patch tokens help with properties other than alive or dead.
  - The patch route needs the patch tokens to be kept when the model is run.

**Speaker notes**

The last option changes nothing in the model at all. Question 2 found that the patch tokens still hold alive-or-dead after block 23. Normally they are thrown away. Instead, average them, and send that average through the same final steps the summary token goes through. A classifier on that vector scores 89.6%, against 85.7% from the usual output. The gain is 3.9 points with an interval of 1.6 to 6.2. Doing the rescaling before the averaging gives 89.8%, so the order barely matters. Read directly at block 24, before the final steps, the patch tokens score 91.0%. And since nothing was modified, the summary token is still there for naming at the full 90.6%. For anyone who already runs BioCLIP 2 and cares about a property like alive or dead, this is the cheapest thing on the table: keep the patch tokens and read them.

## Slide 35: Reading the patch tokens makes BioCLIP 2 better at telling alive from dead without lowering its naming

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

## Slide 36: Six measurements placed on the model, from block 1 to where photos meet names

LOOKING BACK · THE WHOLE MODEL

Top row: the image side. Bottom row: the text side. The fewer directions hold a weight change, the more ordered the change is. Telling alive animals from dead ones was tested on 1,323 photos of 115 species that the test’s classifier never saw.

**Method notes**

The slide marks six earlier measurements on a diagram of the whole model.

- What was measured
  - The slide places six earlier results where each was measured in the model.
  - The slide reports no new measurement.
- Data
  - Alive or dead was tested on 1,323 photos of 115 species the classifier never saw.
  - Species naming used five example photos of each of 223 species.
  - Vehicle naming used 1,000 CIFAR-100 photos of ten vehicle classes.
- Numbers
  - In block 1, 141 directions hold 90% of the weight change.
  - In blocks 8 to 24 about 500 directions hold 90% of the change, 481 to 515 by block.
  - A random change of the same size needs 523 directions.
  - At block 23 BioCLIP 2's summary token becomes 4.2 points worse at alive or dead.
  - The patch tokens still score 91% at block 23, 91.16% unrounded.
  - Training changed the word table by 88%, 0.877 unrounded.
  - Species naming is 45.5% in the starting model and 90.6% in BioCLIP 2.
  - Vehicle naming from words is 93.0% in the starting model and 45.8% in BioCLIP 2.
- Uncertainty
  - The 95% interval on the 4.2 point fall at block 23 is -6.38 to -2.33 points.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The diagram does not show a causal link between any weight change and any score.
- Definitions
  - The fewer directions hold a weight change, the more ordered the change is.

**Speaker notes**

This is the anatomy slide from the start, drawn as one picture, and now we can write on it. Follow a photo from the left. It is cut into 256 patches, a summary token is added, and all 257 tokens pass through 24 image blocks. Only the summary token goes on through the final rescaling and projection to become 768 numbers. A name takes the lower route through the word table and the text blocks, and the two lists meet in a cosine score. Now the six marks. In block 1 the weight change is organised: 141 directions hold 90% of it. From block 8 on it looks like a random change. At block 23 the summary token loses 4.2 points on alive or dead in one step, while the patch tokens beside it still score 91%. On the text side the word table changed by 88%. At the image output, species naming goes from 45.5% to 90.6%. And where photos meet names, vehicles named from words fall from 93.0% to 45.8%.

## Slide 37: The word “forgetting” covers three different results in BioCLIP 2

LOOKING BACK · FORGETTING

A model trained further on new data usually gets worse at things it could do before; researchers call this catastrophic forgetting. In BioCLIP 2 the scores fell in three different ways.

93.0% → 45.8%

Named from words, most vehicle photos now get a wrong name

The ten vehicle names became less alike: average similarity fell from 0.774 to 0.662. Every name measured scores higher on every vehicle photo than before. The right name rose least, so “rocket”, “streetcar” or “tank” often scores highest.

91.5% → 86.7%

Named from example photos, the same vehicle photos score 4.8 points lower

Each photo is compared with five example photos of each vehicle, with no words involved. The image side still separates the ten vehicles.

85.7%

89.6%

BioCLIP 2’s patch tokens still tell alive animals from dead ones

The starting model scores 91.4%. BioCLIP 2’s summary token, the one token that becomes the output, scores 85.7%. Its patch tokens score 89.6% passed through the same last steps of the model, and 91.0% read straight after block 24.

In two of the three, the model still held most of what the lower score suggested was lost.

**Method notes**

The slide separates three different results that the word forgetting could cover.

- What was measured
  - The slide sets three earlier results side by side and reports no new measurement.
- Data
  - The vehicle results use 1,000 CIFAR-100 photos of ten vehicle classes.
  - The alive-or-dead results use 1,323 photos of 115 held-out species.
- Numbers
  - Named from words, vehicle photos fall from 93.0% correct to 45.8%.
  - The average similarity between the ten vehicle names fell from 0.774 to 0.662.
  - Each of the four names measured scores higher on every vehicle photo in BioCLIP 2.
  - Named from five example photos, the same vehicles fall from 91.5% to 86.7%.
  - The fall from example photos is 4.8 points, 4.77 unrounded.
  - The starting model scores 91.4% at alive or dead.
  - BioCLIP 2's summary token scores 85.7% at alive or dead.
  - BioCLIP 2's patch tokens score 89.6% passed through the same final steps.
  - BioCLIP 2's patch tokens score 91.0% read straight after block 24.
- Uncertainty
  - The patch-token gain of 3.9 points has a 95% interval of 1.6 to 6.2 points.
  - A separate checker independently recomputed the second study's headline numbers and matched.
- Not shown
  - The slide does not show which side of the model causes the wrong vehicle names.
  - Three results from one pair of models do not describe forgetting in general.
- Definitions
  - Catastrophic forgetting is a model getting worse at earlier skills after further training.

**Speaker notes**

Forgetting is the word everyone reaches for. Train a model further and it usually gets worse at old things; the literature calls that catastrophic forgetting. But look at what we measured, because it is three different things. First, vehicles named from words: 93.0% down to 45.8%. The names did not blur into each other. They became less alike, 0.774 to 0.662, and what goes wrong is that every name scores higher on every photo and rocket, streetcar or tank often comes out on top. Second, the same photos named from five example photos, with no words: 91.5% to 86.7%. Third, alive or dead: the summary token reads 85.7%, but the patch tokens of the same model give 89.6% through the same final steps, and 91.0% read directly at block 24. So in two of the three cases the score fell and most of the knowledge was still there.

## Slide 38: Three methods beat the starting model at naming and BioCLIP 2 at telling alive from dead, with no retraining

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

## Slide 39: Could several specialist models share the same first 12 blocks?

LOOKING AHEAD

What the measurements showed

A hybrid’s two scores follow the model that supplies image blocks 13 to 24. With the starting model’s last 12 blocks, BioCLIP 2 scores 92.9% on telling alive animals from dead ones and names 52.3% of species photos. With BioCLIP 2’s last 12, the starting model scores 87.7% and names 76.6%. Neither combination was trained.

The summary token can name species only in the late blocks. Neither model names 1 photo in 10 from any block up to block 16.

BioCLIP 2’s patch tokens can still tell alive animals from dead ones. They score 91.0% at block 24.

Open questions, not yet measured

1. Could one shared lower half carry several specialist upper halves, for birds, plants or satellite images, with one chosen for each photo?

2. Could training be changed so the summary token keeps the information the patch tokens still carry?

3. Does the summary token’s score also fall at one block in other models trained from CLIP?

4. How specialised can the trained model be before averaging the weights stops giving both skills?

**Method notes**

The slide lists four open questions, none of which has been measured.

- What was measured
  - The slide restates three measured results and poses four questions that are untested.
- Numbers
  - BioCLIP 2 with the starting model's last 12 blocks scores 92.9% at alive or dead.
  - BioCLIP 2 with the starting model's last 12 blocks names 52.3% of species photos.
  - The starting model with BioCLIP 2's last 12 blocks scores 87.7% and names 76.6%.
  - Neither model names 1 photo in 10 from any block up to block 16.
  - BioCLIP 2's patch tokens score 91.0% at alive or dead at block 24.
- Not shown
  - No test was run of several expert upper halves sharing one lower half.
  - No test was run of training that makes the summary token keep the patch information.
  - No other model trained from CLIP was read block by block.
  - No test was run of how specialised a model can be before weight averaging stops working.
  - The birds, plants and satellite images in the diagram are illustrations only.

**Speaker notes**

This is the part I find most exciting, and none of it has been measured. Start from what we did see. When we exchanged the last 12 image blocks between the two models, both scores followed those blocks: BioCLIP 2 with the starting model’s last 12 scored 92.9% on alive or dead and named 52.3% of species, and the starting model with BioCLIP 2’s last 12 named 76.6%. So both hybrids run, the species skill is built late, and BioCLIP 2’s patch tokens still hold alive or dead. Could one lower half serve several upper halves, one for birds, one for plants, one for satellite images, with the right one chosen per photo? Could training tell the summary token to keep what the patch tokens hold? Does the block-23 step appear in other models trained from CLIP? How specialised can the specialist get before averaging stops working? Each is a test someone could run.

## Slide 40: Further training on organism photos raised the share of species photos named correctly from 45.5% to 90.6%.

TO TAKE AWAY

Much of what looked forgotten was still inside BioCLIP 2: it still tells vehicles apart from example photos (86.7%), and its patch tokens still tell alive animals from dead ones (89.6%).

Three methods combined the two skills with no retraining: average the two models’ weights, read BioCLIP 2’s patch tokens, or exchange two blocks.

If you have a general model and a model trained from it, try all three on your own pair, and test a skill the training never targeted.

**Method notes**

The closing slide restates the naming gain, the retained knowledge and the three methods.

- What was measured
  - The slide summarises the explainer and reports no new measurement.
- Numbers
  - Further training raised species naming from 45.5% to 90.6%.
  - Named from example photos, vehicles fell 4.8 points.
  - BioCLIP 2's patch tokens tell alive from dead at 91.0% at block 24.
  - BioCLIP 2's summary token reads 85.7% at the output.
  - The three methods are weight averaging, reading patch tokens and exchanging two blocks.
- Not shown
  - The results come from one pair of models and may not hold for another pair.
- Scope of the measurements
  - The slide lists four limits on what the measurements cover.
  - The slide states the limits of the study and reports no new measurement.
  - Every number comes from one starting model and one model trained from it.
  - Alive or dead was measured on 1,323 photos of 115 species.
  - The skill outside biology was naming ten classes of vehicle.
  - Attention was checked on eight photos.
  - No second pair of models was measured.
  - Skills other than the two tested may behave differently.
  - Classifiers fitted to each block's tokens show what can be read at that block.
  - Block swaps show what changes when blocks are exchanged.
  - Neither the classifiers nor the swaps show why training produced the step at block 23.
  - On all eight photos BioCLIP 2 took more of its attention from a quarter of the patches.
  - The attention concentration figures were computed once and not independently checked.

**Speaker notes**

Three things to take with you. One: training the starting model further on organism photos took species naming from 45.5% to 90.6%. Two: part of what looked forgotten was still there. Named from example photos, vehicles fell only 4.8 points, and its patch tokens tell alive from dead at 89.6% through the same final steps where the summary token reads 85.7%. Three: you can get more of both skills out of the two finished models with no training run: average the weights, read the patch tokens, or exchange blocks 23 and 24. If you have a general model and something trained from it, try all three. Pick a skill the training never aimed at and measure it before and after.

## Slide 41: Photos are from iNaturalist, cropped to 224 × 224 pixels

PHOTO CREDITS

CC BY-NC 4.0

jessicaturtle · Chloé de Mazancourt · Алексей Эбель · Alex Heffernan · Ezri · Isaac Krauss · Andrew Thompson · Gabrielle · errror44 · Andrea Angiari · Susie Prescott · sabsi31 · Bluecross · Дарья Месюсина · katharper · Ramiro Pereira Garbero · lincolnwallerr · gshugart · רעות בן אלישר · Jeff McIntyre · anf-flaxweiler · gaye_white · wyliecath · Dean Fisher · jakob_mair · Jarkko Peltoniemi · Dorota Walkiewicz · Kasey P · cajis · rigbynature · tanjapikaia · zebra1193 · dsunday · albertoaries · jeanhampson · gmurray24 · anschamo · Susanne Vogel · sara_biana · grahamwoodhouse · annabry · worthj · Татьяна Химера · jollytswift · David Bell

CC BY 4.0

Lindsey G. · Andrew Murray · Sophie Hale · Nathan May

CC0, no rights reserved

The American Red Squirrel photo among the photos only one model labels correctly

Each CC BY and CC BY-NC photo is (c) its photographer, some rights reserved. The only change is the crop the models apply to their input.

Licences: creativecommons.org/licenses/by-nc/4.0, creativecommons.org/licenses/by/4.0 and creativecommons.org/publicdomain/zero/1.0.

**Method notes**

The slide credits the iNaturalist photographers and states the photo licences.

- What was measured
  - The slide lists photo credits and reports no measurement.
- Data
  - All photos are from iNaturalist and are cropped to 224 by 224 pixels.
  - The crop that the models apply to their input is the only change to each photo.
  - The slide credits 45 photographers under CC BY-NC 4.0 and 4 under CC BY 4.0.
  - One photo, of an American Red Squirrel, is CC0 with no rights reserved.
  - Each CC BY and CC BY-NC photo remains the copyright of its photographer.
  - Credits cover the one-photo slide, the two similar-photo slides and the attention slide.
  - Credits also cover the sixteen photos on the two slides of disagreements.
  - The junco on the attention slide is the same photo as on the one-photo slide.

**Speaker notes**

Credits cover the one-photo slide, the two nearest-photo slides, the sixteen photos on the two slides of photos only one model labels correctly and the junco on the attention slide, which is the same photo as on the one-photo slide.
