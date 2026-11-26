# Learning brief: EE502 L08 - Positive definiteness and SVD

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 12 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_08/EE502 L08 - Positive definiteness and SVD.md`
2. **Quiz note:** not written yet for this lesson. Use the check questions of the lesson note.
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 81-88)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_08/EE502_Lecture_08_PosDef_SVD.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_08/lecture_08.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Symmetric matrices (slides 81-82)
- 2. Positive definite matrices (slides 83-84)
- 3. Singular values and the SVD (slides 85-87)
- 4. Condition number (slide 88)

## Known errors and traps in the sources (do not teach the errors)

- **Slide error: the semi-definite minors test:** The slide says "$M\ge 0$ iff every leading minor is nonnegative". False: $\begin{bmatrix}0&0\\0&-1\end{bmatrix}$ has $D_1=D_2=0$ but the form is $-1$ at $(0,1)$. For $M\ge 0$ check **all** principal minors (same rows and columns chosen), or the eigenvalues.
- **Watch out:** The tests need a symmetric $M$. $\begin{bmatrix}1&4\\0&1\end{bmatrix}$ has eigenvalues $1,1$ but its form is $-2$ at $(1,-1)$. Positive entries are not enough either: $\begin{bmatrix}1&2\\2&1\end{bmatrix}$ has eigenvalues $3,-1$.
- **Slide slip: order of the singular values:** The slide says "in ascending order". The standard convention (MATLAB `svd`, the condition number) is descending: $\sigma_1$ is the largest.
- **Slide typos:** - The slide writes $\sigma_n=\lVert A^{-1}\rVert_2$. Correct: $\sigma_n=1/\lVert A^{-1}\rVert_2$. - The slide writes $H=RSQ$ in Remark 2. The transpose is intended: $H=RSQ^{\mathsf T}$. - $\kappa$ uses singular values, not eigenvalues. They agree only for symm...

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
