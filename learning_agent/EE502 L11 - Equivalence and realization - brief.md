# Learning brief: EE502 L11 - Equivalence and realization

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 15 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_11/EE502 L11 - Equivalence and realization.md`
2. **Quiz note:** not written yet for this lesson. Use the check questions of the lesson note.
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 94-102, 110-113)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_11/EE502_Lecture_11_Equivalence_Realization.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_11/lecture_11.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Change of state and equivalence (slides 94-95)
- 2. Same transfer matrix does not imply equivalence (slide 96)
- 3. Realization of a proper transfer matrix (slides 98-100)
- 4. Examples and the controllable canonical form (slides 101-102)
- 5. Equivalence of time-varying representations (slides 110-111)
- 6. Not every transformation is Lyapunov; periodic systems (slides 112-113)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** $P$ goes on the left of $B$, $P^{-1}$ on the right of $C$.
- **Slide typo:** The slide prints the left side of the node-voltage equation as $u-i+u-i-i_c$. The current label in the figure is $u-i+i_c$, and only that sign gives the stated result $u=2i-i_c$.
- **Slide error:** Slide 100 prints $Z_j\in\mathbf{R}(s)^{n\times p}$. Each block $Z_j$ is $p\times p$. The whole $Z$ is $n\times p$ with $n=pr$. Reading help for slide 99: "at least one less than the degree $r$" means the degree of $N(s)$ is at most $r-1$, because $N/d$ is stri...
- **Slide typo (p. 101, second realization):** The slide prints the second $A$ as $\operatorname{diag}(-\tfrac52,-\tfrac52)$. With the printed $B=\begin{bmatrix}-6&3\\12&-\tfrac32\end{bmatrix}$ and $C=\begin{bmatrix}1&0\end{bmatrix}$ that gives a pole at $-\tfrac52$, which $G$ does not have. The matrix tha...
- **Watch out:** - Do the long division first and make $d$ monic. The top row holds the **negated** coefficients. - A common root of $n(s)$ and $d(s)$ leaves a hidden mode in the realization. Cancel first: a coprime $g$ of degree $r$ needs exactly $r$ states. - Every pole of $...
- **Watch out:** Never decide from the frozen eigenvalues of $A(t)$. Markus-Yamabe example in our notes: the frozen eigenvalues are $-\tfrac14\pm\tfrac{\sqrt7}{4}j$ for every $t$, yet one solution grows like $e^{t/2}$.

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
