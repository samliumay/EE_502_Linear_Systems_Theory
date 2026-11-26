# Learning brief: EE502 L04 - Equations, eigenvalues, diagonalization

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 14 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_04/EE502 L04 - Equations, eigenvalues, diagonalization.md`
2. **Quiz note:** not written yet for this lesson. Use the check questions of the lesson note.
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 47-60)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_04/EE502_Lecture_04_Equations_Eigenvalues.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_04/lecture_04.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Existence of solutions of Ax = y (slides 47-48)
- 2. The set of all solutions (slides 49-51)
- 3. Determinants and inverses (slides 52-53)
- 4. Similarity transformation and companion form (slides 54-55)
- 5. Eigenvalues and eigenvectors (slide 56)
- 6. Diagonalization, distinct eigenvalues (slides 57-58)
- 7. Diagonalization, repeated eigenvalues (slides 59-60)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** - Slide 48, converse of (ii): it says "has a solution for **a** $\mathbf{y}$". The argument needs a solution for **every** $\mathbf{y}\in\mathbb{R}^m$. ($\mathbf{y}=\mathbf{0}$ is always solvable, whatever the rank.) - Part (ii) needs $n\ge m$. That is necessa...
- **Watch out:** - Slide 49 writes $\alpha_1,\dots,\alpha_n$. There are only $\nu$ coefficients. - Slide 50: "reduced column echelon form" should be "reduced row echelon form", and the identity block is $I_{n-r}$.
- **Watch out:** Slide errors found by our notes: - Slide 52 says "$\det A=0$ iff ... columns of $A$ are linearly **independent**". It must be **dependent**. - $M_{ij}$ is the matrix, not its determinant. The triangular product rule is a consequence of Laplace's formula, not a...
- **Watch out:** - Slide 55 prints the third row of $B$ as $[1\ \ 1\ \cdots\ 0\ \ \beta_3]$. The correct row is $[0\ \ 1\ \cdots\ 0\ \ \beta_3]$. - Similar implies same eigenvalues. The converse is false (the two examples of section 7).
- **Watch out:** Eigenvectors are never unique (any nonzero multiple works). A repeated root does not guarantee as many independent eigenvectors as its multiplicity.
- **Watch out:** Distinct eigenvalues imply diagonalizable. The converse is false: $I_n$ is diagonal with all eigenvalues equal.
- **Watch out:** Slide 59 prints the third row of $A-I$ in Example 1 as $[1\ \ 0\ \ -2]$. Since $a_{33}=3$, the correct row is $[1\ \ 0\ \ 2]$.

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
