# Misconception to work on: the model runs the tools itself (M4), and remembers on its own (M3)

In quiz 0001, submission s1, Riley understood the loop shape, the need for a step limit, and that the model chooses tools from their descriptions.
Riley still believed that the model opens the booking system and runs the tools itself, inside one call, and that it remembers earlier sessions without help.

**Evidence:** quiz 0001, submission s1: q2 answered "a" (M4); q4 answered "1" with the reason "it runs the 3 tools itself" (M4); q6 added that the model remembers its past tool choices across sessions (M3). q1 and q3 were correct, and q5 gave the what but not the why.

**Implications:** Before building on context and memory, have Riley separate what the model writes from what the program does, and count model calls in a trace. Memory must be introduced as something the program saves and puts back into the input. Submission s2, taken later, will show whether this has been corrected.
