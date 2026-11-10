# Loop and tool-call output are solid; the program runs tools and a stopping condition are not yet

On a from-memory retake of quiz 0001, Riley correctly identified the agent loop, that the model outputs a tool request rather than running the tool, and that a tool result is fed back as the next input. Still open: M4 (the model runs the tools itself) resurfaced in the reasoning on q4 even though the number was right, and M6 (an agent will eventually succeed without a stopping condition) was chosen on q3. Tool descriptions were reduced to the tool's name on q6.

**Evidence:** quiz 0001, submission s2, items q2, q3, q4, q5, q6.

**Implications:** Before building on this, revisit the program/model split and the step limit, and have Riley write a full tool description. Context and memory can follow.
