# Learning brief: EE502 L02 - LTI models and linearization

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 21 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_02/EE502 L02 - LTI models and linearization.md`
2. **Quiz note** (21 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_02/EE502 L02 - LTI models and linearization - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 12-35)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_02/EE502_Lecture_02_LTI_Models.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_02/lecture_02.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. Linearity and input-linearity (slide 15)
- 2. Impulse response (slides 16-18)
- 3. Time invariance (slides 19-20)
- 4. Example: feedback loop with a unit delay (slide 21)
- 5. Transfer function and transfer matrix (slides 22-23)
- 6. Rational vs irrational, poles and zeros (slides 24-26)
- 7. Transfer matrix terminology, blocking zeros (slides 27-28)
- 8. State-space representation of LTI systems (slides 29-30)
- 9. Example: mass-spring-damper (slide 31)
- 10. Linearization (slides 32-34)
- 11. Modelling example: double pendulum (slide 35)

## Known errors and traps in the sources (do not teach the errors)

- **Watch out:** - Adding inputs while keeping the same nonzero initial state is not a linearity test. Test on $\dot x=-x+u$: $(y_1+y_2)-y_3=e^{-t}x_0\neq0$. - An affine map such as $y=2u+3$ is not linear: zero input gives a nonzero output.
- **Watch out:** Slide 18 says $g_{ij}$ is the response "at the j-th output to an impulse at the i-th input". The matrix product gives $y_i=\sum_j\int g_{ij}u_j$, so the **row $i$ is the output, the column $j$ is the input** (Chen's convention). Slide 23 has the same swap for ...
- **Watch out:** Slide typos: the third term is printed $a^3(t-3)$, it is $a^3\delta(t-3)$. The integrand is printed $g_f(t)r(\tau)$, it is $g_f(t-\tau)r(\tau)$.
- **Watch out:** $\hat y=\hat g\hat u$ is only the zero-state response. A nonzero initial state adds a term (section 8).
- **Watch out:** Lumped implies rational, one direction only. A non-rational $\hat g$ proves "distributed".
- **Watch out:** Every pole of $\hat G$ is an eigenvalue of $A$. The converse fails: a factor of $\det(sI-A)$ can cancel. Example: $A=\operatorname{diag}(-1,-2)$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&1\end{bmatrix}$ gives $\hat g=\dfrac{1}{s+1}$.
- **Watch out:** The slide prints the second state as "$x_1:=\dot y$". It is $x_2:=\dot y$.
- **Watch out:** - Slide 33 gives the sizes of $C(t)$ and $D(t)$ as $n\times n$ and $n\times p$. They are $q\times n$ and $q\times p$. - The linear model is in the deviations $\tilde{\mathbf{x}}=\mathbf{x}-\mathbf{x}_o$, not in $\mathbf{x}$. - $\tilde u_1$ drops out in the sli...
- **Watch out:** The slide states the assumption as "$\sin\theta_1\cong0$". The matrix shown needs $\sin\theta_i\cong\theta_i$ (first-order terms kept).

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
