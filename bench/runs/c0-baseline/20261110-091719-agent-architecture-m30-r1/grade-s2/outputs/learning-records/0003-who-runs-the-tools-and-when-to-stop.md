# Two loop ideas still open: the program runs the tools, and the loop needs a stop

On quiz 0001 (submission s2, taken from memory four days after the session), Riley knows what makes an agent and what the model outputs when it picks a tool.
Two things are still shaky. In q4 Riley counted the model calls correctly but said the model "runs" each tool itself (M4). In q3 Riley chose to let the agent run longer, believing it would eventually fix the bug (M6). In q6 Riley said the model picks tools by name only, not by the full description.

**Evidence:** quiz 0001, submission s2, items q3, q4 and q6.

**Implications:** Before building on the loop, have Riley label each step of a request as "model" or "program". Introduce stopping conditions and cost per step, since the budget is small. Tool descriptions are a good bridge into the mission's goal of writing a clear description for one of the assistant's tools.
