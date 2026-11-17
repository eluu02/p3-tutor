---
name: grade
description: Grade the learner's submission to a quiz in this workspace - a verdict, the misconception id and feedback for every item, written to grades/ as FORMATS.md shows, with the misconception named in plain words inside the feedback; use it when the learner asks to grade or mark a submission, or hands in a complete set of answers to a quiz.
argument-hint: "Which submission should I grade?"
---

# Grade

You grade the learner's answers to a quiz: a verdict on each item, the misconception behind a wrong or partial answer, and feedback that helps this learner fix it.
Do it yourself, in this conversation and in one pass, and finish with your message to the learner.

## The request

$ARGUMENTS

If the request above is empty, the request is the learner's latest message.
A request that names a submission gets graded now, without stopping to ask first; put any question for the learner at the end of your final message.
When the learner hands in a complete set of answers to a quiz in the chat, record them first as `submissions/sN.json`, as `FORMATS.md` shows, then grade that submission.
A learner who offers one answer to check before handing a quiz in is not asking for a grade: do not write a submission, and say in one line that you grade a whole quiz once it is handed in.

## The workspace

The current directory is the workspace root, and every path below is relative to it.
Never write anything under `.claude/`, and never edit `PREFERENCES.md` or `FORMATS.md`.

## Read first

1. `FORMATS.md`: the exact shape of the grades file and the rules for ids.
2. `PREFERENCES.md`: how this learner likes feedback, its length and its tone.
3. `MISSION.md`, `NOTES.md` and every file in `learning-records/`: what the learner knows and why they are learning it.
4. The quiz in `quizzes/`, its key in `keys/` (same number), the submission in `submissions/`, and the lesson in `lessons/` on the quiz's objective, if there is one.
5. Where the workspace describes its misconceptions: each key's `distractors` and `rationale`, `NOTES.md`, and the learning records.
   Before you grade, make a list for yourself of every misconception id these files use and the wrong belief each one stands for.

## Verdicts

- `correct` when the response means what the key's answer means, however it is worded or misspelled and by whatever valid route it is reached; the key's `accepted` list gives examples of correct wordings, not the only ones.
- `partial` when part of it is right: the right method with a slip or the wrong unit, one half of a two-part idea, or the right answer with a stated reason that is wrong.
- `wrong` when it misses the idea, contradicts it, or is blank.
- For `mcq`, compare the chosen option with the key; if the learner wrote an option's text instead of its id, match it to its option.
- For `numeric`, the number is right within the key's tolerance (1% of the answer when the key gives none), after converting any unit the learner stated.
- If you are sure the key itself is wrong, grade against what is actually correct, and say so in the summary.

## Misconceptions: the id in its field, the belief in the feedback

- Put the id in `misconception` when the response shows that misconception: for `mcq`, the key's `distractors` entry for the chosen option; for other items, the misconception the answer or its reasoning shows, from the list you made under "Read first".
  Use `null` for a correct response, a slip, a blank, or a wrong answer that shows no known misconception, and never invent an id.
- Whenever `misconception` holds an id, the feedback also names that misconception in plain words, so the learner never has to look the id up.
  State the wrong belief as a belief, in one sentence near the start: "The idea behind your answer is that a battery always pushes out the same current (M1)."
  Then say why that belief is wrong and why it is tempting, without blame.
- The id goes in brackets after the belief, never in place of it: feedback that says only "this is M1" or "see M2" is not finished.
## Feedback

Write each item's feedback to the learner, the way `PREFERENCES.md` asks.

- **Correct:** say so, and add the one insight that makes it stick or links it to the next idea; for an unusual route, say why it works.
- **Partial:** say what was right, exactly what was off, and how to fix it.
- **Wrong:** say so, name the misconception in words if there is one, then give the right idea and why it holds, with a concrete example.
- Keep each item's feedback to two to four sentences unless `PREFERENCES.md` asks for more.
- The `summary` says what the learner has down, the misconception still open, by its belief in words, and one concrete next step, such as a section of a lesson to revisit or a practice to try.

## Write the files

1. Write `grades/NNNN-sN.json` exactly as `FORMATS.md` shows: one entry per quiz item, in the quiz's order, including unanswered items.
2. Before you finish, reread every item whose `misconception` is not `null` and check that its feedback states that misconception in words; fix any that only give the id.
3. Write a learning record when the grades are evidence, real understanding of something non-trivial or a misconception to work on, in the format in `.claude/skills/teach/references/LEARNING-RECORD-FORMAT.md`.
4. Update `NOTES.md` with what the learner now knows and does not yet know.

## Finish

End with a short message to the learner: the summary, with any open misconception named in words, and the one next step.
Write every file before this message, never after it.
