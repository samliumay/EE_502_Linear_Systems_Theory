---
course: EE 502 Linear System Theory
lesson: EE502 L10 - LTV state equation solution
type: quiz
questions: 13
---

# EE502 L10 - LTV state equation solution - quiz

Lesson note: [[EE502 L10 - LTV state equation solution]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. The system is $\dot{\mathbf{x}}=A(t)\mathbf{x}+B(t)\mathbf{u}$, $\mathbf{y}=C(t)\mathbf{x}+D(t)\mathbf{u}$. $\Phi(t,t_0)$ is the state transition matrix: the unique solution of $\partial_t\Phi(t,t_0)=A(t)\Phi(t,t_0)$ with $\Phi(t_0,t_0)=I$. It maps the state at $t_0$ to the state at $t$ when $\mathbf{u}\equiv\mathbf{0}$.

## 1. The LTV equations, existence and uniqueness (slide 104)

### Q1 (slide 104, Fact 1)

Fact 1: if the entries of $A(t)$ and $\mathbf{v}(t)$ are piecewise continuous on an interval (finitely many finite jumps), then $\dot{\mathbf{x}}=A(t)\mathbf{x}+\mathbf{v}(t)$ has exactly one solution on that interval for each initial value. Take $\dot x=\tfrac{1}{t-1}x$ on $[0,2]$ with $x(0)=1$. The function $x=1-t$ on $[0,1]$, followed by $x=c\,(t-1)$ on $[1,2]$, satisfies the equation at every $t\ne 1$, for every constant $c$. Does Fact 1 apply, and is the solution unique?

- A) No. $a(t)=\tfrac{1}{t-1}$ is unbounded at $t=1$. Past $t=1$ the solution is not unique: every $c$ works.
- B) Yes. $a(t)$ has only one bad point, $t=1$. So $x=1-t$ on all of $[0,2]$ is the only solution.
- C) No. $a(t)=\tfrac{1}{t-1}$ is unbounded at $t=1$. The solution is still unique: $x(1)=0$ forces $x\equiv 0$ after $t=1$.
- D) Yes. $a(t)$ has only one bad point, $t=1$. But past $t=1$ the solution is not unique: every $c$ works.

> [!success]- Answer
> **A.** "Piecewise continuous" allows only finite jumps. $\tfrac{1}{t-1}\to\infty$ at $t=1$, so Fact 1 does not apply on $[0,2]$.
> On $(1,2]$: $x=c(t-1)$ gives $\dot x=c$ and $\tfrac{x}{t-1}=c$, equal for every $c$. Both pieces are $0$ at $t=1$, so the function is continuous.
> So the continuation past $t=1$ is really not unique. (On $[0,1)$ the coefficient is continuous and $1-t$ is unique there.)
> - B: An infinite jump is not allowed in "piecewise continuous". Also $1-t$ is not the only solution: $c=-1$ gives it, but every other $c$ works too.
> - C: The uniqueness argument needs Fact 1 across $t=1$, which does not hold. The check above shows that $c(t-1)$ with $c\ne 0$ is a solution with $x(1)=0$.
> - D: The uniqueness part is right, but Fact 1 does not apply. Fact 1 would even forbid the non-uniqueness.

### Q2 (slide 104, scalar case)

Take the scalar equation $\dot x=(\cos t)\,x$ with state transition $\Phi(t,\tau)$. Compute $\Phi(\pi/2,\,0)$ and $\Phi(\pi,\,\pi/2)$.

- A) $\Phi(\pi/2,0)=e$ and $\Phi(\pi,\pi/2)=e$
- B) $\Phi(\pi/2,0)=e^{-1}$ and $\Phi(\pi,\pi/2)=e$
- C) $\Phi(\pi/2,0)=e$ and $\Phi(\pi,\pi/2)=e^{-1}$
- D) $\Phi(\pi/2,0)=e^{-1}$ and $\Phi(\pi,\pi/2)=e^{-1}$

> [!success]- Answer
> **C.** Scalars commute, so $\Phi(t,\tau)=e^{\int_\tau^t\cos\sigma\,d\sigma}=e^{\sin t-\sin\tau}$.
> $\Phi(\pi/2,0)=e^{1-0}=e$. $\Phi(\pi,\pi/2)=e^{0-1}=e^{-1}$.
> Check: $\partial_t e^{\sin t-\sin\tau}=\cos t\,e^{\sin t-\sin\tau}$ and $\Phi(\tau,\tau)=1$.
> Both intervals have length $\pi/2$, but the results differ: $\Phi$ is not a function of $t-\tau$ alone.
> - A: $\Phi$ taken as $e^{\sin(t-\tau)}$, a function of $t-\tau$ as in the LTI case. Both intervals then give $e^{\sin(\pi/2)}=e$.
> - B: $\Phi(\tau,t)$ computed instead of $\Phi(t,\tau)$: $e^{\sin\tau-\sin t}$.
> - D: Wrong antiderivative: $e^{\cos t-\cos\tau}$ gives $e^{0-1}$ and $e^{-1-0}$.

## 2. Fundamental matrix (slide 105)

### Q3 (slide 105, fundamental matrix)

$A(t)$ has the rows $(2t,\ 0)$ and $(1,\ 2t)$. The vectors $\mathbf{x}_1(t)=e^{t^2}(1,\ t)^{\mathsf T}$ and $\mathbf{x}_2(t)=e^{t^2}(0,\ 1)^{\mathsf T}$ solve $\dot{\mathbf{x}}=A(t)\mathbf{x}$. What is $\det X(t)$ for $X(t)=[\mathbf{x}_1\ \mathbf{x}_2]$?

- A) $\det X(t)=e^{2t^2}$
- B) $\det X(t)=e^{t^2}$
- C) $\det X(t)=2e^{t^2}$
- D) $\det X(t)=e^{4t^2}$

> [!success]- Answer
> **A.** $X(t)$ has the rows $(e^{t^2},\ 0)$ and $(te^{t^2},\ e^{t^2})$. It is triangular: $\det X=e^{t^2}\cdot e^{t^2}=e^{2t^2}$.
> Trace formula: $\det X(t)=\det X(0)\,e^{\int_0^t\operatorname{tr}A}$ with $X(0)=I$, $\operatorname{tr}A=4t$, $\int_0^t4\tau\,d\tau=2t^2$. The same.
> It is never zero, and $X(0)=I$ is nonsingular, so $X$ is a fundamental matrix.
> - B: Only one diagonal entry of $A$ used in the trace ($\operatorname{tr}A=2t$), or only one diagonal entry of $X$.
> - C: The diagonal entries of $X$ added, not multiplied.
> - D: $\int_0^t4\tau\,d\tau$ taken as $4t^2$: the factor $\tfrac12$ of the integral was lost.

### Q4 (slide 105, Fact 2)

$X(t)$ has the rows $(1,\ t)$ and $(0,\ t)$. It is singular at $t=0$ and nonsingular at $t=1$. Can $X(t)$ be a fundamental matrix of some $\dot{\mathbf{x}}=A(t)\mathbf{x}$ with $A(t)$ piecewise continuous on $[0,1]$?

- A) Yes. $A(t)=\dot X(t)X(t)^{-1}$ exists for every $t>0$, and that is enough.
- B) Yes. A matrix of solutions only has to be nonsingular at one time, here $t=1$.
- C) No. A fundamental matrix has a constant determinant, but $\det X(t)=t$ changes.
- D) No. $X(t)(0,\ 1)^{\mathsf T}$ would be a solution that is zero at $t=0$ but not at $t=1$.

> [!success]- Answer
> **D.** $\det X(t)=t$, so $X(0)\boldsymbol{\alpha}=\mathbf{0}$ for $\boldsymbol{\alpha}=(0,\ 1)^{\mathsf T}$. Then $\mathbf{x}(t)=X(t)\boldsymbol{\alpha}=(t,\ t)^{\mathsf T}$ is zero at $t=0$.
> The zero function is also a solution with that value. By uniqueness (Fact 1) $\mathbf{x}\equiv\mathbf{0}$. But $\mathbf{x}(1)=(1,\ 1)^{\mathsf T}$. Contradiction.
> Rule: a matrix of solutions is nonsingular at every time or at no time.
> - A: $\dot XX^{-1}$ has the rows $(0,\ 1/t)$ and $(0,\ 1/t)$. It is unbounded at $t=0$, so it is not piecewise continuous on $[0,1]$.
> - B: Nonsingular at one time means nonsingular at every time (Fact 2). Singular at $t=0$ is therefore impossible.
> - C: The conclusion is right, the reason is false. $\det X(t)=\det X(t_0)e^{\int\operatorname{tr}A}$ changes with $t$ whenever $\operatorname{tr}A\ne 0$.

## 3. State transition matrix (slide 106)

### Q5 (slide 106, any fundamental matrix)

$X(t)$ is a fundamental matrix of $\dot{\mathbf{x}}=A(t)\mathbf{x}$ and $\Phi(t,t_0)=X(t)X(t_0)^{-1}$. $K$ is a constant nonsingular matrix and $\tilde X$ denotes the new matrix. Which statement is true in general?

- A) $\tilde X=KX(t)$ is a fundamental matrix, and $\tilde X(t)\tilde X(t_0)^{-1}$ equals $\Phi(t,t_0)$.
- B) $\tilde X=X(t)K$ is a fundamental matrix, and $\tilde X(t)\tilde X(t_0)^{-1}$ equals $\Phi(t,t_0)$.
- C) $\tilde X=X(t)K$ is a fundamental matrix, and $\tilde X(t)\tilde X(t_0)^{-1}$ equals $X(t)KX(t_0)^{-1}K^{-1}$.
- D) $\tilde X=KX(t)$ is a fundamental matrix, and $\tilde X(t)\tilde X(t_0)^{-1}$ equals $K\Phi(t,t_0)K^{-1}$.

> [!success]- Answer
> **B.** $\dot{\tilde X}=\dot XK=A(t)XK=A(t)\tilde X$, and $\tilde X(t_0)=X(t_0)K$ is nonsingular. So $XK$ is a fundamental matrix.
> $\tilde X(t)\tilde X(t_0)^{-1}=X(t)K\,K^{-1}X(t_0)^{-1}=X(t)X(t_0)^{-1}=\Phi(t,t_0)$.
> So $\Phi$ does not depend on the chosen initial vectors.
> - A: $\tfrac{d}{dt}(KX)=KA(t)X$, which is not $A(t)KX$ unless $K$ commutes with $A(t)$. So $KX$ is in general not a solution.
> - C: Inverse of a product in the wrong order: $(X(t_0)K)^{-1}=K^{-1}X(t_0)^{-1}$, not $X(t_0)^{-1}K^{-1}$.
> - D: The algebra $KX(t)\bigl(KX(t_0)\bigr)^{-1}=K\Phi K^{-1}$ is right, but $KX$ is in general not a fundamental matrix (see A).

### Q6 (slide 106, triangular)

$A(t)$ has the rows $(-1,\ 0)$ and $(e^{-t},\ 0)$. Find $\Phi(t,t_0)$ by solving the scalar equations one after another.

- A) Rows $\bigl(e^{t-t_0},\ 0\bigr)$ and $\bigl(\tfrac12(e^{-t}-e^{t-2t_0}),\ 1\bigr)$
- B) Rows $\bigl(e^{-(t-t_0)},\ 0\bigr)$ and $\bigl(\tfrac12(e^{t_0-2t}-e^{-t_0}),\ 1\bigr)$
- C) Rows $\bigl(e^{t-t_0},\ 0\bigr)$ and $\bigl((t-t_0)\,e^{-t_0},\ 1\bigr)$
- D) Rows $\bigl(e^{-(t-t_0)},\ 0\bigr)$ and $\bigl(\tfrac12(e^{-t_0}-e^{t_0-2t}),\ 1\bigr)$

> [!success]- Answer
> **D.** $\dot x_1=-x_1$ gives $x_1(t)=e^{-(t-t_0)}x_1(t_0)$.
> $\dot x_2=e^{-t}x_1=e^{t_0-2t}x_1(t_0)$. Integrate from $t_0$ to $t$: $x_2(t)=x_2(t_0)+e^{t_0}\cdot\tfrac12\bigl(e^{-2t_0}-e^{-2t}\bigr)x_1(t_0)$.
> So the entry $(2,1)$ is $\tfrac12(e^{-t_0}-e^{t_0-2t})$, and the second column is $(0,\ 1)^{\mathsf T}$.
> Check: entry $(2,1)$ is $0$ at $t=t_0$, so $\Phi(t_0,t_0)=I$. Its $t$-derivative is $e^{t_0-2t}=e^{-t}\cdot e^{-(t-t_0)}$, row 2 of $A$ times column 1 of $\Phi$. So $\partial_t\Phi=A(t)\Phi$.
> - A: This is $\Phi(t_0,t)$, the inverse: the arguments $t$ and $t_0$ were swapped.
> - B: Sign slip in $\int_{t_0}^{t}e^{-2\sigma}d\sigma$ (taken as $+\tfrac12e^{-2\sigma}$ at the limits). $\partial_t\Phi=A\Phi$ fails.
> - C: Wrong sign in the first equation, $x_1=e^{t-t_0}x_1(t_0)$. Then $\dot x_2=e^{-t_0}x_1(t_0)$ is constant, which gives $(t-t_0)e^{-t_0}$.

## 4. Properties and the solution formula (slide 107)

### Q7 (slide 107, properties)

A system has $\Phi(t,t_0)=e^{t^2-t_0^2}\,T(t-t_0)$, where $T(d)$ has the rows $(1,\ 0)$ and $(d,\ 1)$. What is $\Phi(2,0)^{-1}$?

- A) $e^{4}$ times the matrix with the rows $(1,\ 0)$ and $(-2,\ 1)$
- B) $e^{-4}$ times the matrix with the rows $(1,\ 0)$ and $(2,\ 1)$
- C) $e^{4}$ times the matrix with the rows $(1,\ 2)$ and $(0,\ 1)$
- D) $e^{-4}$ times the matrix with the rows $(1,\ 0)$ and $(-2,\ 1)$

> [!success]- Answer
> **D.** Inversion property: $\Phi(2,0)^{-1}=\Phi(0,2)=e^{0-4}\,T(0-2)=e^{-4}T(-2)$.
> Check: $\Phi(2,0)=e^{4}T(2)$, and $T(2)T(-2)$ has the rows $(1,\ 0)$ and $(2-2,\ 1)$, so it is $I$. With $e^{4}e^{-4}=1$ the product is $I$.
> Product property, for comparison: $\Phi(2,1)\Phi(1,0)=e^{3}T(1)\cdot e^{1}T(1)=e^{4}T(2)=\Phi(2,0)$.
> - A: Only the matrix part was inverted. The scalar $e^{4}$ must become $e^{-4}$.
> - B: Only the scalar was inverted. $T(2)^{-1}=T(-2)$, not $T(2)$.
> - C: The transpose $\Phi(2,0)^{\mathsf T}$. The inverse of $\Phi$ is "swap the arguments", not the transpose.

### Q8 (slide 107, solution formula)

$A(t)$ has the rows $(-1,\ 0)$ and $(e^{-t},\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $t_0=0$, $\mathbf{x}(0)=\mathbf{0}$, $u(t)=1$ for $t\ge 0$. Use $\mathbf{x}(t)=\Phi(t,0)\mathbf{x}(0)+\int_0^t\Phi(t,\tau)B\,u(\tau)\,d\tau$. What is the second state $x_2(t)$?

- A) $x_2(t)=\tfrac12\bigl(1-e^{-2t}\bigr)$
- B) $x_2(t)=\tfrac12-e^{-t}+\tfrac12e^{-2t}$
- C) $x_2(t)=\tfrac12t\bigl(1-e^{-2t}\bigr)$
- D) $x_2(t)=\tfrac14(1+2t)e^{-t}-\tfrac14e^{t}$

> [!success]- Answer
> **B.** $\Phi(t,\tau)B$ is the first column of $\Phi(t,\tau)$; its second entry is $\tfrac12(e^{-\tau}-e^{\tau-2t})$.
> $x_2(t)=\tfrac12\int_0^t\bigl(e^{-\tau}-e^{\tau-2t}\bigr)d\tau=\tfrac12\bigl[(1-e^{-t})-e^{-2t}(e^{t}-1)\bigr]=\tfrac12-e^{-t}+\tfrac12e^{-2t}$.
> Check: $x_1=1-e^{-t}$ and $\dot x_2=e^{-t}-e^{-2t}=e^{-t}x_1$. Also $x_2(0)=\tfrac12-1+\tfrac12=0$.
> - A: The minus sign in front of the second integral was lost: $\tfrac12\bigl[(1-e^{-t})+(e^{-t}-e^{-2t})\bigr]$.
> - C: $\Phi(t,\tau)$ replaced by $\Phi(t,0)$ and taken out of the integral: $\Phi(t,0)B\cdot t$.
> - D: $\Phi(\tau,t)$ used instead of $\Phi(t,\tau)$: $\tfrac12\int_0^t\bigl(e^{-t}-e^{t-2\tau}\bigr)d\tau$. It is negative for large $t$ although $\dot x_2=e^{-t}x_1>0$.

### Q9 (slide 107, impulse response)

$A(t)$ has the rows $(-1,\ 0)$ and $(e^{-t},\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $C=(0,\ 1)$, $D=0$. The impulse response is $G(t,\tau)=C\,\Phi(t,\tau)B$ for $t\ge\tau$. What is $G(2,1)$, rounded to three decimals?

- A) $G(2,1)\approx 0.432$
- B) $G(2,1)\approx 0.368$
- C) $G(2,1)\approx 0.159$
- D) $G(2,1)\approx 0.147$

> [!success]- Answer
> **C.** $C\Phi B$ is the entry $(2,1)$ of $\Phi(t,\tau)$: $G(t,\tau)=\tfrac12\bigl(e^{-\tau}-e^{\tau-2t}\bigr)$.
> $G(2,1)=\tfrac12(e^{-1}-e^{-3})\approx 0.159$. For comparison $G(1,0)=\tfrac12(1-e^{-2})\approx 0.432$.
> Both are read $1$ time unit after the impulse, but they differ. So $G$ is not a function of $t-\tau$ alone, and there is no transfer function of the usual kind.
> - A: The LTI habit $G(t,\tau)=H(t-\tau)$: $G(2,1)$ taken equal to $G(1,0)$.
> - B: The entry $(1,1)$ of $\Phi$ read instead of $(2,1)$: $e^{-(2-1)}=e^{-1}$.
> - D: $e^{\int_\tau^tA}$ used as $\Phi$, but $A(t)$ does not commute with its integral: $(e^{-1}-e^{-2})(1-e^{-1})$.

## 5. Computing the state transition matrix (slides 108-109)

### Q10 (slide 108, commuting case)

$A(t)$ has the rows $(0,\ t)$ and $(-t,\ 0)$. Find $\Phi(t,t_0)$.

- A) Rows $(\cos\theta,\ -\sin\theta)$ and $(\sin\theta,\ \cos\theta)$ with $\theta=\tfrac12(t^2-t_0^2)$
- B) Rows $(\cos\theta,\ \sin\theta)$ and $(-\sin\theta,\ \cos\theta)$ with $\theta=\tfrac12(t-t_0)^2$
- C) Rows $(\cos\theta,\ \sin\theta)$ and $(-\sin\theta,\ \cos\theta)$ with $\theta=\tfrac12(t^2-t_0^2)$
- D) Rows $(\cos\theta,\ -\sin\theta)$ and $(\sin\theta,\ \cos\theta)$ with $\theta=\tfrac12(t-t_0)^2$

> [!success]- Answer
> **C.** $A(t)=tJ$ with $J$ with the rows $(0,\ 1)$ and $(-1,\ 0)$. Then $M=\int_{t_0}^tA=\theta J$, $\theta=\tfrac12(t^2-t_0^2)$.
> $A(t)M=t\theta J^2=MA(t)$: they commute, so $\Phi=e^{M}$. With $J^2=-I$: $e^{\theta J}=\cos\theta\,I+\sin\theta\,J$.
> Check: $\Phi(t_0,t_0)=I$. With $\dot\theta=t$, $\partial_t\Phi$ has the rows $t(-\sin\theta,\ \cos\theta)$ and $t(-\cos\theta,\ -\sin\theta)$, the same as $A(t)\Phi$.
> - A: This is $\Phi(t_0,t)$: swapping the arguments changes $\theta$ to $-\theta$.
> - B: $\Phi(t,t_0)$ taken as $\Phi(t-t_0,0)$, as in the LTI case. Then $\partial_t\Phi=(t-t_0)J\Phi\ne A(t)\Phi$.
> - D: Both slips: arguments swapped and $\theta$ taken as a function of $t-t_0$.

### Q11 (slide 108, not commuting)

$A(t)$ has the rows $(-1,\ 0)$ and $(e^{-t},\ 0)$, $t_0=0$, and $M=\int_0^tA(\tau)\,d\tau$. Do $A(t)$ and $M$ commute, and what is the entry $(2,1)$ of $e^{M}$ at $t=1$?

- A) They do not commute. The entry $(2,1)$ of $e^{M}$ at $t=1$ is about $0.400$.
- B) They commute. The entry $(2,1)$ of $e^{M}$ at $t=1$ is about $0.400$.
- C) They do not commute. The entry $(2,1)$ of $e^{M}$ at $t=1$ is about $0.632$.
- D) They commute. The entry $(2,1)$ of $e^{M}$ at $t=1$ is about $0.632$.

> [!success]- Answer
> **A.** $M$ has the rows $(-t,\ 0)$ and $(1-e^{-t},\ 0)$.
> $A(t)M$ has the rows $(t,\ 0)$ and $(-te^{-t},\ 0)$. $MA(t)$ has the rows $(t,\ 0)$ and $(-(1-e^{-t}),\ 0)$. They differ for $t\ne 0$.
> $M^2=-tM$, so $e^{M}=I+\tfrac{1-e^{-t}}{t}M$. Entry $(2,1)$: $\tfrac{(1-e^{-t})^2}{t}$, at $t=1$ it is $(1-e^{-1})^2\approx 0.400$.
> The true value is $\Phi_{21}(1,0)=\tfrac12(1-e^{-2})\approx 0.432$. So $e^{\int A}$ is not $\Phi$ here.
> - B: The value is right, but the entries $(2,1)$ of $AM$ and $MA$ are $-te^{-t}$ and $-(1-e^{-t})$, which are not equal.
> - C: $e^{M}$ cut after $I+M$: the entry $(2,1)$ of $M$ is $1-e^{-1}\approx 0.632$. The terms $M^k/k!$ are not zero here.
> - D: Both slips: wrong commutation test and the series cut after $I+M$.

### Q12 (slide 109, example)

$A(t)$ has the rows $(1,\ t)$ and $(0,\ 1)$. $N$ is the matrix with the rows $(0,\ 1)$ and $(0,\ 0)$. Find $\Phi(t,t_0)$.

- A) $\Phi(t,t_0)=I+\tfrac12(t^2-t_0^2)\,N$
- B) $\Phi(t,t_0)=e^{t-t_0}\bigl(I+\tfrac12(t^2-t_0^2)\,N\bigr)$
- C) $\Phi(t,t_0)=e^{t-t_0}\bigl(I+t(t-t_0)\,N\bigr)$
- D) $\Phi(t,t_0)=I+t(t-t_0)\,N$

> [!success]- Answer
> **B.** $A(t)=I+tN$ with $N^2=0$. $M=\int_{t_0}^tA=(t-t_0)I+cN$, $c=\tfrac12(t^2-t_0^2)$.
> $A(t)$ and $M$ contain only $I$ and $N$, so they commute, and $\Phi=e^{M}=e^{t-t_0}e^{cN}=e^{t-t_0}(I+cN)$.
> Check: $\Phi(t_0,t_0)=I$. Entry $(1,2)$: $\partial_t\bigl(e^{t-t_0}c\bigr)=e^{t-t_0}c+e^{t-t_0}t$, equal to row 1 of $A$ times column 2 of $\Phi$.
> - A: Only $e^{cN}$ kept. The factor $e^{(t-t_0)I}=e^{t-t_0}I$ from the identity part of $M$ was lost.
> - C: $M$ taken as $A(t)(t-t_0)$, as if $A$ were constant. The integral of $\tau$ is $\tfrac12(t^2-t_0^2)$, not $t(t-t_0)$.
> - D: Both slips: the factor $e^{t-t_0}$ lost and $M$ taken as $A(t)(t-t_0)$.

### Q13 (slide 109, equivalence)

$A(t)$ has the rows $(0,\ 0)$ and $(t,\ 0)$. The new state is $\hat{\mathbf{x}}=P(t)\mathbf{x}$, where $P(t)$ has the rows $(1,\ 0)$ and $(-t^2/2,\ 1)$. The new unforced equation is $\dot{\hat{\mathbf{x}}}=\hat A(t)\hat{\mathbf{x}}$ with $\hat A=(PA+\dot P)P^{-1}$. What is $\hat A(t)$?

- A) The zero matrix
- B) Rows $(0,\ 0)$ and $(t,\ 0)$
- C) Rows $(0,\ 0)$ and $(2t,\ 0)$
- D) Rows $(0,\ 0)$ and $(-t,\ 0)$

> [!success]- Answer
> **A.** $PA$ has the rows $(0,\ 0)$ and $(t,\ 0)$. $\dot P$ has the rows $(0,\ 0)$ and $(-t,\ 0)$. So $PA+\dot P=0$ and $\hat A=0$.
> Reason: here $\Phi(t,0)$ has the rows $(1,\ 0)$ and $(t^2/2,\ 1)$, so $P(t)=\Phi(t,0)^{-1}=\Phi(0,t)$. Then $\hat{\mathbf{x}}(t)=\Phi(0,t)\mathbf{x}(t)=\mathbf{x}(0)$ is constant.
> - B: $\dot P$ forgotten: $PAP^{-1}$ is the LTI formula. Here it gives back $A$.
> - C: Sign slip: $(PA-\dot P)P^{-1}$.
> - D: $PA$ dropped: only $\dot PP^{-1}$ kept.
