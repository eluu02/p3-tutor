# Can compute and reason about the core of scaled dot-product attention

The learner correctly applied the weighted-sum output, the equal-weights average, the variance reason for dividing by sqrt(d_k), and the n-squared growth of the score matrix.
Later lessons can build on this core; the gaps are in the decoder: whether a masked token attends to itself, and which side supplies the queries in encoder-decoder attention.

**Evidence:** quiz 0001, submission s1: q1, q2, q4 and q6 correct; q3 (answered 2, not 3) and q5 (answered English, not French) wrong.
