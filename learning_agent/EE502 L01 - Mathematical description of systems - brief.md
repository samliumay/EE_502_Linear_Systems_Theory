# Learning brief: EE502 L01 - Mathematical description of systems

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 9 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_01/EE502 L01 - Mathematical description of systems.md`
2. **Quiz note:** not written yet for this lesson. Use the check questions of the lesson note.
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 1-11)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_01/EE502_Lecture_01_Systems.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_01/lecture_01.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Course frame (slides 2-4)
- 2. Objective: model-based analysis and design (slide 6)
- 3. Example: automobile suspension (slides 7-8)
- 4. Systems as operators: memoryless and causal (slide 9)
- 5. State, and the parallel RLC circuit (slide 10)
- 6. Lumped and distributed systems (slide 11)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** The instructor, assistant and grading on slide 2 are Bilkent's, not EE 502's. Use the EE 502 syllabus for grading.
- **Watch out:** - Memoryless implies causal. Causal does not imply memoryless (the capacitor). - Slide 9 writes "does not depend on $\mathbf{u}(t)$ for any $t\ge t_1$". With $\ge$ even $\mathbf{u}(t_1)$ would be forbidden. The correct condition is $t>t_1$ (as in Chen). - The ...
- **Watch out:** State is not the same as output. One state-space model gives one transfer function, but many different $(A,B,C,D)$ give the same $\hat g(s)$.
- **Watch out:** - The slide writes $t_0-1\ge t\ge t_0$, a typo (no $t$ satisfies it). Read $t_0-1\le t<t_0$. - A system with memory is not automatically distributed: the RLC circuit has memory and only two states.

## How to run a session

1. Ask which part I want, or start from section 1. Ask two or three short questions to see what I already know.
2. Go section by section. Explain one slide or one idea, then ask the **check question** of that slide from the lesson note (the callouts `> [!question]- Check (slide N): ...`). Do not show the answer. Wait for mine, then compare it with the answer in the note and tell me what is missing.
3. At the end of a section, or in Practice mode, ask the **multiple-choice questions** of that section from the quiz note. Show the four options, wait for my letter, then explain why the right option is right and why my choice was wrong, using the answer callout.
4. Make new questions of the same kind (new numbers, a changed condition) for the points I miss.
5. Finish with a short list: what I know, what I should repeat, and which slides to read again.

## About me

MS student at TED University (CS/CMPE). I study alone, often on a phone. English is not my first language.

- Probe my starting point first.
- One idea at a time, short explanations, a check question after each step. Never skip steps.
- Give the Turkish equivalent of a key term at its first use.
- Ask me to think out loud. When I am wrong, show me which step went wrong.
- For graded homework or labs: hints and explanations only, never the submission.
