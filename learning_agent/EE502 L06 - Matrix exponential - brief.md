# Learning brief: EE502 L06 - Matrix exponential

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 11 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_06/EE502 L06 - Matrix exponential.md`
2. **Quiz note:** not written yet for this lesson. Use the check questions of the lesson note.
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 78-80)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_06/EE502_Lecture_06_Matrix_Exponential.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_06/lecture_06.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Power series definition of f(A) (slides 78-79)
- 2. Properties of the matrix exponential (slide 80)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** - $e^{At}$ is not "$e$ to each entry". Zero entries do not become $e^0=1$. - A divergent series does not mean $f(A)$ is undefined. For $f(\lambda)=1/(1-\lambda)$ and $A=\operatorname{diag}(0.5,2)$ the series diverges, yet $f(A)=(I-A)^{-1}=\operatorname{diag}(2...
- **Watch out:** - P4 needs $AB=BA$. Counterexample: $A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$, $B=\begin{bmatrix}0&0\\1&0\end{bmatrix}$. Then $e^{(A+B)t}=\begin{bmatrix}\cosh t&\sinh t\\ \sinh t&\cosh t\end{bmatrix}$, but $e^{At}e^{Bt}=\begin{bmatrix}1+t^2&t\\t&1\end{bmatrix}$...

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
