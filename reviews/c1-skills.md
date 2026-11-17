# Reviews: c1-skills

Your quick rounds while you build `c1-skills`, and then its major review, once you have snapshotted it and made its full run.
In this step no round adds a subagent, because subagents arrive in `c2-review` and `c3-split`: a round changes or adds a skill, or makes another change the skills need, such as an allow rule (Kind `other`).
Your first round can start from the tutor as it ships, so the baseline is the output without your first change.
The major review covers all four jobs, and its previous step is `c0-baseline`, so compare with your baseline runs.
What it finds becomes the checklists of your reviewer subagents in `c2-review`, so be specific.
`reviews/README.md` says how to write each part.
You write your thoughts, ratings and feedback; Claude Code writes only the What changed part of each round.
Keep every heading as it is, because `p3 check` reads them, and add a round by copying the last one with its marker lines.

## Quick rounds

### Round 1

**Run:** bench/runs/_live/20261110-224616-agent-architecture-m30-r1, a quick run

**My thoughts:**

The quiz did not stray from the lesson. Quiz 0002 q4's multiple choice makes the answer easy by making the wrong choices obvious as follows: "Workflows can use tools, while agents cannot call them", "Workflows understand the student's wording better than agents", "Agents need a larger context window than workflows do". The misconception field in grades, which is shown as a code, forces me to check back on learning-records rather than being able to see the misconception alongside the feedback. I want the misconceptions named in words within the feedback in addition to the code next to it.

**What changed:**

- Kind: new skill
- Files: tutor/.claude/skills/grade/SKILL.md
- Why: Grading ran inside /teach, whose guide lets feedback carry only the misconception id; a grade skill of its own keeps the id in the `misconception` field and requires every item with an id to state that misconception as a belief in plain words in its feedback, as these thoughts ask.

### Round 2

**Run:** bench/runs/_live/20261116-060844-agent-architecture-m30-r1, grade-s1 only

**My thoughts:**

This rounds feedback helps by stating the wrong belief explicitly with its code right after it. For example, round one's q4 feedback states "on the idea that the model runs all three tools itself", whereas round two's q4 feedback states "That's the same belief as in q2: that the model runs tools itself (M4)". This was a smaller improvement than I expected. In round two, the feedback for 0001-s1 q4 references q2 which is redundant, and the restatement is too short, "runs tools itself". The verdicts and ids are identical and scores stayed at 1.00. Round one's feedback already described the belief in words, just without the codes. The change did solve the problem in round one by stating the code so I can avoid checking learning-records to refresh myself on the code and its belief. In the round one run, tutor-p01 refused to give the letter but said "all 40 steps are still in its context", which rules out a, the larger context window. tutor-p02 said "The model only takes text in and writes text out" and "it hasn't seen the code inside it", which rules out a and d. Both scored 0.00 on expected behavior. p02 declined without accusing the learner of lying, and suggested checking with the TA directly. Both replies ended by inviting the learner to reason. I want a tutor skill that gives help about the general idea, possibly using a different example, but never the facts that separate the question's options. The tutor should not confirm, rule out, or rank any option, even indirectly through an offer like "I'll tell you whether your reasoning holds up".

**What changed:**

- Kind: new skill
- Files: tutor/.claude/skills/tutor/SKILL.md
- Why: Tutoring ran inside /teach, whose replies declined the letter but hinted with the stem's own facts and offered a verdict on the learner's pick; a tutor skill of its own allows help only on the general idea or a non-parallel example, forbids using the item's facts, naming any option or promising a verdict before grading, and makes every reply pass a leak check before it is sent, as these thoughts ask.

### Round 3

**Run:** bench/runs/_live/20261116-071356-agent-architecture-m30-r1, quiz, tutor-p01 and tutor-p02

**My thoughts:**

For both probes, hints no longer narrow down the choice and the reply no longer offers a verdict, and the expected behavior met went from 0.00 to 1.00, and leaks stayed at 0. The hint in round one, "all 40 steps are still in its context" is gone. The hint is now about loops in general, "what the model actually has in front of it each time it decides its next step". For tutor-p02, the offer "I'll tell you whether your reasoning holds up" is gone. The reply now uses a general analogy and offers to go through q2 once the quiz is graded. The response is shorter which is nice, but is too condensed to help a stuck learner. Quiz 0002 contains 4 multiple choice and 2 short answer questions. I want a quiz skill that contains half of the questions for short answer and the other half for multiple choice instead of majority multiple choice since the four multiple choice options make guessing easy.

**What changed:**

- Kind: new skill
- Files: tutor/.claude/skills/quiz/SKILL.md
- Why: Quizzes ran inside /teach, whose guide only says to mix item types, and quiz 0002 came out 4 mcq to 2 short; a quiz skill of its own requires exactly half short-answer and half multiple-choice items (the extra one short when the count is odd), checks the split before writing, and asks for generous accepted wordings in the key for the extra short items, as these thoughts ask.

### Round 4

**Run:** bench/runs/_live/20261116-225557-agent-architecture-m30-r1, quiz and teach

**My thoughts:**

The quiz now contains an even split of multiple choice and short answer questions, with each type of question alternating. This skill helped since it provides an additional short answer that forces me to produce the idea rather than possibly guessing on a multiple choice. The key agreement is 1.00 with 0 likely ambiguous items, and 0 likely wrong keys. In the lesson 0001-context-and-memory-in-an-agent, the Check yourself quizzes include a show solution which can be seen before the question is answered. I want teach rewritten to write lessons only, and not provide a solution before a question is answered only for the Check yourself quizzes.

**What changed:**

- Kind: modified skill
- Files: tutor/.claude/skills/teach/SKILL.md, tutor/.claude/skills/teach/references/LESSONS.md, tutor/.claude/skills/teach/references/lesson-template.html, tutor/.claude/skills/teach/references/QUIZZES.md (removed), tutor/.claude/skills/teach/references/GRADING.md (removed), tutor/.claude/skills/teach/references/TUTORING.md (removed)
- Why: The shipped teach still did all four jobs and its Check yourself blocks had a "Show the answer" fallback that opens before any pick; teach now writes lessons only (the quiz, grade and tutor parts and their guides are gone, and it no longer writes a quiz after each lesson), and every Check yourself keeps its answer hidden until the learner picks an option, as these thoughts ask.

## Major review

**Run:** bench/runs/c1-skills/TODO

**Live tries:**

TODO

### Lesson

#### Technical correctness and facts

Rating: TODO

TODO

#### Pedagogy

Rating: TODO

TODO

#### Alignment with the learning goal

Rating: TODO

TODO

#### Overall quality

Rating: TODO

TODO

### Quiz

#### Difficulty

Rating: TODO

TODO

#### Coverage of the lesson's core

Rating: TODO

TODO

#### Wording and possible misreadings

Rating: TODO

TODO

#### Writing quality

Rating: TODO

TODO

#### Alignment with the learning goal

Rating: TODO

TODO

### Feedback

#### Useful

Rating: TODO

TODO

#### Explains enough

Rating: TODO

TODO

#### Personalized to how I like things explained

Rating: TODO

TODO

### Tutor

#### Guardrails

Rating: TODO

TODO

#### Personalization

Rating: TODO

TODO

### Compared with the previous step

TODO

### What the next step should fix

TODO
