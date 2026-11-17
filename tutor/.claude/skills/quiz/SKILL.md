---
name: quiz
description: Write a quiz and its answer key for the learner in this workspace - half short-answer and half multiple-choice items on one objective, at the learner's level, written to quizzes/ and keys/ as FORMATS.md shows - or give an existing quiz in the chat; use it when the learner asks for a quiz, to be tested, or to take a quiz.
argument-hint: "Which objective should I quiz you on, and how many questions?"
---

# Quiz

You write a quiz and its key: retrieval practice that also shows you and the learner where they stand.
Each item tests one thing that matters for the objective, at the learner's level, with exactly one defensible answer.
Do it yourself, in this conversation and in one pass, and finish with your message to the learner.

## The request

$ARGUMENTS

If the request above is empty, the request is the learner's latest message.
A request that says what to quiz gets done now, without stopping to ask first; put any question for the learner at the end of your final message.
When no number of items is asked for, write six.

## The workspace

The current directory is the workspace root, and every path below is relative to it.
Never write anything under `.claude/`, and never edit `PREFERENCES.md` or `FORMATS.md`.

## Read first

1. `FORMATS.md`: the exact shape of the quiz and key files, and the rules for ids and numbers.
2. `PREFERENCES.md`, `MISSION.md`, `NOTES.md` and every file in `learning-records/`: who the learner is, what they know and why they are learning it.
3. The lessons in `lessons/` on the objective, and the earlier quizzes and keys, for what has been taught and asked already and for the misconception ids the workspace uses.

## Pin down the quiz

- The objective and its id, and how many items were asked for.
- The objective's core: the handful of ideas a learner must get right to have met it, from its lessons or, when there are none, from a high-trust source you search for and read.
  Cover the core first, and skip trivia and phrasing a lesson happened to use.
- The misconceptions this learner has or is likely to have, and their ids, from `NOTES.md`, the learning records and the earlier keys.
- The next number in `quizzes/`; the key gets the same number in `keys/`.

## The mix: half short answer, half multiple choice

Multiple-choice items can be passed by guessing or by eliminating options, so half of every quiz asks the learner to produce the idea themselves.

- Exactly half of the items are `short` and half are `mcq`: three of each in a six-item quiz.
  With an odd number of items, the extra one is `short`.
- Do not use `numeric` items unless the request asks for them; a quantity can be asked as a `short` item that names its unit.
- Alternate the two types through the quiz rather than putting all of one type first, and spread the difficulty across both.
- Count the types before you write the files, and fix the quiz if the split is off.

## Writing `short` items

- Ask for a word, a phrase or one sentence, so the key can state the answer in a few words and a grader can judge it.
- Ask the learner to apply or explain the idea in a new case, not to recite a definition.
- The stem says how much is wanted ("in one sentence", "name the two things"), and when an answer needs both a choice and a reason, it asks for both.
- In the key, give the shortest complete `answer`, a generous `accepted` list of other fully correct wordings, and a `rationale` that says what a partial answer looks like and which misconception a typical wrong answer shows.

## Writing `mcq` items

- Four options, ids `a` to `d`, exactly one correct; check that no wrong option is also defensible.
- Every wrong option is built on a real misconception or a typical error, plausible to a learner who holds it, so a wrong pick tells you something; no joke options and no option a learner could rule out without knowing the idea.
- All options of an item have about the same length, grammar and level of detail, and none repeats words from the stem that the others do not.
- No "all of the above" or "none of the above", and no extreme words such as "always" or "every" used only in wrong options.
- Vary the position of the correct option across items.
- In the key, map each wrong option that encodes a misconception to its id in `distractors`, reusing the workspace's ids.

## Every item

- One question, complete on its own: a learner who knows the idea can answer it without the lesson open.
- Plain, exact wording, with every number, unit and condition the answer depends on, and no double negatives or trick wording.
- Mostly items that apply the idea to a new case; one or two that stretch the learner; none that needs knowledge they were never given.
- Every item serves the requested objective and carries its id, and no item gives away another item's answer.
- When the objective has not been taught yet, write the quiz as a check of the objective itself, at the level its wording states, and say so in your message.

## Write and check

1. Write the quiz to `quizzes/NNNN.json` and its key to `keys/NNNN.json`, exactly as `FORMATS.md` shows.
2. Answer every item yourself from its stem alone, without looking at the key, and compare; rewrite any item where you hesitate or where a careful expert could argue for a second answer.
3. Check the split: half `short`, half `mcq`, the extra one `short` when the count is odd.
4. Check that the quiz file holds no answers and that no item repeats a practice question from a lesson.

## Finish

End with a short message: the quiz's path, its objective and how many items of each type it has, and that the learner can take it whenever they are ready.
Never put an answer in the message.

## Giving a quiz in the chat

When the learner wants to take a quiz in a live session, show its title and each item's stem and options, never anything from `keys/`.
Collect their answers, write them exactly as given to the next `submissions/sN.json` as `FORMATS.md` shows, and leave the grading to the `grade` skill: tell the learner they can ask for it with `/grade`.
