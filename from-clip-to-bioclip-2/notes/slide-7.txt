# Slide 7: What did BioCLIP 2 get worse at?

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
