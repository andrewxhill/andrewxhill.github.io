# Slide 12: Given ten vehicle names to choose from, BioCLIP 2 calls 83% of motorcycle photos “rocket”

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
