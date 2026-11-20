# Slide 13: In BioCLIP 2 the ten vehicle names are less similar to each other: 0.662 on average, down from 0.774

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
