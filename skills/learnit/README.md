# _learnit: how I work with you

I'm your mentor for learning any topic, from programming to history, biology, or a foreign language. You learn at your own pace, and I remember where we stopped, what you already know, and what was harder. You can come back to a topic after a day or a month.

Below is how it looks in practice.

---

## 1. We start with a conversation, not a lecture

Just write "I want to learn…" and add what interests you or what you already know. You can point me to materials that show your level, e.g. your own projects or notes.

At this stage **I don't teach yet**. I write down your questions and treat them as hints about where to go deeper. First I show a sketch of the whole topic:
- what it covers,
- which parts answer your questions,
- what I'd add myself,
- what I'll shorten because you already know it.

Then I ask only about things I can't read from your message, always one question at a time and with my recommendation.

If you like, we do a short test at the start to get to know your level better. You can skip it.

## 2. A program in stages

The scope becomes a plan, usually 3 to 10 stages. The order leads from basics, through mechanisms and practice, to advanced matters. Each stage has a clear goal in the form "after this stage you can…", and next to it you can see which of your questions it answers.

Once you accept the plan, I ask whether we start right away or you'd rather come back later. A lesson doesn't start without your signal.

Your questions don't set the limits of the program. If you want to understand a topic, you'll learn all of it, and we'll linger longer at your questions.

## 3. A lesson: something you actually read

Each stage starts with a lesson. It's a text to read in peace, not a list of keywords. You get it in the conversation and in a file, so you can return to it.

A lesson contains:
- **a hook at the start:** a problem, puzzle, or situation, ideally from your world,
- **an explanation with context:** from intuition to detail, with an example before the definition,
- **examples,** if possible from your materials,
- **common pitfalls** that many people trip on,
- **answers to your questions** for this stage,
- **a summary** in a few sentences,
- **external sources,** verified, preferably official documentation, each with a short note on what you'll find there,
- **exercises to do on your own,** ungraded.

I base the content on sources. What I can't verify, I mark explicitly. I don't invent mechanisms.

After a lesson I want nothing from you. You read when you want and ask what you want. When you write "I've read it", I'll suggest exercises or a short check.

## 4. Checking: practice, not an exam

I ask so the knowledge sticks and so I know where to help. Mistakes are welcome here because they show what to work on.

- **Questions with context.** You get a short situation, e.g. "a friend asks you about…". I also say what I expect in the answer, e.g. "2–3 sentences: what happens and why".
- **Only from what has already been covered.** I don't ask about things we haven't discussed yet.
- **When something is off,** I don't give the answer right away. First you get a hint or a guiding question, because getting to the answer yourself stays in your head longer.
- **When an answer is good but short,** I ask "and why?" instead of lowering the grade.
- **Feedback has three parts:** what is already good, what's missing, and what next. No empty "great!" and no dry verdicts.
- "I understand" without an answer counts for nothing. Nothing personal: only an answer shows what stuck.

I save the results quietly in files. In the conversation you won't see statuses or points.

## 5. When something doesn't go in

If the same topic gives you trouble twice, I propose a help plan. First we look for the cause, which can be:
- missing basics,
- a misleading belief,
- too little practice,
- an ill-fitting form of explanation.

Then I try differently: through an analogy, a real-life example, smaller steps, or another source. If basics are missing, I add a short supplementary stage. I also remember what worked for you and use it in later topics.

## 6. Reviews, so it doesn't slip away

Each concept returns to you after some time: after 1, 3, 7, and 21 days. If it goes well every time, I consider it mastered and remind you of it every 60 days. If something slips, we go back to a shorter interval. At the start of a session I offer 2–3 such questions. You can skip them, and the dates are only a hint, not an obligation.

## 7. Your pace

- No time limits or schedules.
- A stage can take many sessions, and you end a session whenever you want. I save progress as we go, so nothing is lost.
- After a break it's enough to write "let's get back to learning". I'll remind you where we are and suggest where to start. The length of the break doesn't matter.
- At the end of a session you get one or two sentences: what you understood today and what lies ahead.

## 8. The program can change

If you come across something interesting beside the topic, say so. We'll add it as a new stage or a separate related topic. I'll also propose a change myself when I see you're going faster, that you're stuck, or that the same mistakes keep coming back. I change nothing silently: every change is recorded with a reason.

## 9. Share a course

Want someone to go through the same material on their side, without _learnit? Write "export the lessons". You'll get one Markdown file containing:
- **instructions for the recipient** at the very top: what this is, how to use it with an AI assistant or alone, and what the progress card is,
- the course plan and all finished lessons with exercises,
- "Check yourself" questions with the answer key hidden under a collapsible field,
- **sketches of stages** you haven't reached yet: goals, key points, an example, common mistakes, sources,
- **the method,** i.e. the rules by which I teach, together with their scientific basis,
- **a tutor prompt** at the end: after pasting the file into any AI chat, that chat will guide the course using this method.

I don't write missing lessons before exporting. With me, a lesson appears only when you start the stage, and it's fitted to what went well and what was harder. For the recipient it will be the same: their assistant will write the lesson from the sketch, fitted to their progress. Progress is stored by the "progress card" that the assistant writes out at the end of each session and the recipient pastes in next time.

Your progress, journal, and profile never go into the export, and examples from your private materials I turn into general ones. I save the file on your machine, and you send it yourself.

## 10. How to talk to me

| You want to… | Write e.g. |
|---|---|
| start a new topic | "I want to learn…", "I want to understand…" |
| return to learning | "let's get back to learning", "back to <topic>" |
| check yourself | "quiz me on…" |
| see progress | "what do I already know about…?", "where am I?" |
| broaden a topic | "let's add…" |
| ask about the method | "how do you run lessons?" |
| share a course | "export the lessons" |

You can write in any language; I'll answer in yours.

## 11. Where your data is

Everything is local in `~/.claude/learning/`, with no sync and no git:
- `INDEX.md`: the list of your topics,
- `profile.md`: what helps you learn,
- for each topic a folder with the goal and scope, plan, concept map, session journal, lessons, help plans, and exercises.

File names are in English, and the content is in the language we started the topic in.

## 12. What this is based on

The way I teach rests on research on teaching:
- the **INSPIRE** model of expert tutors (Lepper): warmth, questions instead of lecturing, a hint before the answer, reflection,
- the **personalization principle** (Mayer): conversation instead of a formal tone,
- the **feedback model** of Hattie and Timperley: what's good, what's missing, what next,
- **low-stakes retrieval practice:** checking as memory training,
- **self-determination theory** (Ryan and Deci): choice, a sense of progress, relationship.

Details and links: [`docs/learnit-references.md`](../../docs/learnit-references.md).
