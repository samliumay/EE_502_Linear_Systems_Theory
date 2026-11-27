# Learning brief: EE502 L13 - Controllability

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 19 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_13/EE502 L13 - Controllability.md`
2. **Quiz note** (19 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_13/EE502 L13 - Controllability - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 130-139, 153-159)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_13/EE502_Lecture_13_Controllability.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_13/lecture_13.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Definition and two examples (slides 131-132)
- 2. Main theorem of LTI controllability (slides 133-137)
- 3. Gramian example and the double pendulum (slides 138-139)
- 4. LTV controllability and the Gramian test (slides 154-156)
- 5. A sufficient rank condition for LTV (slides 157-159)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** PBH must hold at **every** eigenvalue. In Example 1, $\lambda=2$ passes and $\lambda=0$ fails. A rank drop at $\lambda$ gives a left vector $\mathbf{v}^{\mathsf T}$, and $\mathbf{v}^{\mathsf T}\mathbf{x}$ is the combination the input cannot change.
- **Slide misprint (p. 139):** The $(3,4)$ entry of $A^3$ is printed as $1$. It is $-c$ (row 3 of $A^3$ is row 4 of $A^2$). The matrix $\mathcal{C}$ on the slide is correct.
- **Slide slips (p. 155):** The input formula is printed with $B(t)^{\mathsf T}$ and without the brackets around $\Phi(t_f,t_0)\mathbf{x}_0-\mathbf{x}_f$. Read it as above, with $B(\tau)^{\mathsf T}$. "For some $t_f>0$" should be $t_f>t_0$.
- **Watch out:** - Sufficient only: rank $<n$ proves nothing. Then use the Gramian. - Do not forget the derivative term $\dot M_k$. - The slide says "$M_k$ for $k=0,1,\dots,n-2$" for the recursion index; the test uses $M_0,\dots,M_{n-1}$.
- **Slide slip (p. 159):** Example 2 ends with "controllable at any $t_0>0$". The condition $t_0>0$ is not needed: $t^2+1\ne0$ for all real $t$, so the pair is controllable at every $t_0$.

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
