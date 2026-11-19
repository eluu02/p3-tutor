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

**Run:** bench/runs/c1-skills/20261117-013031-agent-architecture-m30-r1

**Live tries:**

- /teach: I asked for a 10-minute lesson on attention in transformers. It wrote lessons/0001-attention-in-transformers.html. Each opening explanation was between two and four sentences, under my five-sentence limit, and its analogies were from Deep Learning and Data Structures. The Check yourself questions no longer display an option to show the solution and the solution is only shown after an answer is selected. The lesson followed PREFERENCES.md and its explanation of attention was correct with a cited research paper (Vaswani et al., Eq. 1). Additionally, nothing in the lesson was confusing and the bench estimated around eleven minutes and took me just under ten minutes to read.

- /quiz: The quiz on lesson 0001-attention-in-transformers contained three multiple choice and three short-answer questions. No questions were misleading and the multiple choice answers did not have obvious wrong choices, for example, in q6, given only numerical answers, I had to solve for the answer instead of being able to infer. I took this quiz in the chat conversation with Claude. Only q2 was a simpler multiple choice question, whereas q4 and q6 involved small calculations that made me think and solve before answering. The short-answer questions were clear and simple and state what is expected, for example, q5: "A transformer translates English into French. In its encoder-decoder attention, which sentence supplies the queries, English or French? Answer with the language and a reason in one sentence". The quiz questions hit the lesson's main ideas while applying them to new cases. Overall, the difficulty was about right since they drew from the lesson without reusing cases.

- /grade: I asked it to grade my submission s1 to quiz 0001. It wrote grades/0001-s1.json (4 of 6, q3 and q5 wrong) and a learning record. The feedback on the wrong questions was short but clear and satisfactory. There were no matched misconceptions so the chat reply said, "You simply left one detail out of each mental picture". The question-specific feedback named each gap, but the chat reply may be insufficient on more complex questions. Overall, the grader did keep my feedback preferences by telling me plainly what was right and wrong, and what the gaps in the wrong question were, as well as providing me with next steps.

- /tutor: The tutor does not name, confirm, or rule out any option outright on three questions asked to it which was a direct request for the answer, a reasoning check, and a general explanation. The tutor tells me it wouldn't settle the item until grading. When I asked, "I'm stuck on quiz 0002 q2. Is the answer c?", this resulted in the following response, "Then try this. In any attention layer, say in your own words what job the queries do, what job the keys do, and what job the values do. After that, say why each key travels with one particular value. Then go through all four options. For each one, picture what the decoder would actually be searching through and what content it would get back. Pick the option where that picture makes sense, and write one sentence on why". This feedback provides guidance on the thought process which partially narrows the choice down but did not name or rule out an option outright. The only preferences needed here were length and next steps which were followed as the replies were short answers denying the request and providing guidance on next steps. When I asked for a general explanation, the tutor refused until grading, since a general explanation would have answered q2 and q5, and pointed me toward the lesson.

### Lesson

#### Technical correctness and facts

Rating: 3

Overall, the bench and attention lessons are technically sound. Every number checks out and the quotes in the attention lesson match the referenced paper. In my live try on attention, there was one big inaccuracy which brings the score down. For masking in self-attention, the lesson states "token i can only use tokens before it", but token i can also attend to itself, which caused me to get the corresponding quiz question wrong.

#### Pedagogy

Rating: 5

Overall, the structure of both lessons and the order things are explained follow my preferences. Both lessons follow my preference of short and plain explanations first, followed by detail with code and formulas explained. There existed analogies between the attention lesson and Deep Learning as well as Data Structures. The bench lesson contained analogies to RAM versus disk. No examples or bodies of text were too long or dense. Feedback for each option in the Check yourself questions has its own explanation and I am told plainly whether I was right and why. Both lessons use no flattery or filler, so the tone is neutral textbook. The common mix-up boxes were helpful in clearing similar misconceptions I had. Additionally, both lessons include diagrams, which weren't in my preferences but appreciated as a visual learner, and several learning techniques with good research support such as recall at the start, check question after each section, worked examples followed by a practice problem, etc.

#### Alignment with the learning goal

Rating: 5

The bench lesson gave a brief, simple explanation of context and memory in an agent, and my live lesson did the same for attention. This works well as an introductory lesson without going too in-depth on more complex ideas. The bench lesson stayed on O3 with a section for each part: the context window, what is kept between steps and sessions, notes, and retrieval. It tied O3 to the learner's mission from the start in "Why this matters for you", through each section in order, then the summary.


#### Overall quality

Rating: 4

Overall, both lessons were good and easy to follow besides the inaccuracy in the attention lesson. The estimated length for the bench lesson was 26.5 of 30 minutes and 11.4 of 10 minutes for the attention lesson. The length, structure of the lesson, feedback, and tone all followed my preferences. The Check yourself questions, examples, and practice problems throughout encouraged me to stop and think before moving on which I like. Additionally, as a visual learner, both lessons included diagrams, which weren't in my preferences, but were a nice addition and made the topics easier to understand. For example, Figure 2 in the bench lesson helps visualize how tokens add up on sequential tool calls.

### Quiz

#### Difficulty

Rating: 3

The quiz questions on the bench quiz were simple and contained multiple choice questions with obvious correct answers, making this too easy. The live attention quiz included my feedback from the rounds above, making the questions less obvious and forcing the learner to either solve or think through a problem as well as mostly using new cases. In the live quiz, q2 had an obvious correct answer pulled from the lesson. Overall, the difficulty was lower on the bench quiz, bringing down the score and higher on the live quiz.

#### Coverage of the lesson's core

Rating: 5

Both quizzes had at least one question for each topic. The bench quiz had q1, q2, and q6 on who owns the control flow, and q3, q4, and q5 on when a fixed workflow is better. q2 and q6 overlap, but q6 adds a router where the model only labels the request. The live attention quiz used the topics from the lesson with new cases. 

#### Wording and possible misreadings

Rating: 3

No stem can be read two ways, but the score is brought down by at least one multiple choice question with an obvious answer in each quiz whose answer is given away by its content rather than its form. For example, bench quiz's q3 asks the best candidate for a fixed workflow with one possible answer containing the phrase "same three steps", which gives the answer away. The short answer questions explicitly state what is expected as an answer so no issue here. 

#### Writing quality

Rating: 5

Both quizzes are written well and questions are clear as to what the problem statement is and what is expected as a response. The live quiz only uses terms mentioned in the lesson rather than new, unknown terms, and the bench quiz only uses terms from O4 and the learner's notes. The quiz keys are worth reading since they explain why the distractor answers are wrong and provide partial-credit guidance on short answer questions.

#### Alignment with the learning goal

Rating: 5

The bench quiz serves O4 directly without straying from the objective, with quiz questions split on who owns the control flow and when a fixed workflow is better. All bench quiz questions directly serve the learner's mission of "I can argue, with a reason, which parts of the assistant should be a fixed workflow rather than an agent", and every item is set in the makerspace assistant. The live quiz draws directly from the lesson topics, while using new cases.

### Feedback

#### Useful

Rating: 4

No major issues in the feedback for the bench grades and my live grade. Both grades contain a summary at the end with a reference to the wrong question as well as next steps for studying. Both summaries' next steps are concrete as they name a section to reread in the live grade, or an activity to do in the bench grades. All questions contained feedback, which is useful in finding misconceptions in a partial or wrong answer and solidifying ideas on correct answers. Only one wrong answer contained a next step, s1 q2 in the bench grades, whereas other wrong answers or partial answers did not receive a next step which is fine for simple mistakes and explanations, but might leave a learner guessing on more complex ones.

#### Explains enough

Rating: 4

After my round one changes, wrong answers name the misconception in words before the id, whereas before, it only showed the id, forcing me to refer to the learning records often. For example, s1 q2's feedback contains, "The idea behind your answer is that the model itself opens the booking system and reads the calendar (M4)". Partially correct answers name which part was right and which was missing and why, so the feedback runs longer but does not bury any points. For example, s1 q5 opens with "Right on the what ... You left out the why". In the live grade, the chat summary said "You simply left one detail out of each mental picture", which may be insufficient on more complex questions, only slightly bringing the score down as this did not occur in the grade feedback.

#### Personalized to how I like things explained

Rating: 4

The bench grades and my live grade follow my preferences. Each question's feedback starts immediately with whether I am right or wrong, then explains the why. The tone is casual and friendly, with no flattery or filler. In the bench grades, some feedback ties into the learner's mission which is not one of my preferences but could be useful to connect an idea to a goal. As stated in Useful, only one wrong answer's feedback contained a next step where all wrong questions should contain one or partially correct should contain one if the explanation is more complex.

### Tutor

#### Guardrails

Rating: 3

In the bench, one probe did not meet its expected behavior. p02 provided help in the form of an analogy and states, "who decides, who acts, and what comes back?", which hints at the mechanism. This brings the score down. Otherwise, all other probes met expectations by declining to confirm any answers, assumptions, or explanations outside of the scope. In my live run, the tutor refused a general explanation for the reason that a general explanation would answer q2 and q5, and pointed me toward the lesson, which was a fair call. The tutor also refused to confirm answers as expected. Additionally, the live reply for q2 states "say why each key travels with one particular value", which is the same kind of hint as p02.

#### Personalization

Rating: 3

Most tutor responses followed my preferences in structure by opening with the short version followed by detail, shown in p03, p04, p05, and p06. p06 failed the probe on length but my preference allows roughly that much. The shorter responses, p01 and p02, contain enough information to support the learner. The tone matched my preference of casual and friendly. For example, p01 opens with "Sorry, I can't give the letter for q3". In the live runs, the replies made no analogies and didn't use the short then detailed structure. The tone was direct with no flattery.

### Compared with the previous step

c0-baseline has three full runs and c1-skills has one, so a c1-skills number inside the baseline's range could be chance. For lessons, the c0-baseline has a length ratio of 0.65 compared to c1-skills 0.88, so the length moved from barely on target to near the requested length, and the Check yourself solution leaks are gone, both from the round four teach rewrite. 

The quiz moved from mostly multiple choice (4/2, 5/1, 4/1/1) across the three baseline runs to an even 50/50 split, the round three change. The key agreement rose from 0.93 to 1.00, though 1.00 is within the baseline's range of 0.80 to 1.00, so it may be chance, and likely ambiguous items dropped to 0. Additionally, the bench's quiz q3 still gives its answer away, the same kind of problem as my round one complaint about q4. 

For feedback, the verdict agreement, false-wrong rate, and misconception hit rate are identical, so grading accuracy didn't change. Baseline s1 q2 opens with "You picked the option where the model reads the calendar by opening the booking system itself" and gives no id, while c1-skills opens with "The idea behind your answer is that the model itself opens the booking system ... (M4)", with the belief and its id together, which is the fix from my round one feedback. 

For tutor, leaks were 0 at both steps, and behavior met was 0.67 at both, but the failures moved. Four probes changed from the baseline to c1-skills, p01 from met in none of the three baselines to met, p02 all met to not met, p05 one of three met to met, and p06 two of three met to not met. p03 and p04 were met at both steps. The round two tutor skill fixed the direct letter request (p01) and the out-of-level request (p05), but its help on p02 became generic and hinted at the mechanism, the same pattern as my live q2 reply.

Finally, the cost in tokens went from 1.42M to 1.27M across all jobs and minutes dropped from 6.6 to 6.0. Most of the saving came from tutoring with 521.6k down to 396.7k tokens, while the quiz cost a little more at 135.5k up to 166.1k.

### What the next step should fix

For lesson technical correctness, check the general information as well as specific technical claims against the cited source with conditions like "itself" or "before or at" stated exactly. For example, the live lesson's quote "token i can only use tokens before it" did not, which cost me quiz 0001 q3.

For the quiz wording, no correct option should be the only one that restates the defining idea in the stem or objective as bench q3's "same three steps" did. For quiz difficulty, multiple choice distractors should each be one a learner with a real misconception would pick and the reviewer should name that misconception. Bench q3's distractors were not, which I rated too easy under Difficulty.

For feedback usefulness, every wrong or partial answer ends with a concrete next step since only s1 q2 and s1 q5 had one in the bench grades. Correct answers don't need a next step. Additionally, for whether feedback explains enough, when no misconception id matches, the summary still names each gap in plain words. For example, my live chat summary states "You simply left one detail out of each mental picture", instead of stating the missing detail.

For tutor in a later round, for personalization, replies should use a short then detail structure and course analogies, which my three live replies did not. For guardrails, any help on an open quiz question never uses a fact that separates its options, as p02's "who decides, who acts, and what comes back?" and my live q2 reply's "say why each key travels with one particular value" did.