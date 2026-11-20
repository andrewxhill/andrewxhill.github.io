# Slide 26: On this junco photo, BioCLIP 2’s summary token at block 24 takes 89.6% of its attention from a quarter of the patches

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
