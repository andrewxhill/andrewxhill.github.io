# Slide 10: Eight photos the starting model labels correctly as alive or dead and BioCLIP 2 labels wrongly

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
