# Learning brief: EE502 L10 - LTV state equation solution

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 13 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_10/EE502 L10 - LTV state equation solution.md`
2. **Quiz note** (13 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_10/EE502 L10 - LTV state equation solution - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 103-109)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_10/EE502_Lecture_10_LTV_Solution.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_10/lecture_10.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. The LTV equations, existence and uniqueness (slide 104)
- 2. Fundamental matrix (slide 105)
- 3. State transition matrix (slide 106)
- 4. Properties and the solution formula (slide 107)
- 5. Computing the state transition matrix (slides 108-109)
- 6. Extras in our notes (not on these slides)

## Known errors and traps in the sources (do not teach the errors)

- **Slide slip:** The slide solves the example with $t_0=0$. Its last line is labelled $\Phi(t,t_0)$, but it uses $X(0)^{-1}$, so it is $\Phi(t,0)$. Do not read it as the formula for a general $t_0$: there the entry $(2,1)$ is $\tfrac{t^2-t_0^2}{2}$, as in the example above (sl...
- **Slide slips:** The slide states the solution "for $t\ge 0$" and writes the feedthrough as $D\mathbf{u}(t)$. Intended: $t\ge t_0$ and the time-varying $D(t)\mathbf{u}(t)$. The inverse of $\Phi$ is "swap the arguments", not the transpose. In the product the later leg stands on...
- **Watch out:** - Never write $\Phi=e^{\int A}$ without the commutation test. - Frozen-time eigenvalues say nothing reliable: $A(t)=\begin{bmatrix}-1&e^{2t}\\0&-1\end{bmatrix}$ has eigenvalues $-1,-1$ for every $t$, yet $\Phi_{12}(t,0)=\sinh t$ grows without bound.
- **Slide error:** The series on slide 109 is written $I_2+M+M^2+\cdots$, without the factors $\tfrac{1}{k!}$. The correct series is $I+M+\tfrac{1}{2!}M^2+\tfrac{1}{3!}M^3+\cdots$. The result on the slide is still right, because $M^2=0$ in this example.

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
