---
course: EE 502 Linear System Theory
lesson: EE502 L11 - Equivalence and realization
type: quiz
questions: 15
---

# EE502 L11 - Equivalence and realization - quiz

Lesson note: [[EE502 L11 - Equivalence and realization]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. The model is $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$, with transfer matrix $G(s)=C(sI-A)^{-1}B+D$. A change of state $\hat{\mathbf{x}}=P\mathbf{x}$ ($P$ nonsingular) gives the equivalent model $(\hat A,\hat B,\hat C,\hat D)$.

## 1. Change of state and equivalence (slides 94-95)

### Q1 (slide 94)

$A$ has the rows $(1,\ 2)$ and $(0,\ 3)$, $B=(0,\ 1)^{\mathsf T}$, $C=(1,\ 0)$, $D=0$. The new state is $\hat{\mathbf{x}}=P\mathbf{x}$ with $P$ having the rows $(1,\ 1)$ and $(0,\ 1)$. Then $\hat B=(1,\ 1)^{\mathsf T}$. Find $\hat A$ and $\hat C$.

- A) $\hat A=\operatorname{diag}(1,\ 3)$ and $\hat C=(1,\ -1)$
- B) $\hat A$ with rows $(1,\ 4)$, $(0,\ 3)$ and $\hat C=(1,\ 1)$
- C) $\hat A$ with rows $(1,\ 4)$, $(0,\ 3)$ and $\hat C=(1,\ -1)$
- D) $\hat A=\operatorname{diag}(1,\ 3)$ and $\hat C=(1,\ 1)$

> [!success]- Answer
> **C.** From $\mathbf{x}=P^{-1}\hat{\mathbf{x}}$: $\hat A=PAP^{-1}$, $\hat C=CP^{-1}$. Here $P^{-1}$ has the rows $(1,\ -1)$ and $(0,\ 1)$.
> $PA$ has the rows $(1,\ 5)$, $(0,\ 3)$, so $PAP^{-1}$ has the rows $(1,\ 4)$, $(0,\ 3)$. $CP^{-1}=(1,\ -1)$.
> Check: both $A$ and $\hat A$ are triangular with eigenvalues $1,3$, and both models give $g(s)=\dfrac{2}{(s-1)(s-3)}$.
> - A: $\hat A=P^{-1}AP$ (the convention $\mathbf{x}=P\hat{\mathbf{x}}$). With $\hat B=PB$ and $\hat C=CP^{-1}$ this gives $g=\dfrac{-2}{(s-1)(s-3)}$, a different $g$.
> - B: $\hat C=CP$ instead of $CP^{-1}$. This gives $g=\dfrac{2s}{(s-1)(s-3)}$.
> - D: Both slips: $P^{-1}AP$ and $CP$. This gives $g=\dfrac{2(s-2)}{(s-1)(s-3)}$.

### Q2 (slide 95)

Model 1: $A_1$ with rows $(0,\ 1)$ and $(-2,\ -3)$, $B_1=(0,\ 1)^{\mathsf T}$, $C_1=(1,\ 0)$. Model 2: $A_2=\operatorname{diag}(-1,\ -2)$, $B_2=(1,\ 1)^{\mathsf T}$, $C_2=(1,\ 1)$. Both have $D=0$ and the eigenvalues $-1,-2$. Equivalent models have the same $CA^kB$ for every $k\ge 0$. Which statement is right?

- A) $C_1B_1=0$ and $C_2B_2=2$. They differ, so no $P$ can relate the two models.
- B) Both have the eigenvalues $-1$ and $-2$. That is enough, so a $P$ exists.
- C) $C_1B_1=0$ and $C_2B_2=2$ differ, but $CB$ can change under $P$, so the test decides nothing.
- D) Both transfer functions have the denominator $s^2+3s+2$, so the models are equivalent.

> [!success]- Answer
> **A.** $C_1B_1=1\cdot0+0\cdot1=0$ and $C_2B_2=1+1=2$. Equivalence would force $C_1B_1=C_2B_2$, so no $P$ exists.
> In $G$: $g_1=\dfrac{1}{s^2+3s+2}=\dfrac{0}{s}+\dfrac{1}{s^2}+\dots$ and $g_2=\dfrac{2s+3}{s^2+3s+2}=\dfrac{2}{s}-\dfrac{3}{s^2}+\dots$.
> - B: The same eigenvalues are necessary, not sufficient. The example shows two models with the same eigenvalues that are not equivalent.
> - C: $\hat C\hat B=CP^{-1}PB=CB$. Markov parameters never change under $P$.
> - D: The denominators agree, but the numerators are $1$ and $2s+3$. The transfer functions differ, so the models cannot be equivalent.

## 2. Same transfer matrix does not imply equivalence (slide 96)

### Q3 (slide 96, circuit)

Circuit 1 has no state: $y=0.5u$, so $G(s)=0.5$. Circuit 2 has one capacitor voltage $x_c$: $\dot x_c=-x_c$, $y=-0.5x_c+0.5u$. Its $G(s)$ is also $0.5$. Circuit 2 starts with $x_c(0)=4$, and the input is $u(t)=2$ for $t\ge0$. What is $y(t)$ of circuit 2, and which part of it does $G(s)=0.5$ explain?

- A) $y=1+2e^{-t}$. $G$ explains only the part $1$, the zero-state response.
- B) $y=1-2e^{-t}$. $G$ explains all of $y$, since both circuits have $G=0.5$.
- C) $y=1+2e^{-t}$. $G$ explains all of $y$, since both circuits have $G=0.5$.
- D) $y=1-2e^{-t}$. $G$ explains only the part $1$, the zero-state response.

> [!success]- Answer
> **D.** $\dot x_c=-x_c$ has no $u$, so $x_c(t)=4e^{-t}$. Then $y=-0.5\cdot4e^{-t}+0.5\cdot2=1-2e^{-t}$.
> $G$ gives only the zero-state part $0.5u=1$. The term $-2e^{-t}$ is the zero-input response from $x_c(0)$. At $t=0$ circuit 2 gives $y=-1$, circuit 1 gives $y=1$.
> - A: The sign of $-0.5x_c$ is lost. The split into zero-state and zero-input parts is right.
> - B: $y$ is right, but $G(s)$ only describes the response from $\mathbf{x}(0)=\mathbf{0}$. It cannot see $-2e^{-t}$.
> - C: Sign slip and the wrong claim about $G$.

### Q4 (slide 96, dimensions)

Model 1: $A=-2$, $B=1$, $C=1$, $D=0$. Model 2: $A=\operatorname{diag}(-2,\ 1)$, $B=(1,\ 0)^{\mathsf T}$, $C=(1,\ 1)$, $D=0$. Both have the transfer function $g(s)=\dfrac{1}{s+2}$. Are they algebraically equivalent, and what can the zero-input output ($u=0$) of model 2 do?

- A) Equivalent, since the transfer functions agree. With $x_2(0)\ne0$ the output grows like $e^{t}$.
- B) Equivalent, since the transfer functions agree. Every zero-input output decays like $e^{-2t}$.
- C) Not equivalent: $1$ state against $2$. With $x_2(0)\ne0$ the output grows like $e^{t}$.
- D) Not equivalent: $1$ state against $2$. Every zero-input output decays like $e^{-2t}$.

> [!success]- Answer
> **C.** Algebraic equivalence needs a square nonsingular $P$, so the same number of states. Here $1\ne2$.
> Model 2 with $u=0$: $x_1=e^{-2t}x_1(0)$, $x_2=e^{t}x_2(0)$, so $y=e^{-2t}x_1(0)+e^{t}x_2(0)$. The input never reaches $x_2$, so $g$ does not show the eigenvalue $+1$.
> - A: The same $G$ means zero-state equivalence only. It does not give a $P$.
> - B: Wrong twice: no $P$ exists, and the hidden mode $e^{t}$ is missed.
> - D: The verdict is right, but the pole list of $g$ ($-2$ only) is not the eigenvalue list of $A$ ($-2$ and $1$).

## 3. Realization of a proper transfer matrix (slides 98-100)

### Q5 (slide 98)

A realization $(A,B,C,D)$ of $g(s)$ means $g(s)=C(sI-A)^{-1}B+D$ with constant matrices. Which of these have a realization, and what is $D$? (a) $\dfrac{2s^2+1}{s^2+4}$, (b) $\dfrac{s^3}{s^2+1}$, (c) $\dfrac{1}{(s+1)^3}$, (d) $\dfrac{e^{-s}}{s+1}$.

- A) Only (a) and (c). $D=2$ for (a) and $D=0$ for (c).
- B) (a), (c) and (d). $D=\tfrac14$ for (a), $D=0$ for (c) and (d).
- C) (a), (c) and (d). $D=2$ for (a), $D=0$ for (c) and (d).
- D) Only (a) and (c). $D=\tfrac14$ for (a) and $D=0$ for (c).

> [!success]- Answer
> **A.** A realization exists if and only if $g$ is rational and proper. Then $D=g(\infty)$.
> (a) degrees $2$ and $2$: proper, $D=\lim_{s\to\infty}g=2$. (b) degree $3$ over $2$: improper, no realization. (c) strictly proper, $D=0$.
> (d) $e^{-s}$ is a delay, not a ratio of polynomials. No finite-dimensional realization.
> - B: Two slips: $D=g(0)=\tfrac14$ instead of $g(\infty)$, and (d) accepted because it tends to $0$.
> - C: $D$ is right, but (d) is not rational. A finite $\lim_{s\to\infty}$ is not enough.
> - D: The list is right, but $D=g(0)=\tfrac14$. $D$ is the value at $s=\infty$.

### Q6 (slide 99)

Block realization for one input ($p=1$): write the strictly proper $G$ as $N(s)/d(s)$ with $d(s)=s^2+\alpha_1s+\alpha_2$ monic and $N(s)=N_1s+N_2$. Then $A$ has the rows $(-\alpha_1,\ -\alpha_2)$ and $(1,\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $C=[N_1\ N_2]$, $D=0$. Take $G(s)$ as the column with entries $\dfrac{1}{s+1}$ and $\dfrac{1}{s+2}$. Find $A$ and $C$.

- A) $A$ with rows $(-3,\ -2)$, $(1,\ 0)$ and $C$ with rows $(1,\ 2)$, $(1,\ 1)$
- B) $A$ with rows $(3,\ 2)$, $(1,\ 0)$ and $C$ with rows $(1,\ 2)$, $(1,\ 1)$
- C) $A$ with rows $(-3,\ -2)$, $(1,\ 0)$ and $C$ with rows $(2,\ 1)$, $(1,\ 1)$
- D) $A$ with rows $(3,\ 2)$, $(1,\ 0)$ and $C$ with rows $(2,\ 1)$, $(1,\ 1)$

> [!success]- Answer
> **A.** $d(s)=(s+1)(s+2)=s^2+3s+2$, so $\alpha_1=3$, $\alpha_2=2$ and the top row of $A$ is $(-3,\ -2)$.
> $N(s)=d\,G=\begin{bmatrix}s+2\\s+1\end{bmatrix}$, so $N_1=\begin{bmatrix}1\\1\end{bmatrix}$, $N_2=\begin{bmatrix}2\\1\end{bmatrix}$ and $C=[N_1\ N_2]$ has the rows $(1,\ 2)$, $(1,\ 1)$.
> Check: $(sI-A)^{-1}B=\dfrac{1}{d}(s,\ 1)^{\mathsf T}$, and $C$ times it gives $\dfrac{s+2}{d}=\dfrac{1}{s+1}$ and $\dfrac{s+1}{d}=\dfrac{1}{s+2}$. There are $n=pr=2$ states.
> - B: The top row holds $+\alpha_i$ instead of $-\alpha_i$. Then $\det(sI-A)=s^2-3s-2$, not $d(s)$.
> - C: $N_1$ and $N_2$ swapped in the first row. Row 1 then gives $\dfrac{2s+1}{d}\ne\dfrac{1}{s+1}$.
> - D: Both slips.

### Q7 (slide 100)

$A$ has the rows $(-5,\ -4)$ and $(1,\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $C=(2,\ 3)$. So $d(s)=s^2+5s+4$. Solve $sZ=AZ+B$ for $Z=(Z_1,\ Z_2)^{\mathsf T}=(sI-A)^{-1}B$, then give $g(s)=CZ$.

- A) $Z_1=\dfrac{1}{s^2+5s+4}$, $Z_2=\dfrac{s}{s^2+5s+4}$, $g=\dfrac{3s+2}{s^2+5s+4}$
- B) $Z_1=\dfrac{s}{s^2+5s+4}$, $Z_2=\dfrac{1}{s^2+5s+4}$, $g=\dfrac{2s+3}{s^2+5s+4}$
- C) $Z_1=\dfrac{1}{s^2-5s-4}$, $Z_2=\dfrac{s}{s^2-5s-4}$, $g=\dfrac{3s+2}{s^2-5s-4}$
- D) $Z_1=\dfrac{s}{s^2-5s-4}$, $Z_2=\dfrac{1}{s^2-5s-4}$, $g=\dfrac{2s+3}{s^2-5s-4}$

> [!success]- Answer
> **B.** Row 2: $sZ_2=Z_1$, so $Z_2=Z_1/s$.
> Row 1: $sZ_1=-5Z_1-4Z_2+1$, so $\left(s+5+\tfrac4s\right)Z_1=1$ and $Z_1=\dfrac{s}{s^2+5s+4}$, $Z_2=\dfrac{1}{s^2+5s+4}$.
> $g=2Z_1+3Z_2=\dfrac{2s+3}{s^2+5s+4}$. The entries of $C$ are the numerator coefficients.
> - A: The powers of $s$ put the wrong way round. Row 2 needs $sZ_2=Z_1$, so the powers go down: $Z_k=s^{r-k}/d$.
> - C: Sign slip when moving $-5Z_1-4Z_2$ to the left, plus the order slip of A.
> - D: Only the sign slip: $\left(s-5-\tfrac4s\right)Z_1=1$. The denominator must be $\det(sI-A)=s^2+5s+4$.

## 4. Examples and the controllable canonical form (slides 101-102)

### Q8 (slide 101)

Two inputs, one output: $G(s)=\begin{bmatrix}\dfrac{s+3}{s+1}&\dfrac{2}{s+3}\end{bmatrix}$. Block realization: $D=G(\infty)$, $G_{sp}=G-D$, $d(s)=(s+1)(s+3)=s^2+4s+3$, $N(s)=d\,G_{sp}=N_1s+N_2$ with $N_1,N_2\in\mathbb{R}^{1\times2}$. Then $A$ has the block rows $(-4I_2,\ -3I_2)$ and $(I_2,\ 0)$, $B=\begin{bmatrix}I_2\\0\end{bmatrix}$, $C=[N_1\ N_2]$. Find $D$ and $C$.

- A) $D=(1,\ 0)$ and $C=(2,\ 2,\ 6,\ 2)$
- B) $D=(0,\ 0)$ and $C=(2,\ 6,\ 2,\ 2)$
- C) $D=(1,\ 0)$ and $C=(2,\ 6,\ 2,\ 2)$
- D) $D=(0,\ 0)$ and $C=(2,\ 2,\ 6,\ 2)$

> [!success]- Answer
> **A.** $\dfrac{s+3}{s+1}=1+\dfrac{2}{s+1}$, so $D=(1,\ 0)$ and $G_{sp}=\begin{bmatrix}\dfrac{2}{s+1}&\dfrac{2}{s+3}\end{bmatrix}$.
> $N(s)=\begin{bmatrix}2(s+3)&2(s+1)\end{bmatrix}=(2,\ 2)\,s+(6,\ 2)$. So $C=[N_1\ N_2]=(2,\ 2,\ 6,\ 2)$, with $n=pr=4$ states.
> Fewer states: $A=\operatorname{diag}(-1,-3)$, $B=\operatorname{diag}(2,2)$, $C=(1,\ 1)$, $D=(1,\ 0)$ also realizes $G$. The 4-state $A$ has the eigenvalues $-1,-1,-3,-3$.
> - B: Both slips of C and D: $D$ forgotten and $C$ grouped per input.
> - C: $C$ grouped per input, $(2,6)$ for input 1 and $(2,2)$ for input 2. The columns of $C$ must follow the blocks of $A$: first $N_1$, then $N_2$.
> - D: $D$ forgotten. Then $C(sI-A)^{-1}B+D$ gives $\dfrac{2}{s+1}$ in the first entry, not $\dfrac{s+3}{s+1}$.

### Q9 (slide 102, proper g)

Controllable canonical form of $g(s)=\dfrac{n(s)}{d(s)}+g(\infty)$, with $d$ monic of degree $2$ and $n(s)=n_1s+n_2$: $A$ has the rows $(-\alpha_1,\ -\alpha_2)$, $(1,\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $C=(n_1,\ n_2)$, $D=g(\infty)$. For $g(s)=\dfrac{6s^2+2s+4}{2s^2+8s+6}$, $A$ has the rows $(-4,\ -3)$, $(1,\ 0)$. Find $C$ and $D$.

- A) $C=(1,\ 2)$ and $D=0$
- B) $C=(-11,\ -7)$ and $D=0$
- C) $C=(-11,\ -7)$ and $D=3$
- D) $C=(1,\ 2)$ and $D=3$

> [!success]- Answer
> **C.** Monic form: $g=\dfrac{3s^2+s+2}{s^2+4s+3}$. Equal degrees, so $D=g(\infty)=3$.
> Remainder: $3s^2+s+2-3(s^2+4s+3)=-11s-7$. So $g=3+\dfrac{-11s-7}{s^2+4s+3}$ and $C=(-11,\ -7)$.
> Check: $(sI-A)^{-1}B=\dfrac{1}{s^2+4s+3}(s,\ 1)^{\mathsf T}$, so $C(sI-A)^{-1}B+D=\dfrac{-11s-7}{s^2+4s+3}+3=g$.
> - A: $g$ treated as strictly proper: $D=0$ and $C$ from the improper numerator $3s^2+s+2$. This gives $\dfrac{s+2}{s^2+4s+3}$.
> - B: The long division is right, but $D$ is forgotten. The result is $g-3$.
> - D: $D$ is right, but $C$ is read from $3s^2+s+2$ instead of the remainder $-11s-7$.

### Q10 (slide 102, third order)

$g(s)=\dfrac{4s^2+2}{2s^3+4s^2+6s+8}$. Its controllable canonical form has $A$ with the top row $(-\alpha_1,\ -\alpha_2,\ -\alpha_3)$ and ones below the diagonal, $B=(1,\ 0,\ 0)^{\mathsf T}$, $C=(n_1,\ n_2,\ n_3)$, where $d$ is monic and $n(s)=n_1s^2+n_2s+n_3$. The observable canonical form is the dual $(A_o,B_o,C_o)=(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T})$. So $C_o=(1,\ 0,\ 0)$ and $A_o$ has the second column $(1,\ 0,\ 0)^{\mathsf T}$ and the third column $(0,\ 1,\ 0)^{\mathsf T}$. Find the first column of $A_o$ and $B_o$.

- A) First column $(-4,\ -3,\ -2)^{\mathsf T}$ and $B_o=(4,\ 0,\ 2)^{\mathsf T}$
- B) First column $(-2,\ -3,\ -4)^{\mathsf T}$ and $B_o=(2,\ 0,\ 1)^{\mathsf T}$
- C) First column $(-2,\ -3,\ -4)^{\mathsf T}$ and $B_o=(4,\ 0,\ 2)^{\mathsf T}$
- D) First column $(-4,\ -3,\ -2)^{\mathsf T}$ and $B_o=(2,\ 0,\ 1)^{\mathsf T}$

> [!success]- Answer
> **B.** Divide top and bottom by $2$: $g=\dfrac{2s^2+0s+1}{s^3+2s^2+3s+4}$. Strictly proper, $D=0$.
> $\alpha=(2,\ 3,\ 4)$ and $n=(2,\ 0,\ 1)$. The top row of $A$ is $(-2,\ -3,\ -4)$, so the first column of $A^{\mathsf T}$ is $(-2,\ -3,\ -4)^{\mathsf T}$, and $B_o=C^{\mathsf T}=(2,\ 0,\ 1)^{\mathsf T}$.
> Check: $C_o(sI-A_o)^{-1}B_o=g$, since a scalar equals its transpose.
> - A: Both slips of C and D: coefficients reversed and numerator not divided by $2$.
> - C: The denominator is made monic, but the numerator is not divided by $2$. This gives $2g$.
> - D: The $\alpha_i$ in the wrong order ($\alpha_3$ first). Then $\det(sI-A_o)\ne s^3+2s^2+3s+4$.

## 5. Equivalence of time-varying representations (slides 110-111)

### Q11 (slide 110)

For $\hat{\mathbf{x}}=P(t)\mathbf{x}$ the new model has $\hat A=(PA+\dot P)P^{-1}$ and $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$. Take the scalar system $\dot x=2t\,x$ and $p(t)=e^{-t^2+t}$. Find $\hat a(t)$ and $\hat\Phi(t,t_0)$.

- A) $\hat a(t)=2t$ and $\hat\Phi(t,t_0)=e^{t^2-t_0^2}$
- B) $\hat a(t)=1$ and $\hat\Phi(t,t_0)=e^{t^2-t_0^2}$
- C) $\hat a(t)=2t$ and $\hat\Phi(t,t_0)=e^{t-t_0}$
- D) $\hat a(t)=1$ and $\hat\Phi(t,t_0)=e^{t-t_0}$

> [!success]- Answer
> **D.** $\dot p=(-2t+1)p$, so $\hat a=(pa+\dot p)p^{-1}=2t-2t+1=1$.
> Old: $\Phi(t,t_0)=e^{t^2-t_0^2}$. Fact: $\hat\Phi=e^{-t^2+t}\,e^{t^2-t_0^2}\,e^{t_0^2-t_0}=e^{t-t_0}$.
> Direct check: $\dot{\hat x}=\hat x$ has $\hat\Phi=e^{t-t_0}$. The same.
> - A: $\dot P$ forgotten: $\hat a=pap^{-1}=a$. The new system then looks like the old one.
> - B: $\hat a$ is right, but $\hat\Phi$ is taken equal to $\Phi$. The transition matrix changes with $P(t)$.
> - C: $\hat\Phi$ is right, but $\dot P$ is forgotten in $\hat a$. Then $\hat a=2t$ does not fit $\hat\Phi=e^{t-t_0}$.

### Q12 (slide 111)

$A$ is constant with rows $(0,\ 1)$ and $(-1,\ 0)$, so $X(t)=e^{At}$ has the rows $(\cos t,\ \sin t)$ and $(-\sin t,\ \cos t)$. Fact 7 with $A_0=0$ uses $P(t)=e^{A_0t}X(t)^{-1}$, and $\hat A=(PA+\dot P)P^{-1}$. A Lyapunov transformation needs $P$ nonsingular, $P$ and $\dot P$ continuous, and $P$, $P^{-1}$ bounded. Find $P$ and $\hat A$, and decide if $P$ is a Lyapunov transformation on $[0,\infty)$.

- A) $P$ with rows $(\cos t,\ \sin t)$, $(-\sin t,\ \cos t)$; $\hat A$ with rows $(0,\ 2)$, $(-2,\ 0)$; Lyapunov: yes.
- B) $P$ with rows $(\cos t,\ -\sin t)$, $(\sin t,\ \cos t)$; $\hat A=0$; Lyapunov: yes.
- C) $P$ with rows $(\cos t,\ -\sin t)$, $(\sin t,\ \cos t)$; $\hat A=0$; Lyapunov: no, $P(t)$ has no limit.
- D) $P$ with rows $(\cos t,\ \sin t)$, $(-\sin t,\ \cos t)$; $\hat A$ with rows $(0,\ 2)$, $(-2,\ 0)$; Lyapunov: no, $P(t)$ has no limit.

> [!success]- Answer
> **B.** $P=X(t)^{-1}$, the rotation by $-t$: rows $(\cos t,\ -\sin t)$, $(\sin t,\ \cos t)$.
> $PA$ has the rows $(\sin t,\ \cos t)$, $(-\cos t,\ \sin t)$, and $\dot P$ has the rows $(-\sin t,\ -\cos t)$, $(\cos t,\ -\sin t)$. The sum is $0$, so $\hat A=0$.
> $\det P=1$, and all entries of $P$ and $P^{-1}=X(t)$ are sines and cosines: bounded. So $P$ is a Lyapunov transformation.
> - A: $P=X(t)$ instead of $X(t)^{-1}$. Then $\hat A=2A$, not $A_0=0$.
> - C: The definition asks for bounded $P$ and $P^{-1}$, not for a limit as $t\to\infty$.
> - D: Both slips.

## 6. Not every transformation is Lyapunov; periodic systems (slides 112-113)

### Q13 (slide 112, example)

$A(t)$ has the rows $(0,\ 0)$ and $(e^{-t},\ 0)$. Let $X(t)$ be the fundamental matrix with $X(t_0)=I$ (it solves $\dot X=A(t)X$), and $P(t)=X(t)^{-1}$. Then $P$ has the rows $(1,\ 0)$ and $(q(t),\ 1)$. Find $q(t)$ and decide if $P$ is a Lyapunov transformation on $[t_0,\infty)$ ($P$, $\dot P$ continuous, $P$ and $P^{-1}$ bounded).

- A) $q(t)=e^{-t_0}-e^{-t}$. Yes: $P$ and $P^{-1}$ are bounded on $[t_0,\infty)$.
- B) $q(t)=e^{-t}-e^{-t_0}$. Yes: $P$ and $P^{-1}$ are bounded on $[t_0,\infty)$.
- C) $q(t)=e^{-t}-e^{-t_0}$. No: as on slide 112, $X(t)^{-1}$ is unbounded.
- D) $q(t)=e^{-t_0}-e^{-t}$. No: as on slide 112, $X(t)^{-1}$ is unbounded.

> [!success]- Answer
> **B.** $\dot x_1=0$ and $\dot x_2=e^{-t}x_1$ give $x_2(t)=x_2(t_0)+\left(e^{-t_0}-e^{-t}\right)x_1(t_0)$.
> So $X(t)$ has the rows $(1,\ 0)$, $(e^{-t_0}-e^{-t},\ 1)$, and the inverse flips the sign of that entry: $q(t)=e^{-t}-e^{-t_0}$.
> For $t\ge t_0$ the entry stays between $-e^{-t_0}$ and $0$, so $P$ and $P^{-1}$ are bounded. $\dot P$ has the entry $-e^{-t}$, continuous. Lyapunov: yes.
> - A: $q$ is the entry of $X(t)$, not of $X(t)^{-1}$. The sign is not flipped.
> - C: On slide 112 the entry is $\tfrac{t_0^2-t^2}{2}$, because $\int t\,dt$ diverges. Here $\int e^{-t}dt$ converges.
> - D: Both slips.

### Q14 (slide 112, periodic fact)

Scalar periodic system $\dot x=(-1+\cos t)\,x$ with period $T=2\pi$, and $X(t)=e^{-t+\sin t}$ (so $X(0)=1$). Floquet: choose $\bar a$ with $e^{\bar aT}=X(0)^{-1}X(T)$ and put $P(t)=e^{\bar at}X(t)^{-1}$. Find $\bar a$, decide if $P$ and $P^{-1}$ are bounded, and decide if all solutions tend to $0$.

- A) $\bar a=-2\pi$. $P^{-1}$ is unbounded. All solutions tend to $0$.
- B) $\bar a=-1$. $P$ and $P^{-1}$ are bounded. Not all tend to $0$, since $a(0)=0$.
- C) $\bar a=-2\pi$. $P^{-1}$ is unbounded. Not all tend to $0$, since $a(0)=0$.
- D) $\bar a=-1$. $P$ and $P^{-1}$ are bounded. All solutions tend to $0$.

> [!success]- Answer
> **D.** $X(0)^{-1}X(2\pi)=e^{-2\pi+\sin2\pi}=e^{-2\pi}$. From $e^{2\pi\bar a}=e^{-2\pi}$: $\bar a=-1$.
> $P(t)=e^{-t}\,e^{t-\sin t}=e^{-\sin t}$, periodic, between $e^{-1}$ and $e$. $P^{-1}=e^{\sin t}$ is bounded too.
> New system $\dot{\hat x}=-\hat x$, so $\hat x\to0$ and $x=e^{\sin t}\hat x\to0$. Direct: $x(t)=e^{-t+\sin t}x(0)\to0$.
> - A: $\bar aT=-2\pi$ is not divided by $T$. Then $P=e^{(1-2\pi)t-\sin t}$ and $P^{-1}$ grows without bound.
> - B: Stability is not decided by the frozen value $a(t)$. $a(0)=0$ at single instants does not stop the decay.
> - C: Both slips.

### Q15 (slide 113)

A student says: "$A(t)$ is periodic with period $T$, so the fundamental matrix is periodic: $X(t+T)=X(t)$." Which formula holds for every fundamental matrix $X$ of a $T$-periodic $A(t)$?

- A) $X(t+T)=X(0)^{-1}X(T)\,X(t)$
- B) $X(t+T)=X(t)\,X(T)^{-1}X(0)$
- C) $X(t+T)=X(t)\,X(0)^{-1}X(T)$
- D) $X(t+T)=X(t)$, the student is right

> [!success]- Answer
> **C.** $Y(t):=X(t+T)$ solves $\dot Y=A(t+T)Y=A(t)Y$. So does $X(t)M$ for the constant $M=X(0)^{-1}X(T)$.
> Both equal $X(T)$ at $t=0$. By uniqueness they are equal for all $t$.
> This is why $P(t)=e^{\bar At}X(t)^{-1}$ is periodic: $e^{\bar AT}=X(0)^{-1}X(T)$ cancels the factor $M$.
> - A: The constant factor is on the left. $MX(t)$ does not solve $\dot Y=A(t)Y$ in general, because $A(t)M\ne MA(t)$.
> - B: The inverse of the right factor. At $t=0$ it gives $X(0)X(T)^{-1}X(0)\ne X(T)$. For $X(t)=e^{-t+\sin t}$ it would give growth $e^{2\pi}$ per period.
> - D: Only the equation repeats, not the solution. $X(t)=e^{-t+\sin t}$ for $\dot x=(-1+\cos t)x$ has $X(t+2\pi)=e^{-2\pi}X(t)$.
