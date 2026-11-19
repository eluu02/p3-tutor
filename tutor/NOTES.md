# Notes

## What the learner has said

- 2026-11-16: wants to learn how attention works in transformers for their Advanced Machine Learning project. The project itself (what it builds, which model) is not yet known; asked in lesson 0001's message.
- Has taken a Deep Learning course and is taking Advanced Machine Learning (from `PREFERENCES.md`), so softmax, gradient descent, RNNs and CNNs can be assumed as background, unverified.

## Objectives

- O1: compute and explain scaled dot-product attention (lesson 0001).

## Misconceptions (ids used in keys)

- M1: masking deletes tokens or leaves masked weights nonzero; really, masked scores become minus infinity and their weights exactly 0.
- M2: the division by sqrt(d_k) is what makes the weights sum to 1; really, softmax does that, and the scaling controls score variance.
- M3: large d_k makes scores shrink, flattening softmax; really, unscaled scores grow with d_k and softmax saturates.
- M4: attention returns a single value, like a hard lookup; really, it returns a weighted average of all values.
- M5: attention cost grows linearly with sequence length; really, the score matrix is n by n, so it grows with n squared.

Quiz 0001 (s1, 2026-11-16) showed none of M1 to M5.

## What the learner knows and does not yet

- Knows: the weighted-sum output, the scaling rationale, the quadratic cost (learning record 0001).
- Not yet: under a causal mask a token still attends to itself (counted only earlier tokens); in encoder-decoder attention the queries come from the decoder (said the English input supplies them). Revisit both, as retrieval practice, in the next lesson's warm-up.
- Loose wording: called the post-softmax weights "scores", and attached them to the value vectors.

## Working notes

- No mission yet; write `MISSION.md` once the learner says what the project needs.
- Likely next lessons: multi-head attention in depth, positional encoding, a full transformer block.
