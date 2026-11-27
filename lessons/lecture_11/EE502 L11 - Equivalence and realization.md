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

> [!question]- Check (slide 94): Take $A$ with rows $(1,\ 2)$ and $(0,\ 3)$, $B=(0,\ 1)^{\mathsf T}$, $C=(1,\ 0)$, $D=0$, and $P$ with rows $(1,\ 1)$ and $(0,\ 1)$. Find $\hat A,\hat B,\hat C$. Check that the eigenvalues and the transfer function do not change.
> Inverse: $P^{-1}=\begin{bmatrix}1&-1\\0&1\end{bmatrix}$ (check: $PP^{-1}=I$).
> $PA=\begin{bmatrix}1&5\\0&3\end{bmatrix}$, so $\hat A=PAP^{-1}=\begin{bmatrix}1&-1+5\\0&3\end{bmatrix}=\begin{bmatrix}1&4\\0&3\end{bmatrix}$.
> $\hat B=PB=\begin{bmatrix}1\\1\end{bmatrix}$, $\hat C=CP^{-1}=\begin{bmatrix}1&-1\end{bmatrix}$, $\hat D=0$.
> Eigenvalues: $A$ and $\hat A$ are upper triangular with diagonal $1,3$. Both have eigenvalues $1$ and $3$.
> Transfer function of the old model: $(sI-A)^{-1}=\dfrac{1}{(s-1)(s-3)}\begin{bmatrix}s-3&2\\0&s-1\end{bmatrix}$. Times $B$: $\dfrac{1}{(s-1)(s-3)}\begin{bmatrix}2\\s-1\end{bmatrix}$. Times $C$: $g(s)=\dfrac{2}{(s-1)(s-3)}$.
> New model: $(sI-\hat A)^{-1}\hat B=\dfrac{1}{(s-1)(s-3)}\begin{bmatrix}s-3&4\\0&s-1\end{bmatrix}\begin{bmatrix}1\\1\end{bmatrix}=\dfrac{1}{(s-1)(s-3)}\begin{bmatrix}s+1\\s-1\end{bmatrix}$. Times $\hat C$: $\dfrac{(s+1)-(s-1)}{(s-1)(s-3)}=\dfrac{2}{(s-1)(s-3)}$. The same.

> [!question]- Check (slide 95): Model 1 has $A_1$ with rows $(0,\ 1)$ and $(-2,\ -3)$, $B_1=(0,\ 1)^{\mathsf T}$, $C_1=(1,\ 0)$. Model 2 has $A_2=\operatorname{diag}(-1,-2)$, $B_2=(1,\ 1)^{\mathsf T}$, $C_2=(1,\ 1)$. Both have the eigenvalues $-1,-2$. Use item iii of the Fact to decide if they can be equivalent.
> Item iii says: equivalent models have the same $CA^kB$ for every $k$. One different value is enough to say "not equivalent".
> $k=0$: $C_1B_1=1\cdot 0+0\cdot 1=0$, but $C_2B_2=1+1=2$. They differ, so no $P$ exists.
> The same thing seen in $G$: $g_1(s)=\dfrac{1}{s^2+3s+2}=\dfrac{0}{s}+\dfrac{1}{s^2}+\dots$ and $g_2(s)=\dfrac{1}{s+1}+\dfrac{1}{s+2}=\dfrac{2s+3}{s^2+3s+2}=\dfrac{2}{s}-\dfrac{3}{s^2}+\dots$. The coefficient of $s^{-1}$ is $CB$, the coefficient of $s^{-2}$ is $CAB$ ($C_1A_1B_1=1$, $C_2A_2B_2=-1-2=-3$).
> Lesson: the same eigenvalues are necessary for equivalence, not sufficient.

## 2. Same transfer matrix does not imply equivalence (slide 96)
![[ee502_eee501alllecturenotesabo_p096.jpg]]

**Notes.** Circuit 1 has no storage element: $y=0.5u$, order 0, $G(s)=0.5$. Circuit 2 has one capacitor with voltage $x_c$:
$$\dot x_c=-x_c,\qquad y=-0.5x_c+0.5u .$$
Here $B=0$, so $G(s)=C(sI-A)^{-1}B+D=0.5$ again. Same transfer function, but order 0 against order 1, so no square $P$ can relate them. With $x_c(0)\ne 0$ the zero-input part $-\tfrac12e^{-t}x_c(0)$ shows at the output of circuit 2 only.

> [!warning] Slide typo
> The slide prints the left side of the node-voltage equation as $u-i+u-i-i_c$. The current label in the figure is $u-i+i_c$, and only that sign gives the stated result $u=2i-i_c$.

> [!info] Zero-state equivalence (beyond the slides)
> Two models are **zero-state equivalent** if they have the same transfer matrix. Then they give the same output for the same input when both start from $\mathbf{x}(0)=\mathbf{0}$. The dimensions may differ.
> **Algebraic equivalence** (section 1) is stronger. It needs the same dimension and a nonsingular $P$. It also matches the zero-input responses: the initial states are related by $\hat{\mathbf{x}}(0)=P\mathbf{x}(0)$.
> So: algebraically equivalent $\Rightarrow$ zero-state equivalent. The two circuits show that the converse is false.

> [!question]- Check (slide 96, circuit): The second circuit starts with $x_c(0)=4$ and the input is the constant $u(t)=2$ for $t\ge 0$. Find $y(t)$ for both circuits. Which part of $y$ does $G(s)=0.5$ explain?
> Circuit 1: $y=0.5u=1$ for all $t\ge0$.
> Circuit 2: $\dot x_c=-x_c$ does not contain $u$, so $x_c(t)=e^{-t}x_c(0)=4e^{-t}$.
> Output: $y=-0.5x_c+0.5u=-2e^{-t}+1$.
> $G(s)=0.5$ explains only the part $0.5u=1$ (zero-state response). The part $-2e^{-t}$ comes from the initial capacitor voltage (zero-input response). It dies out, but at $t=0$ circuit 2 gives $y=-1$ while circuit 1 gives $y=1$.

> [!question]- Check (slide 96, dimensions): Model 1 is $A=-2$, $B=1$, $C=1$, $D=0$. Model 2 has $A=\operatorname{diag}(-2,\ 1)$, $B=(1,\ 0)^{\mathsf T}$, $C=(1,\ 1)$, $D=0$. Do they have the same transfer function? Are they algebraically equivalent? What can the output of model 2 do that $G(s)$ does not show?
> Model 1: $g(s)=\dfrac{1}{s+2}$.
> Model 2: $(sI-A)^{-1}B=\begin{bmatrix}\tfrac{1}{s+2}\\0\end{bmatrix}$, so $g(s)=1\cdot\dfrac{1}{s+2}+1\cdot 0=\dfrac{1}{s+2}$. The same.
> Not algebraically equivalent: one state against two states, so $P$ would not be square.
> In model 2 the second state obeys $\dot x_2=x_2$ with no input. With $u=0$ the output is $y=e^{-2t}x_1(0)+e^{t}x_2(0)$. If $x_2(0)\ne0$ the output grows like $e^{t}$. The pole list of $g$ ($-2$ only) does not show the eigenvalue $+1$.

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

> [!info] Why $C(sI-A)^{-1}B$ is strictly proper (beyond the slides)
> Slide 98 says "the right hand side of (1) is proper" without a reason. Write $(sI-A)^{-1}=\dfrac{\operatorname{adj}(sI-A)}{\det(sI-A)}$. The denominator has degree $n$. Every entry of the adjugate is a determinant of size $n-1$, so its degree is at most $n-1$. Each entry of $C(sI-A)^{-1}B$ has numerator degree below denominator degree, so it tends to $0$ as $s\to\infty$. Adding the constant $D$ gives a proper matrix with $G(\infty)=D$.
> Terms: **proper** means numerator degree $\le$ denominator degree in every entry. **Strictly proper** means $<$. **Monic** means the leading coefficient is $1$.

> [!warning] Slide error
> Slide 100 prints $Z_j\in\mathbf{R}(s)^{n\times p}$. Each block $Z_j$ is $p\times p$. The whole $Z$ is $n\times p$ with $n=pr$.
> Reading help for slide 99: "at least one less than the degree $r$" means the degree of $N(s)$ is at most $r-1$, because $N/d$ is strictly proper.

> [!question]- Check (slide 98): Which of these have a realization $(A,B,C,D)$, and what is $D$? (a) $\dfrac{2s^2+1}{s^2+4}$, (b) $\dfrac{s^3}{s^2+1}$, (c) $\dfrac{1}{(s+1)^3}$, (d) $\dfrac{e^{-s}}{s+1}$.
> The test: realizable if and only if proper and rational.
> (a) Degrees $2$ and $2$: proper. $D=g(\infty)=2$ (ratio of the leading coefficients).
> (b) Degree $3$ over degree $2$: improper. No realization. It grows like $s$ as $s\to\infty$, but $C(sI-A)^{-1}B+D$ stays finite.
> (c) Degree $0$ over degree $3$: strictly proper. Realizable, $D=0$.
> (d) $e^{-s}$ (a time delay) is not a ratio of polynomials. Not rational, so no finite-dimensional realization.

> [!question]- Check (slide 99): One input, two outputs: $G(s)$ is the column with entries $\dfrac{1}{s+1}$ and $\dfrac{1}{s+2}$. Build the block realization. How many states does it have?
> $G$ is strictly proper, so $D=G(\infty)=\begin{bmatrix}0\\0\end{bmatrix}$. Here $p=1$, $q=2$.
> Common denominator: $d(s)=(s+1)(s+2)=s^2+3s+2$, so $r=2$, $\alpha_1=3$, $\alpha_2=2$.
> $N(s)=d(s)G(s)=\begin{bmatrix}s+2\\s+1\end{bmatrix}=\begin{bmatrix}1\\1\end{bmatrix}s+\begin{bmatrix}2\\1\end{bmatrix}$, so $N_1=\begin{bmatrix}1\\1\end{bmatrix}$, $N_2=\begin{bmatrix}2\\1\end{bmatrix}$.
> $$A=\begin{bmatrix}-3&-2\\1&0\end{bmatrix},\quad B=\begin{bmatrix}1\\0\end{bmatrix},\quad C=\begin{bmatrix}N_1&N_2\end{bmatrix}=\begin{bmatrix}1&2\\1&1\end{bmatrix}.$$
> States: $n=pr=1\cdot2=2$. The number of outputs $q$ changes only the number of rows of $C$.
> Check: $(sI-A)^{-1}B=\dfrac{1}{d}\begin{bmatrix}s\\1\end{bmatrix}$. Row 1 of $C$: $\dfrac{s+2}{(s+1)(s+2)}=\dfrac{1}{s+1}$. Row 2: $\dfrac{s+1}{(s+1)(s+2)}=\dfrac{1}{s+2}$.

> [!question]- Check (slide 100): Take $r=2$, $p=1$, $d(s)=s^2+5s+4$ and $C=(2,\ 3)$. Solve $sZ=AZ+B$ by hand for $Z_1,Z_2$ as on the slide. Then give $g(s)=CZ$.
> $A=\begin{bmatrix}-5&-4\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$. The two rows of $sZ=AZ+B$:
> Row 2: $sZ_2=Z_1$, so $Z_2=Z_1/s$.
> Row 1: $sZ_1=-5Z_1-4Z_2+1=-\left(5+\dfrac4s\right)Z_1+1$.
> Collect $Z_1$: $\left(s+5+\dfrac4s\right)Z_1=1$, that is $\dfrac{s^2+5s+4}{s}Z_1=1$, so $Z_1=\dfrac{s}{d(s)}$ and $Z_2=\dfrac{1}{d(s)}$.
> This is the pattern $Z_k=\dfrac{s^{r-k}}{d(s)}$: the powers of $s$ go down along the chain.
> $g(s)=CZ=2Z_1+3Z_2=\dfrac{2s+3}{s^2+5s+4}$. The entries of $C$ are the numerator coefficients.

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

> [!info] Minimal realization (beyond the slides)
> Slide 101 ends with "(2) is not necessarily a realization with minimum number of states". A realization with the smallest possible number of states is called a **minimal realization**. That smallest number is the **degree** of $G$ (McMillan degree).
> - One input, one output: after cancelling common factors of $n(s)$ and $d(s)$, the degree is the degree of $d(s)$. The controllable canonical form of the cancelled $g$ is minimal.
> - Several inputs: the block construction gives every input its own copy of all roots of $d(s)$, so it has $pr$ states. Often fewer are enough, as in the slide example ($4$ states against $2$).
> - General test (Lectures 13-14): a realization is minimal if and only if it is controllable and observable. All minimal realizations of the same $G$ are algebraically equivalent.

> [!question]- Check (slide 101): Two inputs, one output: $G(s)$ is the row with entries $\dfrac{s+3}{s+1}$ and $\dfrac{2}{s+3}$. Build the block realization. Then give a realization with fewer states.
> Step 1, split off $D$: $\dfrac{s+3}{s+1}=1+\dfrac{2}{s+1}$. So $D=G(\infty)=\begin{bmatrix}1&0\end{bmatrix}$ and $G_{sp}=\begin{bmatrix}\dfrac{2}{s+1}&\dfrac{2}{s+3}\end{bmatrix}$.
> Step 2: $d(s)=(s+1)(s+3)=s^2+4s+3$, $r=2$, $\alpha_1=4$, $\alpha_2=3$.
> $N(s)=d\,G_{sp}=\begin{bmatrix}2(s+3)&2(s+1)\end{bmatrix}=\begin{bmatrix}2&2\end{bmatrix}s+\begin{bmatrix}6&2\end{bmatrix}$.
> Step 3, $p=2$, so $n=pr=4$:
> $$A=\begin{bmatrix}-4&0&-3&0\\0&-4&0&-3\\1&0&0&0\\0&1&0&0\end{bmatrix},\ B=\begin{bmatrix}1&0\\0&1\\0&0\\0&0\end{bmatrix},\ C=\begin{bmatrix}2&2&6&2\end{bmatrix},\ D=\begin{bmatrix}1&0\end{bmatrix}.$$
> Fewer states: each entry of $G_{sp}$ has one pole, so one state per pole is enough.
> $A=\operatorname{diag}(-1,-3)$, $B=\operatorname{diag}(2,2)$, $C=\begin{bmatrix}1&1\end{bmatrix}$, $D=\begin{bmatrix}1&0\end{bmatrix}$.
> Check: $C(sI-A)^{-1}B=\begin{bmatrix}\dfrac{1}{s+1}&\dfrac{1}{s+3}\end{bmatrix}\begin{bmatrix}2&0\\0&2\end{bmatrix}=\begin{bmatrix}\dfrac{2}{s+1}&\dfrac{2}{s+3}\end{bmatrix}$.
> The 4-state $A$ has the eigenvalues $-1,-1,-3,-3$: each pole is built twice, once per input.

> [!question]- Check (slide 102, proper g): Find the controllable canonical realization of $g(s)=\dfrac{6s^2+2s+4}{2s^2+8s+6}$.
> Make the denominator monic (divide top and bottom by $2$): $g(s)=\dfrac{3s^2+s+2}{s^2+4s+3}$.
> Proper, equal degrees: $D=g(\infty)=3$.
> Remainder: $3s^2+s+2-3(s^2+4s+3)=3s^2+s+2-3s^2-12s-9=-11s-7$.
> So $g(s)=3+\dfrac{-11s-7}{s^2+4s+3}$, with $\alpha_1=4$, $\alpha_2=3$, $n_1=-11$, $n_2=-7$.
> $$A=\begin{bmatrix}-4&-3\\1&0\end{bmatrix},\quad B=\begin{bmatrix}1\\0\end{bmatrix},\quad C=\begin{bmatrix}-11&-7\end{bmatrix},\quad D=3.$$
> Check: $(sI-A)^{-1}B=\dfrac{1}{s^2+4s+3}\begin{bmatrix}s\\1\end{bmatrix}$, so $C(sI-A)^{-1}B+D=\dfrac{-11s-7}{s^2+4s+3}+3$.

> [!question]- Check (slide 102, third order): Write the controllable canonical form of $g(s)=\dfrac{4s^2+2}{2s^3+4s^2+6s+8}$. Then write the observable canonical form by duality.
> Monic denominator: $g(s)=\dfrac{2s^2+1}{s^3+2s^2+3s+4}$. Strictly proper, so $D=0$ and no division is needed.
> $\alpha_1=2$, $\alpha_2=3$, $\alpha_3=4$. Numerator $2s^2+0s+1$: $n_1=2$, $n_2=0$, $n_3=1$. Do not forget the zero coefficient.
> Controllable form:
> $$A=\begin{bmatrix}-2&-3&-4\\1&0&0\\0&1&0\end{bmatrix},\quad B=\begin{bmatrix}1\\0\\0\end{bmatrix},\quad C=\begin{bmatrix}2&0&1\end{bmatrix}.$$
> Observable form $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T})$:
> $$A_o=\begin{bmatrix}-2&1&0\\-3&0&1\\-4&0&0\end{bmatrix},\quad B_o=\begin{bmatrix}2\\0\\1\end{bmatrix},\quad C_o=\begin{bmatrix}1&0&0\end{bmatrix}.$$
> Why the dual has the same $g$: $g$ is a scalar, so $g=g^{\mathsf T}=\left(C(sI-A)^{-1}B\right)^{\mathsf T}=B^{\mathsf T}(sI-A^{\mathsf T})^{-1}C^{\mathsf T}$.

## 5. Equivalence of time-varying representations (slides 110-111)
![[ee502_eee501alllecturenotesabo_p110.jpg]]
![[ee502_eee501alllecturenotesabo_p111.jpg]]

**Notes.** This part starts on the lower half of slide 109 (embedded in [[EE502 L10 - LTV state equation solution]]). For the LTV model, put $\hat{\mathbf{x}}(t)=P(t)\mathbf{x}(t)$ with $P(t)$ nonsingular and differentiable. The product rule adds a $\dot P$ term:
$$\hat A=(PA+\dot P)P^{-1},\qquad \hat B=PB,\qquad \hat C=CP^{-1},\qquad \hat D=D.$$

**Fact 6.** $\hat X(t)=P(t)X(t)$ is a fundamental matrix of the new system, and $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$.

**Fact 7 (too powerful).** For any constant $A_0$, the choice $P(t)=e^{A_0t}X(t)^{-1}$ gives $\hat A(t)=A_0$. So an unrestricted $P(t)$ can turn any LTV system into any LTI system, and can hide growth.

**Definition (Lyapunov transformation).** $P(t)$ nonsingular, $P$ and $\dot P$ continuous, $P$ and $P^{-1}$ bounded on the interval.

> [!info] Symbols and the reason for the bounds (beyond the slides)
> - A **fundamental matrix** $X(t)$ is a nonsingular matrix solution of $\dot X=A(t)X$. The state transition matrix is $\Phi(t,t_0)=X(t)X(t_0)^{-1}$.
> - Where $\dot P$ comes from: $\dot{\hat{\mathbf{x}}}=\dot P\mathbf{x}+P\dot{\mathbf{x}}=\dot P\mathbf{x}+P(A\mathbf{x}+B\mathbf{u})=(\dot P+PA)P^{-1}\hat{\mathbf{x}}+PB\mathbf{u}$.
> - Why bounded $P$ and $P^{-1}$: from $\hat{\mathbf{x}}=P\mathbf{x}$ we get $\lVert\hat{\mathbf{x}}\rVert\le\lVert P\rVert\,\lVert\mathbf{x}\rVert$ and $\lVert\mathbf{x}\rVert\le\lVert P^{-1}\rVert\,\lVert\hat{\mathbf{x}}\rVert$. With both bounds, $\mathbf{x}$ is bounded exactly when $\hat{\mathbf{x}}$ is bounded, and $\mathbf{x}\to0$ exactly when $\hat{\mathbf{x}}\to0$. So a Lyapunov transformation cannot change the stability answer.

> [!question]- Check (slide 110): Scalar system $\dot x=2t\,x$ and $p(t)=e^{-t^2+t}$. Find $\hat a(t)$. Then check Fact 6 ii: compute $\hat\Phi(t,t_0)$ from $p(t)\Phi(t,t_0)p(t_0)^{-1}$ and compare with the solution of the new equation.
> $\dot p=(-2t+1)p$. Formula: $\hat a=(pa+\dot p)p^{-1}=2t+(-2t+1)=1$. The new system is $\dot{\hat x}=\hat x$.
> Old transition function: $\Phi(t,t_0)=e^{\int_{t_0}^{t}2\tau\,d\tau}=e^{t^2-t_0^2}$.
> Fact 6 ii: $\hat\Phi=e^{-t^2+t}\cdot e^{t^2-t_0^2}\cdot e^{t_0^2-t_0}=e^{t-t_0}$.
> Direct: $\dot{\hat x}=\hat x$ has $\hat\Phi(t,t_0)=e^{t-t_0}$. The same.
> Note: this $p$ is not a Lyapunov transformation on $[0,\infty)$, because $p^{-1}=e^{t^2-t}$ is unbounded. It makes the growth $e^{t^2}$ look like the slower growth $e^{t}$.

> [!question]- Check (slide 111): $A$ is constant with rows $(0,\ 1)$ and $(-1,\ 0)$, so $X(t)=e^{At}$ has rows $(\cos t,\ \sin t)$ and $(-\sin t,\ \cos t)$. Use the proof of Fact 7 with $A_0=0$. What is $P(t)$, what is $\hat A$, and is $P$ a Lyapunov transformation on $[0,\infty)$?
> $P(t)=e^{0\cdot t}X(t)^{-1}=X(t)^{-1}=\begin{bmatrix}\cos t&-\sin t\\ \sin t&\cos t\end{bmatrix}$ (the inverse of a rotation is the rotation by $-t$).
> By the proof, $\dot P+PA=A_0P=0$, so $\hat A=0$. Direct check: $PA=\begin{bmatrix}\sin t&\cos t\\-\cos t&\sin t\end{bmatrix}$ and $\dot P=\begin{bmatrix}-\sin t&-\cos t\\ \cos t&-\sin t\end{bmatrix}$. The sum is the zero matrix.
> Lyapunov: yes. $P$ is nonsingular ($\det P=1$), $P$ and $\dot P$ are continuous, and all entries of $P$ and $P^{-1}=X(t)$ are sines and cosines, so they are bounded.
> Meaning: the oscillator ($\mathbf{x}$ turns on a circle) and $\dot{\hat{\mathbf{x}}}=0$ ($\hat{\mathbf{x}}$ stands still) are both bounded and non-decaying. The stability answer is the same, as it must be.

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

> [!info] Reading the periodic fact (beyond the slides)
> - $X(0)^{-1}X(T)$ tells how the solutions change over one period: $X(t+T)=X(t)\,X(0)^{-1}X(T)$ (slide 113). With $X(0)=I$ it is just $X(T)$.
> - $\bar A$ is a constant matrix that produces the same change over one period: $e^{\bar AT}=X(0)^{-1}X(T)$. It may be complex, which is why the slide writes $\bar A\in C^{n\times n}$.
> - Result: $\mathbf{x}(t)=P(t)^{-1}\hat{\mathbf{x}}(t)$ with $P^{-1}$ periodic and $\dot{\hat{\mathbf{x}}}=\bar A\hat{\mathbf{x}}$. Every solution is "periodic factor times $e^{\bar At}$". Since $P$ is a Lyapunov transformation, the eigenvalues of $\bar A$ decide stability.

> [!question]- Check (slide 112, example): Change the example to $A(t)$ with rows $(0,\ 0)$ and $(e^{-t},\ 0)$, and keep $A_0=0$. Find $X(t)$ with $X(t_0)=I$ and $P(t)=X(t)^{-1}$. Is this $P$ a Lyapunov transformation on $[t_0,\infty)$?
> Equations: $\dot x_1=0$ and $\dot x_2=e^{-t}x_1$. So $x_1(t)=x_1(t_0)$ and $x_2(t)=x_2(t_0)+\left(e^{-t_0}-e^{-t}\right)x_1(t_0)$, because $\int_{t_0}^{t}e^{-\tau}d\tau=e^{-t_0}-e^{-t}$.
> $$X(t)=\begin{bmatrix}1&0\\e^{-t_0}-e^{-t}&1\end{bmatrix},\qquad P(t)=X(t)^{-1}=\begin{bmatrix}1&0\\e^{-t}-e^{-t_0}&1\end{bmatrix}.$$
> As on the slide, $\hat A=0$.
> Lyapunov: yes. The entry $e^{-t_0}-e^{-t}$ stays between $0$ and $e^{-t_0}$ for $t\ge t_0$, so $P$ and $P^{-1}$ are bounded. $\dot P$ has the entry $-e^{-t}$, which is continuous.
> Difference to the slide: there the entry $\tfrac{t^2-t_0^2}{2}$ grows without bound because $\int t\,dt$ diverges. Here $\int e^{-t}dt$ converges.

> [!question]- Check (slide 112, periodic fact): Scalar periodic system $\dot x=(-1+\cos t)\,x$, period $T=2\pi$. Find $X(t)$ with $X(0)=1$, then $\bar a$, then $P(t)$. Is $P$ bounded? Do the solutions tend to zero?
> $X(t)=e^{\int_0^t(-1+\cos\tau)d\tau}=e^{-t+\sin t}$.
> Over one period: $X(0)^{-1}X(T)=e^{-2\pi+\sin 2\pi}=e^{-2\pi}\approx0.0019$.
> $e^{\bar aT}=e^{-2\pi}$ with $T=2\pi$ gives $\bar a=-1$ (the average of $a(t)$ over one period).
> $P(t)=e^{\bar at}X(t)^{-1}=e^{-t}\cdot e^{t-\sin t}=e^{-\sin t}$. It is periodic with period $2\pi$ and stays between $e^{-1}\approx0.37$ and $e\approx2.72$. So $P$ and $P^{-1}=e^{\sin t}$ are bounded: a Lyapunov transformation.
> New system: $\dot{\hat x}=-\hat x$, so $\hat x\to0$. Then $x=e^{\sin t}\hat x\to0$ too. Check: $x(t)=e^{-t+\sin t}x(0)\to0$.

> [!question]- Check (slide 113): Find the mistake: "$A(t)$ is periodic with period $T$, so the fundamental matrix is periodic too: $X(t+T)=X(t)$." What is true instead, and why is $P(t)$ periodic anyway?
> The mistake: only the equation repeats, not the solution. Example: $\dot x=(-1+\cos t)x$ has $X(t)=e^{-t+\sin t}$, and $X(t+2\pi)=e^{-2\pi}X(t)\ne X(t)$.
> True statement: $X(t+T)=X(t)\,X(0)^{-1}X(T)$. Reason: $Y(t):=X(t+T)$ satisfies $\dot Y(t)=A(t+T)X(t+T)=A(t)Y(t)$, the same differential equation. The right side $X(t)X(0)^{-1}X(T)$ satisfies it as well (a solution times a constant matrix on the right). Both are equal to $X(T)$ at $t=0$. By uniqueness they are equal for all $t$.
> $P$ is periodic because the two factors cancel: $P(t+T)=e^{\bar At}e^{\bar AT}\left[X(t)X(0)^{-1}X(T)\right]^{-1}=e^{\bar At}\,e^{\bar AT}X(T)^{-1}X(0)\,X(t)^{-1}=e^{\bar At}X(t)^{-1}=P(t)$, since $e^{\bar AT}=X(0)^{-1}X(T)$ by the choice of $\bar A$.

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
> [!question]- 1. Apply $P=\operatorname{diag}(2,1)$ to $A$ with rows $(0,\ 1)$ and $(-2,\ -3)$, $B=(0,\ 1)^{\mathsf T}$, $C=(1,\ 0)$.
> $\hat A=PAP^{-1}=\begin{bmatrix}0&2\\-1&-3\end{bmatrix}$, $\hat B=\begin{bmatrix}0\\1\end{bmatrix}$, $\hat C=\begin{bmatrix}\tfrac12&0\end{bmatrix}$.

> [!question]- 2. Can a 2-state and a 3-state model be equivalent? Can they have the same $G(s)$?
> Not equivalent: $P$ would be $3\times 2$, not invertible. Same $G$ is possible: add a state that neither the input nor the output touches.

> [!question]- 3. Realize $g(s)=\dfrac{3s+1}{s+2}$. Is $\dfrac{s^2}{s+1}$ realizable?
> $g=3+\dfrac{-5}{s+2}$: $A=-2$, $B=1$, $C=-5$, $D=3$. $\dfrac{s^2}{s+1}$ is improper, so it has no realization.

> [!question]- 4. Controllable and observable canonical forms of $g(s)=\dfrac{s+4}{s^2+5s+6}$.
> Controllable: $A=\begin{bmatrix}-5&-6\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&4\end{bmatrix}$, $D=0$. Observable: $A_o=\begin{bmatrix}-5&1\\-6&0\end{bmatrix}$, $B_o=\begin{bmatrix}1\\4\end{bmatrix}$, $C_o=\begin{bmatrix}1&0\end{bmatrix}$.

> [!question]- 5. Is the controllable form of $g(s)=\dfrac{s+1}{s^2+3s+2}$ minimal?
> No. $s^2+3s+2=(s+1)(s+2)$, so $g=\dfrac{1}{s+2}$. In the 2-state form the eigenvector $\mathbf{v}=(-1,1)^{\mathsf T}$ of $\lambda=-1$ has $C\mathbf{v}=0$: the mode $e^{-t}$ is unobservable. One state: $A=-2$, $B=1$, $C=1$.

> [!question]- 6. Is $P(t)$ with rows $(1,\ \sin t)$ and $(0,\ 1)$ a Lyapunov transformation on $[0,\infty)$? And $P(t)=e^{-t}I$?
> First: yes. $P^{-1}=\begin{bmatrix}1&-\sin t\\0&1\end{bmatrix}$, all entries bounded, $\dot P$ continuous. Second: no, $P^{-1}=e^{t}I$ is unbounded. It would turn the unstable $\dot x=x$ into $\dot{\hat x}=0$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L10 - LTV state equation solution]]. Next: [[EE502 L12 - Stability]]
- Used later in: [[EE502 L13 - Controllability]], [[EE502 L14 - Observability]] (minimal realizations, canonical forms), [[EE502 L15 - State feedback (extra)]]
- Full step-by-step notes (PDF): [EE502_Lecture_11_Equivalence_Realization.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_11/EE502_Lecture_11_Equivalence_Realization.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_11/EE502_Lecture_11_Equivalence_Realization.pdf`
- Original slides (PDF, pp. 94-102 and 110-113): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L11 - Equivalence and realization - quiz]]

Slides not embedded: 97 (section title).
