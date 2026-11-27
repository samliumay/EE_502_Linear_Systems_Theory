# Learning brief: EE502 L14 - Observability

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 17 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_14/EE502 L14 - Observability.md`
2. **Quiz note** (17 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_14/EE502 L14 - Observability - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 140-152, 160-162)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_14/lecture_14.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Definition and two examples (slides 141-142)
- 2. The observability Gramian (slides 143-144)
- 3. Duality and the main theorem (slides 145-146)
- 4. Invariance, controllable and uncontrollable parts (slides 147-150)
- 5. Observable parts and the Kalman decomposition (slides 151-152)
- 6. Observability of LTV systems (slides 161-162)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** The slide writes $y(0)=x_{01}+x_{02}$. With $D=1$ it is $y(0)=x_{01}+x_{02}+u(0)$, so subtract $u(0)$ as above. Also: "not measured" does not mean "unobservable". Only the tests decide.
- **Watch out:** $\mathcal{C}$ is a block row, $\mathcal{O}$ is a block column. For controllability the bad vector is a left eigenvector ($\mathbf{v}^{\mathsf T}B=\mathbf{0}^{\mathsf T}$). For observability it is a right eigenvector: $A\mathbf{w}=\lambda\mathbf{w}$ and $C\math...
- **Slide slip (p. 149):** The proof states that $\hat{\mathcal{C}}$ has rank $n$. Since $\hat{\mathcal{C}}=P\mathcal{C}$, the rank is $n_1$.
- **Slide slips (p. 151):** The completing rows are printed as $\mathbf{p}_{n_1+1},\dots,\mathbf{p}_n$ and the output matrix as $[\hat C_c\ \ 0]$. Intended: $\mathbf{p}_{n_2+1},\dots,\mathbf{p}_n$ and $[\hat C_o\ \ 0]$.
- **Watch out:** The LTV dual uses $-A^{\mathsf T}(t)$, not $A^{\mathsf T}(t)$. The rank test is sufficient only, and the recursion includes the derivative $\dot N_k$. The slide lists "$k=0,\dots,n-2$" for the recursion index; the test uses $N_0,\dots,N_{n-1}$.

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
