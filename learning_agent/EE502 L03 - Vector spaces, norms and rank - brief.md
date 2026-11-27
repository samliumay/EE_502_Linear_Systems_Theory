# Learning brief: EE502 L03 - Vector spaces, norms and rank

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 10 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_03/EE502 L03 - Vector spaces, norms and rank.md`
2. **Quiz note** (10 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_03/EE502 L03 - Vector spaces, norms and rank - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 36-46)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_03/EE502_Lecture_03_Vector_Spaces_Rank.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_03/lecture_03.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Vector space, subspace, span, independence (slides 37-38)
- 2. Dimension, basis, representation (slides 39-40)
- 3. Norms (slide 41)
- 4. Orthonormal sets and Gram-Schmidt (slides 42-43)
- 5. Row echelon form (slide 44)
- 6. Rank and nullity (slides 45-46)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** - Containing $\mathbf{0}$ does not make a set a subspace (the two coordinate axes together fail addition). Missing $\mathbf{0}$ proves "not a subspace". - More than $n$ vectors in $\mathbb{R}^n$ are always dependent. But $n$ or fewer are not automatically inde...
- **Watch out:** The slide lists the representation as $[11/4\ \ -3/2]^{\mathsf T}$. That is the order $\{\mathbf{q}_2,\mathbf{q}_1\}$. With $\mathbf{q}_1=[1\ \ 3]^{\mathsf T}$ first, as stated, it is $\tilde{\mathbf{x}}=[-3/2\ \ 11/4]^{\mathsf T}$. The order of the basis vect...
- **Watch out:** Project onto the unit vectors $\mathbf{u}_k$, not onto the raw $\mathbf{v}_k$. If the list is dependent, some $\mathbf{q}_j=\mathbf{0}$ and the normalization divides by zero.
- **Watch out:** Slide errors found by our notes: - Slide 45: $B$ is $r\times(n-r)$, not $m\times(n-r)$. "$\check A=AP$" means $[\hat A_1\ \ \hat A_2]=AP$. - Slide 46: "reduced column echelon form" should be "reduced row echelon form". The identity block in $\begin{bmatrix}-B\...

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
