# Learning brief: EE502 L07 - Jordan form

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 15 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_07/EE502 L07 - Jordan form.md`
2. **Quiz note** (15 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_07/EE502 L07 - Jordan form - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`, `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_jordanformexplanation2`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 61-67) + lectures/jordanFormExplanation2.pdf`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_07/EE502_Lecture_07_Jordan_Form.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_07/lecture_07.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Generalized eigenvectors and chains (slides 61-62)
- 2. Example 2 continued (slide 63)
- 3. Jordan normal form theorem (slide 64)
- 4. Which Jordan forms are possible (slides 65-67)
- 5. Instructor's handout: the tree of eigenvectors (handout pages 2-5)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** - Both conditions in (4) are needed. An eigenvector also satisfies $(A-\lambda I)^2\mathbf{v}=\mathbf{0}$, yet its grade is 1. - The slide says $\mathbf{v}\in\mathbb{R}^n$. For a non-real $\lambda$ the vector is complex, so $\mathbf{v}\in\mathbb{C}^n$ in gener...
- **Watch out:** The slide prints the second row of $(A-I)^2$ as $[1\ \ 0\ \ -2]$. The correct row is $[-1\ \ 0\ \ -2]$. With the misprint, $\mathbf{v}_2$ would not satisfy $(A-I)^2\mathbf{v}_2=\mathbf{0}$.
- **Watch out:** - Slide 66, Case 1: "an eigenvector of multiplicity $n_1$" means an **eigenvalue** of multiplicity $n_1$. Case 2: $\Lambda_1=\{J_{11},J_{12},J_{13}\}$ means $\operatorname{diag}\{J_{11},J_{12},J_{13}\}$. - Slide 67, Case 4(i) lists the $1\times1$ block $\lambd...
- **Watch out:** - Direction: the handout goes up from the eigenvector (solve $N\mathbf{x}=\mathbf{v}_{ij1}$). The slides go down from the top vector (multiply by $N$). Same $J$. - The handout assumes which eigenvector produces what. With $n_1=5$ and nullity 3, both 2+2+1 and ...

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
