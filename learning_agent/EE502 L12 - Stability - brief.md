# Learning brief: EE502 L12 - Stability

This file is for the LearnHarness teacher agent. Read it first, then read the files it lists.

## Goal

Teach me this lecture of EE 502 Linear System Theory so that I understand every slide and can answer its questions without help.
Exams are matrix computations and short proofs (state equations, matrix functions, Jordan form, stability, controllability, observability).

## Sources, in priority order

1. **Lesson note** (my notes, slide by slide, with 16 check questions and their answers): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_12/EE502 L12 - Stability.md`
2. **Quiz note** (16 multiple-choice questions, one per check question, each with a folded answer that explains every option): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/lessons/lecture_12/EE502 L12 - Stability - quiz.md`
3. **Slide images** (one jpg per slide; the lesson note embeds them as `![[<deck>_pNNN.jpg]]`): `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/EE_502_Linear_Systems_Theory/others/slides/ee502_eee501alllecturenotesabo`
4. **Original slides (PDF):** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf (pp. 114-129)`
5. **Full step-by-step notes:** `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf` (LaTeX source: `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_12/lecture_12.tex`)

The slides are the authority for what the course teaches. Text marked "(beyond the slides)" in the lesson note is extra explanation: use it to explain, do not present it as exam material.

## What the lecture covers

- 1. BIBO stability, single input and output (slides 115-117)
- 2. BIBO stability, multivariable case (slide 118)
- 3. Internal stability: poles and eigenvalues (slides 119-120)
- 4. Lyapunov theorem (slides 121-123)
- 5. Routh-Hurwitz criterion (slide 124)
- 6. BIBO stability of LTV systems (slides 126-127)
- 7. Stability of LTV state representations (slides 128-129)

## Known errors and traps in the sources (do not teach the errors)

- **Slide error (p. 117 example):** For $\hat g(s)=\dfrac{s+3}{(s+2)(s+1)^3}$ the slide's expansion is wrong. Correct: $$\hat g(s)=\frac{2}{(s+1)^3}-\frac{1}{(s+1)^2}+\frac{1}{s+1}-\frac{1}{s+2},\qquad g(t)=(t^2-t+1)e^{-t}-e^{-2t}.$$ In the triangle-inequality bound every term enters with a plus...
- **Watch out:** $g(t)\to 0$ is not enough: $1/(1+t)\to 0$ but $\int_0^T\tfrac{dt}{1+t}=\ln(1+T)\to\infty$.
- **Watch out:** - BIBO-stable does not imply internally stable (hidden eigenvalues). Asymptotically stable does imply BIBO-stable. - Marginally stable does not imply BIBO-stable (the integrator $1/s$). - The slide says "for every nonzero initial state and for every input" $x\...
- **Slide misprint (Remark 1):** The third term of $\mathbf{v}^*M\mathbf{v}$ is printed as $-j\mathbf{v}_r^{\mathsf T}M\mathbf{v}_r$. Correct: $\mathbf{v}^*M\mathbf{v}=\mathbf{v}_r^{\mathsf T}M\mathbf{v}_r+j\mathbf{v}_r^{\mathsf T}M\mathbf{v}_i-j\mathbf{v}_i^{\mathsf T}M\mathbf{v}_r+\mathbf{v...
- **Watch out:** Positive coefficients do not prove stability for $n\ge 3$: the slide's polynomial has only positive coefficients and two unstable roots.

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
