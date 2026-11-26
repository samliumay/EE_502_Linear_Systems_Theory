# Learning brief: EE502 L05 - Functions of a matrix

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 12 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_05/EE502 L05 - Functions of a matrix.md`
2. **Quiz note:** not written yet for this lesson. Use the check questions of the lesson note.
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 68-77)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_05/EE502_Lecture_05_Matrix_Functions.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_05/lecture_05.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Polynomials of a matrix (slide 69)
- 2. Cayley-Hamilton theorem (slide 70)
- 3. Minimal polynomial (slides 71-73)
- 4. Indices and the interpolating polynomial (slide 74)
- 5. Examples: A^100, e^{At}, f of a Jordan block (slides 75-77)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** $f(A)$ is not "apply $f$ to every entry". For $A=\begin{bmatrix}1&2\\0&3\end{bmatrix}$, $A^2=\begin{bmatrix}1&8\\0&9\end{bmatrix}$, not $\begin{bmatrix}1&4\\0&9\end{bmatrix}$.
- **Watch out:** - Slide 72 concludes "$\Phi$ divides $\Psi$" after the first division. With $r\equiv0$, $\Phi=\Psi q$, so it is $\Psi$ that divides $\Phi$. The argument is symmetric, so the result stands. - $\Psi$ divides $\Delta$, but a factor of $\Delta$ does not automatica...
- **Watch out:** - The slide says "degree $n$" and "$l=1,\dots,n_i-1$". Correct: degree at most $n-1$, and $l$ starts at 0 (the values themselves must match). That gives $n$ conditions for $n$ unknowns. - For $f(\lambda)=e^{\lambda t}$ differentiate with respect to $\lambda$. ...
- **Watch out:** On slide 77 the left side of the display in Example 3 is written $e^{Jt}$. It is $f(J)$ for a general $f$, and $e^{Jt}$ only for $f(\lambda)=e^{\lambda t}$.

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
