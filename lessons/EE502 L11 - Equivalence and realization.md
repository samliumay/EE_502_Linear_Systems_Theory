---
course: EE 502 Linear System Theory
lecture: 11
title: Equivalence and realization
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 94-102, 110-113)
full_notes: lecture_notes/lecture_11/EE502_Lecture_11_Equivalence_Realization.pdf
---
# EE 502 · Lecture 11 · Equivalence of state representations, realizations

> [!summary] In short
> - A change of state $\hat{\mathbf{x}}=P\mathbf{x}$ gives the equivalent model $(PAP^{-1},PB,CP^{-1},D)$. It keeps the eigenvalues, the transfer matrix and all $CA^kB$.
> - Same transfer matrix does **not** imply equivalence: $G(s)$ sees only the zero-state response.
> - $G(s)$ has a realization $(A,B,C,D)$ if and only if it is proper. $D=G(\infty)$. The block construction gives $n=pr$ states.
> - One input, one output: the controllable canonical form is "copy the coefficients". Its transpose is the observable canonical form.
> - Time-varying change $\hat{\mathbf{x}}=P(t)\mathbf{x}$: $\hat A=(PA+\dot P)P^{-1}$. Only Lyapunov transformations ($P$, $P^{-1}$ bounded) keep stability visible.

Slide numbers below are pages of the 220-page ABO file. Midterm and final material.

## 1. Change of state and equivalence (slides 94-95)
![[ee502_eee501alllecturenotesabo_p094.jpg]]
![[ee502_eee501alllecturenotesabo_p095.jpg]]

**Notes.** Start from $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$. Define $\hat{\mathbf{x}}:=P\mathbf{x}$ with $P$ nonsingular. Then $\mathbf{x}=P^{-1}\hat{\mathbf{x}}$ and
$$\hat A=PAP^{-1},\qquad \hat B=PB,\qquad \hat C=CP^{-1},\qquad \hat D=D.$$
The two quadruples are called **(algebraically) equivalent**.

**Fact.** Equivalent representations have
1. the same characteristic and minimal polynomials ($\hat A$ is similar to $A$),
2. the same transfer matrix: $\hat C(sI-\hat A)^{-1}\hat B=CP^{-1}P(sI-A)^{-1}P^{-1}PB=C(sI-A)^{-1}B$,
3. the same Markov parameters: $\hat C\hat A^{k}\hat B=CA^{k}B$, $k=0,1,2,\dots$ (coefficients of $s^{-k-1}$ in the expansion of $G$).

> [!warning] Watch out
> $P$ goes on the left of $B$, $P^{-1}$ on the right of $C$.

## 2. Same transfer matrix does not imply equivalence (slide 96)
![[ee502_eee501alllecturenotesabo_p096.jpg]]

**Notes.** Circuit 1 has no storage element: $y=0.5u$, order 0, $G(s)=0.5$. Circuit 2 has one capacitor with voltage $x_c$:
$$\dot x_c=-x_c,\qquad y=-0.5x_c+0.5u .$$
Here $B=0$, so $G(s)=C(sI-A)^{-1}B+D=0.5$ again. Same transfer function, but order 0 against order 1, so no square $P$ can relate them. With $x_c(0)\ne 0$ the zero-input part $-\tfrac12e^{-t}x_c(0)$ shows at the output of circuit 2 only.

> [!warning] Slide typo
> The slide prints the left side of the node-voltage equation as $u-i+u-i-i_c$. The current label in the figure is $u-i+i_c$, and only that sign gives the stated result $u=2i-i_c$.

## 3. Realization of a proper transfer matrix (slides 98-100)
![[ee502_eee501alllecturenotesabo_p098.jpg]]
![[ee502_eee501alllecturenotesabo_p099.jpg]]
![[ee502_eee501alllecturenotesabo_p100.jpg]]

**Notes.** $(A,B,C,D)$ is a **realization** of $G(s)$ ($q\times p$, rational entries) if $G(s)=C(sI-A)^{-1}B+D$. Since $C(sI-A)^{-1}B$ is strictly proper, $G$ must be proper. **Theorem:** a realization exists if and only if $G$ is proper.

Construction (this is the proof):
1. $G(s)=G_{sp}(s)+G(\infty)$, with $D:=G(\infty)$ and $G_{sp}$ strictly proper.
2. Pick a monic common denominator $d(s)=s^{r}+\alpha_1s^{r-1}+\dots+\alpha_r$, so that $N(s)=d(s)G_{sp}(s)=N_1s^{r-1}+\dots+N_r$ is a polynomial matrix, $N_j\in\mathbb{R}^{q\times p}$.
3. Fill the blocks (each $p\times p$, total $n=pr$):
$$A=\begin{bmatrix}-\alpha_1I_p&-\alpha_2I_p&\cdots&-\alpha_rI_p\\ I_p&0&\cdots&0\\ \vdots&\ddots&&\vdots\\ 0&\cdots&I_p&0\end{bmatrix},\quad B=\begin{bmatrix}I_p\\0\\ \vdots\\0\end{bmatrix},\quad C=\begin{bmatrix}N_1&N_2&\cdots&N_r\end{bmatrix}.$$

Why it works: with $Z=(sI-A)^{-1}B$ split into blocks $Z_1,\dots,Z_r$, the equation $sZ=AZ+B$ gives $Z_k=\dfrac{s^{r-k}}{d(s)}I_p$. Then $CZ=N(s)/d(s)=G_{sp}(s)$.

## 4. Examples and the controllable canonical form (slides 101-102)
![[ee502_eee501alllecturenotesabo_p101.jpg]]
![[ee502_eee501alllecturenotesabo_p102.jpg]]

**Notes.**

> [!example] Slide example (p. 101): $G(s)=\begin{bmatrix}\dfrac{4s-10}{2s+1}&\dfrac{3}{s+2}\end{bmatrix}$
> $p=2$, $q=1$, $G(\infty)=\begin{bmatrix}2&0\end{bmatrix}$, $G_{sp}=\begin{bmatrix}\dfrac{-6}{s+1/2}&\dfrac{3}{s+2}\end{bmatrix}$.
> $d(s)=(s+\tfrac12)(s+2)=s^2+\tfrac52s+1$, $N(s)=\begin{bmatrix}-6&3\end{bmatrix}s+\begin{bmatrix}-12&\tfrac32\end{bmatrix}$. Block form, 4 states:
> $$A=\begin{bmatrix}-\tfrac52&0&-1&0\\0&-\tfrac52&0&-1\\1&0&0&0\\0&1&0&0\end{bmatrix},\ B=\begin{bmatrix}1&0\\0&1\\0&0\\0&0\end{bmatrix},\ C=\begin{bmatrix}-6&3&-12&\tfrac32\end{bmatrix},\ D=\begin{bmatrix}2&0\end{bmatrix}.$$
> A two-state realization also exists, so the block form is not minimal: four eigenvalues, two poles.

> [!warning] Slide typo (p. 101, second realization)
> The slide prints the second $A$ as $\operatorname{diag}(-\tfrac52,-\tfrac52)$. With the printed $B=\begin{bmatrix}-6&3\\12&-\tfrac32\end{bmatrix}$ and $C=\begin{bmatrix}1&0\end{bmatrix}$ that gives a pole at $-\tfrac52$, which $G$ does not have. The matrix that fits is $A=\begin{bmatrix}-\tfrac52&-1\\1&0\end{bmatrix}$.
> A diagonal alternative: $A=\operatorname{diag}(-\tfrac12,-2)$, $B=\operatorname{diag}(-6,3)$, $C=\begin{bmatrix}1&1\end{bmatrix}$, $D=\begin{bmatrix}2&0\end{bmatrix}$.

**Controllable canonical realization** ($p=q=1$). Write $g(s)=\dfrac{n(s)}{d(s)}+g(\infty)$ with $d$ monic of degree $r$ and $n(s)=n_1s^{r-1}+\dots+n_r$. Then
$$A=\begin{bmatrix}-\alpha_1&-\alpha_2&\cdots&-\alpha_r\\1&0&\cdots&0\\ \vdots&\ddots&&\vdots\\0&\cdots&1&0\end{bmatrix},\quad B=\begin{bmatrix}1\\0\\ \vdots\\0\end{bmatrix},\quad C=\begin{bmatrix}n_1&\cdots&n_r\end{bmatrix},\quad D=g(\infty).$$

> [!example] Slide example (p. 102): $g(s)=\dfrac{2s^2+3s-1}{s^2-2s-5}$
> Long division: $g=2+\dfrac{7s+9}{s^2-2s-5}$. $\alpha_1=-2$, $\alpha_2=-5$, $n_1=7$, $n_2=9$.
> $A=\begin{bmatrix}2&5\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}7&9\end{bmatrix}$, $D=2$.

**Observable canonical form** (our notes): the dual $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T},D)$. The $-\alpha_i$ fill the first column, the $n_i$ fill $B$, and $C=\begin{bmatrix}1&0&\cdots&0\end{bmatrix}$.

> [!warning] Watch out
> - Do the long division first and make $d$ monic. The top row holds the **negated** coefficients.
> - A common root of $n(s)$ and $d(s)$ leaves a hidden mode in the realization. Cancel first: a coprime $g$ of degree $r$ needs exactly $r$ states.
> - Every pole of $G$ is an eigenvalue of $A$. The converse is false.

## 5. Equivalence of time-varying representations (slides 110-111)
![[ee502_eee501alllecturenotesabo_p110.jpg]]
![[ee502_eee501alllecturenotesabo_p111.jpg]]

**Notes.** This part starts on the lower half of slide 109 (embedded in [[EE502 L10 - LTV state equation solution]]). For the LTV model, put $\hat{\mathbf{x}}(t)=P(t)\mathbf{x}(t)$ with $P(t)$ nonsingular and differentiable. The product rule adds a $\dot P$ term:
$$\hat A=(PA+\dot P)P^{-1},\qquad \hat B=PB,\qquad \hat C=CP^{-1},\qquad \hat D=D.$$

**Fact 6.** $\hat X(t)=P(t)X(t)$ is a fundamental matrix of the new system, and $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$.

**Fact 7 (too powerful).** For any constant $A_0$, the choice $P(t)=e^{A_0t}X(t)^{-1}$ gives $\hat A(t)=A_0$. So an unrestricted $P(t)$ can turn any LTV system into any LTI system, and can hide growth.

**Definition (Lyapunov transformation).** $P(t)$ nonsingular, $P$ and $\dot P$ continuous, $P$ and $P^{-1}$ bounded on the interval.

## 6. Not every transformation is Lyapunov; periodic systems (slides 112-113)
![[ee502_eee501alllecturenotesabo_p112.jpg]]
![[ee502_eee501alllecturenotesabo_p113.jpg]]

**Notes.**

> [!example] Slide example (p. 112)
> $A(t)=\begin{bmatrix}0&0\\t&0\end{bmatrix}$, $A_0=0$: $P(t)=X(t)^{-1}=\begin{bmatrix}1&0\\ \tfrac{t_0^2-t^2}{2}&1\end{bmatrix}$ gives $\hat A=0$. The entry $\tfrac{t_0^2-t^2}{2}$ is unbounded as $t\to\infty$, so $P$ is not a Lyapunov transformation on $[t_0,\infty)$. It is one on any finite $[t_0,t_f]$.

**Fact (Floquet).** Let $A(t)$ be piecewise continuous and periodic, $A(t+T)=A(t)$. Let $X(t)$ be a fundamental matrix and choose $\bar A$ with
$$e^{\bar AT}=X(0)^{-1}X(T)\quad\text{(monodromy matrix)}.$$
Then $P(t)=e^{\bar At}X(t)^{-1}$ is periodic, so $P$ and $P^{-1}$ are bounded: a Lyapunov transformation on $[0,\infty)$, with $\hat A(t)=\bar A$.

Stability test for a periodic system (our notes): the eigenvalues of the monodromy matrix (Floquet multipliers) must lie strictly inside the unit circle for all solutions to tend to zero.

> [!warning] Watch out
> Never decide from the frozen eigenvalues of $A(t)$. Markus-Yamabe example in our notes: the frozen eigenvalues are $-\tfrac14\pm\tfrac{\sqrt7}{4}j$ for every $t$, yet one solution grows like $e^{t/2}$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Algebraic equivalence | $(\hat A,\hat B,\hat C,\hat D)=(PAP^{-1},PB,CP^{-1},D)$ |
| Invariants | characteristic and minimal polynomial, $G(s)$, Markov parameters $CA^kB$ |
| Realization | $G(s)=C(sI-A)^{-1}B+D$; exists iff $G$ proper; $D=G(\infty)$ |
| Block construction | $n=pr$ states; top block row $-\alpha_jI_p$, $B=[I_p;0;\dots]$, $C=[N_1\cdots N_r]$ |
| Controllable form | top row $-\alpha_i$, $B=\mathbf{e}_1$, $C=[n_1\cdots n_r]$ |
| Observable form | $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T},D)$ of the controllable form |
| LTV change of state | $\hat A=(PA+\dot P)P^{-1}$, $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$ |
| Lyapunov transformation | $P,\dot P$ continuous; $P$, $P^{-1}$ bounded |
| Floquet | $e^{\bar AT}=X(0)^{-1}X(T)$, $P=e^{\bar At}X^{-1}$ periodic, $\hat A=\bar A$ |

## Check yourself
> [!question]- 1. Apply $P=\operatorname{diag}(2,1)$ to $A=\begin{bmatrix}0&1\\-2&-3\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$, $C=\begin{bmatrix}1&0\end{bmatrix}$.
> $\hat A=PAP^{-1}=\begin{bmatrix}0&2\\-1&-3\end{bmatrix}$, $\hat B=\begin{bmatrix}0\\1\end{bmatrix}$, $\hat C=\begin{bmatrix}\tfrac12&0\end{bmatrix}$.

> [!question]- 2. Can a 2-state and a 3-state model be equivalent? Can they have the same $G(s)$?
> Not equivalent: $P$ would be $3\times 2$, not invertible. Same $G$ is possible: add a state that neither the input nor the output touches.

> [!question]- 3. Realize $g(s)=\dfrac{3s+1}{s+2}$. Is $\dfrac{s^2}{s+1}$ realizable?
> $g=3+\dfrac{-5}{s+2}$: $A=-2$, $B=1$, $C=-5$, $D=3$. $\dfrac{s^2}{s+1}$ is improper, so it has no realization.

> [!question]- 4. Controllable and observable canonical forms of $g(s)=\dfrac{s+4}{s^2+5s+6}$.
> Controllable: $A=\begin{bmatrix}-5&-6\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&4\end{bmatrix}$, $D=0$. Observable: $A_o=\begin{bmatrix}-5&1\\-6&0\end{bmatrix}$, $B_o=\begin{bmatrix}1\\4\end{bmatrix}$, $C_o=\begin{bmatrix}1&0\end{bmatrix}$.

> [!question]- 5. Is the controllable form of $g(s)=\dfrac{s+1}{s^2+3s+2}$ minimal?
> No. $s^2+3s+2=(s+1)(s+2)$, so $g=\dfrac{1}{s+2}$. In the 2-state form the eigenvector $\mathbf{v}=(-1,1)^{\mathsf T}$ of $\lambda=-1$ has $C\mathbf{v}=0$: the mode $e^{-t}$ is unobservable. One state: $A=-2$, $B=1$, $C=1$.

> [!question]- 6. Is $P(t)=\begin{bmatrix}1&\sin t\\0&1\end{bmatrix}$ a Lyapunov transformation on $[0,\infty)$? And $P(t)=e^{-t}I$?
> First: yes. $P^{-1}=\begin{bmatrix}1&-\sin t\\0&1\end{bmatrix}$, all entries bounded, $\dot P$ continuous. Second: no, $P^{-1}=e^{t}I$ is unbounded. It would turn the unstable $\dot x=x$ into $\dot{\hat x}=0$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L10 - LTV state equation solution]]. Next: [[EE502 L12 - Stability]]
- Used later in: [[EE502 L13 - Controllability]], [[EE502 L14 - Observability]] (minimal realizations, canonical forms), [[EE502 L15 - State feedback (extra)]]
- Full step-by-step notes (PDF): [EE502_Lecture_11_Equivalence_Realization.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_11/EE502_Lecture_11_Equivalence_Realization.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_11/EE502_Lecture_11_Equivalence_Realization.pdf`
- Original slides (PDF, pp. 94-102 and 110-113): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: 97 (section title).
