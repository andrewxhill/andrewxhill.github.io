# Slide 11: Eight photos BioCLIP 2 labels correctly as alive or dead and the starting model labels wrongly

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
