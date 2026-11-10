# Misconception to work on: models do not remember earlier conversations on their own

Riley assumed a language model automatically remembers what each student said last week. In fact the model only sees the text sent to it in the current request, so any cross-session memory has to be built by the assistant: save facts, then load the relevant ones into the next prompt.
This matters directly for the makerspace assistant's per-student training status.

**Evidence:** chat question in the session after quiz 0001; the correction was given, and the understanding has not yet been shown back.
**Implications:** The next lesson on context and memory should start here. Check by asking Riley to sketch what is saved, where, and what gets loaded at the start of a visit.
