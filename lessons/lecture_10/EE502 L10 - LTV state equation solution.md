---
course: EE 502 Linear System Theory
lecture: 10
title: LTV state equation solution
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 103-109)
full_notes: lecture_notes/lecture_10/EE502_Lecture_10_LTV_Solution.pdf
---
# EE 502 · Lecture 10 · Solution of the LTV state equation

> [!summary] In short
> - LTV model: $\dot{\mathbf{x}}=A(t)\mathbf{x}+B(t)\mathbf{u}$. Piecewise continuous data give exactly one solution.
> - A fundamental matrix $X(t)$ holds $n$ unforced solutions as columns. It stays nonsingular for all $t$.
> - State transition matrix: $\Phi(t,t_0)=X(t)X(t_0)^{-1}$. It replaces $e^{A(t-t_0)}$ and depends on both $t$ and $t_0$.
> - Solution: $\mathbf{x}(t)=\Phi(t,t_0)\mathbf{x}_0+\int_{t_0}^{t}\Phi(t,\tau)B(\tau)\mathbf{u}(\tau)\,d\tau$.
> - $\Phi(t,t_0)=e^{\int_{t_0}^{t}A(\tau)d\tau}$ only when $A(t)$ commutes with $\int_{t_0}^{t}A$. Test it first.

Slide numbers below are pages of the 220-page ABO file. Midterm and final material.

## 1. The LTV equations, existence and uniqueness (slide 104)
![[ee502_eee501alllecturenotesabo_p104.jpg]]

**Notes.** The LTV (linear time-varying) state representation, for $t\ge t_0$ with $\mathbf{x}(t_0)=\mathbf{x}_0$:
$$\dot{\mathbf{x}}(t)=A(t)\mathbf{x}(t)+B(t)\mathbf{u}(t),\qquad \mathbf{y}(t)=C(t)\mathbf{x}(t)+D(t)\mathbf{u}(t).$$

**Fact 1.** If the entries of $A(t)$ and $\mathbf{v}(t)$ are piecewise continuous on $[t_i,t_f]$ (finitely many finite jumps), then $\dot{\mathbf{x}}=A(t)\mathbf{x}+\mathbf{v}(t)$ has exactly one solution for each $\mathbf{x}(t_0)=\mathbf{x}_0$, valid on the whole interval. Use it with $\mathbf{v}=B\mathbf{u}$.

| | LTI (Lecture 9) | LTV |
|---|---|---|
| State transition | $e^{A(t-t_0)}$ | $\Phi(t,t_0)$ |
| Depends on | $t-t_0$ only | both $t$ and $t_0$ |
| Closed form | always | only in special cases |

Scalar case ($n=1$): $\Phi(t,\tau)=e^{\int_\tau^t a(\sigma)d\sigma}$, always, because scalars commute.

> [!question]- Check (slide 104, Fact 1): Take the scalar equation $\dot x=\tfrac{1}{t-1}x$ on $[0,2]$ with $x(0)=1$. Does Fact 1 apply? Show that $x(t)=1-t$ on $[0,1]$ followed by $x(t)=c\,(t-1)$ on $[1,2]$ satisfies the equation at every $t\ne 1$, for every constant $c$. What does this say about uniqueness?
> Fact 1 does not apply. $a(t)=\tfrac{1}{t-1}$ is not piecewise continuous on $[0,2]$: at $t=1$ it goes to infinity, and piecewise continuous allows only finite jumps.
> On $[0,1)$: $x=1-t$ gives $\dot x=-1$ and $\tfrac{x}{t-1}=\tfrac{1-t}{t-1}=-1$. Equal, and $x(0)=1$.
> On $(1,2]$: $x=c(t-1)$ gives $\dot x=c$ and $\tfrac{x}{t-1}=c$. Equal for every $c$.
> Both pieces are $0$ at $t=1$, so the function is continuous. At $t=1$ itself the equation is not defined, because $a(1)$ does not exist (and for $c\ne -1$ the function has a corner there).
> On $[0,1)$ the coefficient is continuous, so the solution $1-t$ is unique there (Fact 1 on every $[0,t_f]$ with $t_f<1$). Across $t=1$ the coefficient is not continuous, so Fact 1 gives no guarantee. Here the continuation past $t=1$ is really not unique: every $c$ works.
> Fact 1 goes one way only. It does not say that uniqueness must fail when $a(t)$ is unbounded. It only cannot promise it. With a finite jump in $a(t)$ (for example $a=1$ for $t<1$ and $a=-2$ for $t\ge 1$) Fact 1 applies and the solution is unique.

> [!question]- Check (slide 104, scalar case): For $\dot x=(\cos t)\,x$ find $\Phi(t,\tau)$. Compute $\Phi(\pi/2,0)$ and $\Phi(\pi,\pi/2)$. What does the result say about "depends on $t-\tau$ only"?
> $\int_\tau^t\cos\sigma\,d\sigma=\sin t-\sin\tau$, so $\Phi(t,\tau)=e^{\sin t-\sin\tau}$.
> $\Phi(\pi/2,0)=e^{1-0}=e\approx 2.718$. $\Phi(\pi,\pi/2)=e^{0-1}=e^{-1}\approx 0.368$.
> Both intervals have the same length $\pi/2$, but the state grows over the first and shrinks over the second. So $\Phi$ is not a function of $t-\tau$ alone. That is the difference from the LTI case $e^{a(t-\tau)}$.
> Check: $\tfrac{\partial}{\partial t}e^{\sin t-\sin\tau}=\cos t\,e^{\sin t-\sin\tau}$ and $\Phi(\tau,\tau)=e^0=1$.

## 2. Fundamental matrix (slide 105)
![[ee502_eee501alllecturenotesabo_p105.jpg]]

**Notes.** Take the unforced equation $\dot{\mathbf{x}}=A(t)\mathbf{x}$. Solve it from $n$ initial vectors and put the solutions side by side: $X(t)=[\mathbf{x}_1(t)\ \cdots\ \mathbf{x}_n(t)]$. Then $\dot X=A(t)X$. $X$ is a **fundamental matrix** when $X(t_0)$ is nonsingular (independent starting vectors).

**Fact 2.** A fundamental matrix is nonsingular for all $t\ge t_0$. Proof: if $X(t_1)\boldsymbol{\alpha}=\mathbf{0}$ with $\boldsymbol{\alpha}\ne\mathbf{0}$, then $\mathbf{x}(t)=X(t)\boldsymbol{\alpha}$ is a solution that is zero at $t_1$, so it is zero for all $t$ by uniqueness. That contradicts $X(t_0)\boldsymbol{\alpha}\ne\mathbf{0}$.

Quantitative version (our notes): $\det X(t)=\det X(t_0)\exp\bigl(\int_{t_0}^{t}\operatorname{tr}A(\tau)\,d\tau\bigr)$.

> [!question]- Check (slide 105, fundamental matrix): $A(t)$ has rows $(2t,\ 0)$ and $(1,\ 2t)$. Two solutions are claimed: $\mathbf{x}_1(t)=e^{t^2}(1,\ t)^{\mathsf T}$ and $\mathbf{x}_2(t)=e^{t^2}(0,\ 1)^{\mathsf T}$. Verify them. Is $X(t)=[\mathbf{x}_1\ \mathbf{x}_2]$ a fundamental matrix for $t_0=0$? Check $\det X(t)$ with the trace formula.
> The equations are $\dot x_1=2t\,x_1$ and $\dot x_2=x_1+2t\,x_2$.
> $\mathbf{x}_1$: first entry $\tfrac{d}{dt}e^{t^2}=2te^{t^2}$, equal to $2t\cdot e^{t^2}$. Second entry $\tfrac{d}{dt}(te^{t^2})=e^{t^2}+2t^2e^{t^2}$, equal to $x_1+2t\cdot te^{t^2}$. Correct.
> $\mathbf{x}_2$: first entry $0=2t\cdot 0$. Second entry $\tfrac{d}{dt}e^{t^2}=2te^{t^2}=0+2t\,e^{t^2}$. Correct.
> $X(0)=I$ is nonsingular, so $X$ is a fundamental matrix.
> $\det X(t)=e^{t^2}\cdot e^{t^2}-0=e^{2t^2}$. Trace formula: $\operatorname{tr}A=4t$, $\int_0^t4\tau\,d\tau=2t^2$, so $\det X(t)=1\cdot e^{2t^2}$. The same, and never zero.

> [!question]- Check (slide 105, Fact 2): $X(t)$ has rows $(1,\ t)$ and $(0,\ t)$. It is singular at $t=0$ and nonsingular at $t=1$. Can it be a fundamental matrix of some $\dot{\mathbf{x}}=A(t)\mathbf{x}$ with $A(t)$ piecewise continuous on $[0,1]$?
> No. $\det X(t)=t$, so $X(0)\boldsymbol{\alpha}=\mathbf{0}$ for $\boldsymbol{\alpha}=(0,\ 1)^{\mathsf T}$. If $X$ solved such an equation, $\mathbf{x}(t)=X(t)\boldsymbol{\alpha}=(t,\ t)^{\mathsf T}$ would be a solution that is zero at $t=0$. The zero function is also a solution with that value. By uniqueness (Fact 1 holds on the whole interval, forward and backward in time) $\mathbf{x}$ would be zero everywhere. But $\mathbf{x}(1)=(1,\ 1)^{\mathsf T}\ne\mathbf{0}$. Contradiction.
> What goes wrong: the only possible matrix is $A(t)=\dot X(t)X(t)^{-1}$, which has rows $(0,\ 1/t)$ and $(0,\ 1/t)$. It is unbounded at $t=0$, so it is not piecewise continuous there.
> General rule: a matrix of solutions is nonsingular at every time or at no time.

## 3. State transition matrix (slide 106)
![[ee502_eee501alllecturenotesabo_p106.jpg]]

**Notes.** $\Phi(t,t_0):=X(t)X(t_0)^{-1}$ for any fundamental matrix $X$. Read it as "from $t_0$ to $t$". It is the unique solution of
$$\frac{\partial}{\partial t}\Phi(t,t_0)=A(t)\Phi(t,t_0),\qquad \Phi(t_0,t_0)=I_n,$$
and for the unforced system $\mathbf{x}(t)=\Phi(t,t_0)\mathbf{x}(t_0)$. Shortcut: start the runs from $\mathbf{e}_1,\dots,\mathbf{e}_n$ at $t_0$; then $X(t)=\Phi(t,t_0)$ with no inverse.

> [!example] Slide example: $A(t)=\begin{bmatrix}0&0\\t&0\end{bmatrix}$
> Equations: $\dot x_1=0$, $\dot x_2=t\,x_1$. Solve top-down: $x_1(t)=x_1(t_0)$, $x_2(t)=x_2(t_0)+\tfrac{t^2-t_0^2}{2}x_1(t_0)$.
> With $t_0=0$ and starts $(1,1)$, $(1,-1)$: $X(t)=\begin{bmatrix}1&1\\ \tfrac{t^2}{2}+1&\tfrac{t^2}{2}-1\end{bmatrix}$, $\det X=-2$.
> $$\Phi(t,0)=X(t)X(0)^{-1}=\begin{bmatrix}1&0\\ \tfrac{t^2}{2}&1\end{bmatrix},\qquad \Phi(t,t_0)=\begin{bmatrix}1&0\\ \tfrac{t^2-t_0^2}{2}&1\end{bmatrix}.$$
> Not a function of $t-t_0$ alone.

> [!warning] Slide slip
> The slide solves the example with $t_0=0$. Its last line is labelled $\Phi(t,t_0)$, but it uses $X(0)^{-1}$, so it is $\Phi(t,0)$. Do not read it as the formula for a general $t_0$: there the entry $(2,1)$ is $\tfrac{t^2-t_0^2}{2}$, as in the example above (slide 109 gives this general form).

> [!question]- Check (slide 106, any fundamental matrix): The slide says "for any fundamental matrix". Let $X(t)$ be a fundamental matrix and $K$ a constant nonsingular matrix. Show that $\tilde X(t)=X(t)K$ is also a fundamental matrix and that it gives the same $\Phi(t,t_0)$.
> $\dot{\tilde X}=\dot XK=A(t)XK=A(t)\tilde X$, and $\tilde X(t_0)=X(t_0)K$ is a product of two nonsingular matrices, so it is nonsingular. So $\tilde X$ is a fundamental matrix. Its columns are the solutions for other initial vectors.
> $\tilde X(t)\tilde X(t_0)^{-1}=X(t)K\,K^{-1}X(t_0)^{-1}=X(t)X(t_0)^{-1}=\Phi(t,t_0)$.
> So $\Phi$ does not depend on the chosen initial vectors. In the slide example the starts $(1,1)$, $(1,-1)$ and the starts $\mathbf{e}_1$, $\mathbf{e}_2$ give the same $\Phi$.
> The constant must stand on the right. $KX(t)$ is in general not a solution of $\dot X=A(t)X$.

> [!question]- Check (slide 106, triangular): $A(t)$ has rows $(-1,\ 0)$ and $(e^{-t},\ 0)$. Find $\Phi(t,t_0)$ by solving the scalar equations one after another.
> Equations: $\dot x_1=-x_1$ and $\dot x_2=e^{-t}x_1$.
> First: $x_1(t)=e^{-(t-t_0)}x_1(t_0)$.
> Second: $\dot x_2=e^{-t}e^{-(t-t_0)}x_1(t_0)=e^{t_0-2t}x_1(t_0)$. Integrate from $t_0$ to $t$:
> $$x_2(t)=x_2(t_0)+x_1(t_0)\,e^{t_0}\int_{t_0}^{t}e^{-2\sigma}d\sigma=x_2(t_0)+\tfrac12\bigl(e^{-t_0}-e^{t_0-2t}\bigr)x_1(t_0).$$
> Read off the coefficients of $x_1(t_0)$ and $x_2(t_0)$:
> $$\Phi(t,t_0)=\begin{bmatrix}e^{-(t-t_0)}&0\\ \tfrac12\bigl(e^{-t_0}-e^{t_0-2t}\bigr)&1\end{bmatrix}.$$
> Check: at $t=t_0$ the entry $(2,1)$ is $\tfrac12(e^{-t_0}-e^{-t_0})=0$, so $\Phi(t_0,t_0)=I$. Derivative of the entry $(2,1)$ in $t$: $e^{t_0-2t}=e^{-t}\cdot e^{-(t-t_0)}$, which is row 2 of $A(t)$ times column 1 of $\Phi$. So $\partial_t\Phi=A(t)\Phi$.

## 4. Properties and the solution formula (slide 107)
![[ee502_eee501alllecturenotesabo_p107.jpg]]

**Notes.**

**Fact 3.** $\Phi(t,t_0)=\Phi(t,t_1)\Phi(t_1,t_0)$ and $\Phi(t,t_0)^{-1}=\Phi(t_0,t)$. Also $\tfrac{\partial}{\partial\tau}\Phi(t,\tau)=-\Phi(t,\tau)A(\tau)$.

**Fact 4 (variation of constants).**
$$\begin{aligned}\mathbf{x}(t)&=\Phi(t,t_0)\mathbf{x}_0+\int_{t_0}^{t}\Phi(t,\tau)B(\tau)\mathbf{u}(\tau)\,d\tau,\\ \mathbf{y}(t)&=C(t)\Phi(t,t_0)\mathbf{x}_0+\int_{t_0}^{t}C(t)\Phi(t,\tau)B(\tau)\mathbf{u}(\tau)\,d\tau+D(t)\mathbf{u}(t).\end{aligned}$$
First term: zero-input part. Integral: zero-state part. The impulse response is $G(t,\tau)=C(t)\Phi(t,\tau)B(\tau)+D(t)\delta(t-\tau)$, a function of both $t$ and $\tau$.

> [!example] Scalar example (our notes): $\dot x=-2t\,x+2t\,u$, $u\equiv 1$, $x(0)=x_0$
> $\Phi(t,\tau)=e^{-(t^2-\tau^2)}$. Result: $x(t)=x_0e^{-t^2}+(1-e^{-t^2})=1+(x_0-1)e^{-t^2}$.

> [!warning] Slide slips
> The slide states the solution "for $t\ge 0$" and writes the feedthrough as $D\mathbf{u}(t)$. Intended: $t\ge t_0$ and the time-varying $D(t)\mathbf{u}(t)$.
> The inverse of $\Phi$ is "swap the arguments", not the transpose. In the product the later leg stands on the left.

> [!info] Where Fact 3 comes from (beyond the slides)
> The slide says "the definition directly gives". The two lines are:
> $\Phi(t,t_1)\Phi(t_1,t_0)=X(t)X(t_1)^{-1}X(t_1)X(t_0)^{-1}=X(t)X(t_0)^{-1}=\Phi(t,t_0)$.
> $\Phi(t,t_0)^{-1}=\bigl(X(t)X(t_0)^{-1}\bigr)^{-1}=X(t_0)X(t)^{-1}=\Phi(t_0,t)$.
> Meaning: going from $t_0$ to $t$ is the same as going from $t_0$ to $t_1$ and then from $t_1$ to $t$. Going backward in time undoes going forward. $t_1$ does not have to lie between $t_0$ and $t$.

> [!question]- Check (slide 107, properties): A system has $\Phi(t,t_0)=e^{t^2-t_0^2}\,T(t-t_0)$, where $T(d)$ has rows $(1,\ 0)$ and $(d,\ 1)$. Verify $\Phi(2,0)=\Phi(2,1)\Phi(1,0)$ and write $\Phi(2,0)^{-1}$ with the inversion property.
> $\Phi(1,0)=e^{1}T(1)$ and $\Phi(2,1)=e^{4-1}T(1)=e^{3}T(1)$.
> $T(1)T(1)$: rows $(1,\ 0)$ and $(1+1,\ 1)=(2,\ 1)$, so $T(1)T(1)=T(2)$.
> Product: $\Phi(2,1)\Phi(1,0)=e^{3}e^{1}T(2)=e^{4}T(2)$. Direct: $\Phi(2,0)=e^{4-0}T(2)$. Equal.
> Inverse: $\Phi(2,0)^{-1}=\Phi(0,2)=e^{0-4}T(-2)$, that is $e^{-4}$ times the matrix with rows $(1,\ 0)$ and $(-2,\ 1)$.
> Check: $T(2)T(-2)$ has rows $(1,\ 0)$ and $(2-2,\ 1)$, so it is $I$, and $e^{4}e^{-4}=1$.

> [!question]- Check (slide 107, solution formula): $A(t)$ has rows $(-1,\ 0)$ and $(e^{-t},\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $t_0=0$, $\mathbf{x}(0)=\mathbf{0}$, $u\equiv 1$. The first column of $\Phi(t,\tau)$ is $\bigl(e^{-(t-\tau)},\ \tfrac12(e^{-\tau}-e^{\tau-2t})\bigr)^{\mathsf T}$. Find $\mathbf{x}(t)$ with Fact 4 and check it.
> $\mathbf{x}_0=\mathbf{0}$, so only the integral is left, and $\Phi(t,\tau)B$ is the first column of $\Phi(t,\tau)$.
> $x_1(t)=\int_0^te^{-(t-\tau)}d\tau=e^{-t}(e^{t}-1)=1-e^{-t}$.
> $x_2(t)=\tfrac12\int_0^t\bigl(e^{-\tau}-e^{\tau-2t}\bigr)d\tau=\tfrac12\bigl[(1-e^{-t})-e^{-2t}(e^{t}-1)\bigr]=\tfrac12-e^{-t}+\tfrac12e^{-2t}$.
> Check: the equations are $\dot x_1=-x_1+1$ and $\dot x_2=e^{-t}x_1$.
> $\dot x_1=e^{-t}$ and $-x_1+1=e^{-t}$. $\dot x_2=e^{-t}-e^{-2t}$ and $e^{-t}(1-e^{-t})=e^{-t}-e^{-2t}$. $\mathbf{x}(0)=(0,\ \tfrac12-1+\tfrac12)^{\mathsf T}=\mathbf{0}$.

> [!question]- Check (slide 107, impulse response): For the same system take $C=(0,\ 1)$ and $D=0$. Find $G(t,\tau)$ for $t\ge\tau$. Compare $G(1,0)$ with $G(2,1)$. What does it mean?
> $G(t,\tau)=C\,\Phi(t,\tau)B$ is the entry $(2,1)$ of $\Phi(t,\tau)$: $G(t,\tau)=\tfrac12\bigl(e^{-\tau}-e^{\tau-2t}\bigr)$.
> $G(1,0)=\tfrac12(1-e^{-2})\approx 0.432$. $G(2,1)=\tfrac12(e^{-1}-e^{-3})\approx 0.159$.
> In both cases the output is read $1$ time unit after the impulse, but the values differ. So $G$ is not a function of $t-\tau$ alone: the answer to an impulse depends on when the impulse is applied. For an LTI system the two values would be equal, $H(t-\tau)$. This is why an LTV system has no transfer function $G(s)$ of the usual kind.

## 5. Computing the state transition matrix (slides 108-109)
![[ee502_eee501alllecturenotesabo_p108.jpg]]
![[ee502_eee501alllecturenotesabo_p109.jpg]]

**Notes.** In general, solve $\partial_t\Phi=A(t)\Phi$, $\Phi(t_0,t_0)=I$: $n$ vector equations, one per $\mathbf{e}_i$. Triangular $A(t)$: one row at a time.

**Fact 5 (commuting case).** If $A(t)$ and $M=\int_{t_0}^{t}A(\tau)\,d\tau$ commute, then $\Phi(t,t_0)=e^{M}$. For constant $A$ this gives $e^{A(t-t_0)}$, the LTI result.

Recipe: integrate $A$ entry by entry, test $A(t)M=MA(t)$, compute $e^{M}$ (a nilpotent $N$ with $N^2=0$ gives $e^{cN}=I+cN$), check $\Phi(t_0,t_0)=I$.

> [!example] Slide example (p. 109): $A(t)=\begin{bmatrix}0&0\\t&0\end{bmatrix}$
> $M=\begin{bmatrix}0&0\\ \tfrac{t^2-t_0^2}{2}&0\end{bmatrix}$, $A(t)M=MA(t)=0$ and $M^2=0$. So $\Phi(t,t_0)=I+M$, the same answer as in section 3.

> [!example] Non-commuting (our notes): $A(t)=\begin{bmatrix}0&t\\0&1\end{bmatrix}$
> $A(t)$ and $\int A$ do not commute. Solving row by row gives $\Phi(t,t_0)=\begin{bmatrix}1&(t-1)e^{t-t_0}+1-t_0\\0&e^{t-t_0}\end{bmatrix}$, which is not $e^{\int A}$.

> [!warning] Watch out
> - Never write $\Phi=e^{\int A}$ without the commutation test.
> - Frozen-time eigenvalues say nothing reliable: $A(t)=\begin{bmatrix}-1&e^{2t}\\0&-1\end{bmatrix}$ has eigenvalues $-1,-1$ for every $t$, yet $\Phi_{12}(t,0)=\sinh t$ grows without bound.

The lower half of slide 109 starts "Equivalence of time-varying representations". It is covered in [[EE502 L11 - Equivalence and realization]].

> [!info] Why Fact 5 needs the commutation (beyond the slides)
> The proof on slide 108 only says "by the chain rule". Write $M(t)=\int_{t_0}^{t}A(\tau)\,d\tau$, so $\dot M=A(t)$, and $e^{M}=I+M+\tfrac{1}{2!}M^2+\tfrac{1}{3!}M^3+\cdots$.
> Product rule for the square: $\tfrac{d}{dt}M^2=\dot MM+M\dot M=AM+MA$. This is $2AM$ only if $AM=MA$.
> If $A$ and $M$ commute, then $\tfrac{d}{dt}M^k=kAM^{k-1}$ for every $k$, and term by term $\tfrac{d}{dt}e^{M}=A\bigl(I+M+\tfrac{1}{2!}M^2+\cdots\bigr)=A(t)e^{M}$. So $e^{M}$ solves $\partial_t\Phi=A(t)\Phi$.
> If they do not commute, the terms $MA$ stay. Then in general $\tfrac{d}{dt}e^{M}\ne A(t)e^{M}$, and $e^{M}$ is not the state transition matrix.
> Cases where the test always passes: constant $A$, diagonal $A(t)$, and $A(t)=f(t)A_0$ with a scalar function $f$ and a constant matrix $A_0$.

> [!warning] Slide error
> The series on slide 109 is written $I_2+M+M^2+\cdots$, without the factors $\tfrac{1}{k!}$. The correct series is $I+M+\tfrac{1}{2!}M^2+\tfrac{1}{3!}M^3+\cdots$. The result on the slide is still right, because $M^2=0$ in this example.

> [!question]- Check (slide 108, commuting case): $A(t)$ has rows $(0,\ t)$ and $(-t,\ 0)$. Does Fact 5 apply? Find $\Phi(t,t_0)$.
> $A(t)=t\,J$ with the constant matrix $J$ with rows $(0,\ 1)$ and $(-1,\ 0)$. Then $M=\int_{t_0}^{t}\tau\,d\tau\,J=\theta J$ with $\theta=\tfrac{t^2-t_0^2}{2}$.
> $A(t)M=t\theta J^2=MA(t)$: both are multiples of the same matrix, so they commute. Fact 5 applies.
> $J^2=-I$, so the series gives $e^{\theta J}=\cos\theta\,I+\sin\theta\,J$:
> $$\Phi(t,t_0)=\begin{bmatrix}\cos\theta&\sin\theta\\-\sin\theta&\cos\theta\end{bmatrix},\qquad\theta=\frac{t^2-t_0^2}{2}.$$
> Check: $\theta=0$ at $t=t_0$, so $\Phi(t_0,t_0)=I$. With $\dot\theta=t$: $\partial_t\Phi$ has rows $t(-\sin\theta,\ \cos\theta)$ and $t(-\cos\theta,\ -\sin\theta)$, and $A(t)\Phi$ has the same rows.
> The state turns on a circle, faster and faster, because the angle grows like $t^2/2$.

> [!question]- Check (slide 108, not commuting): $A(t)$ has rows $(-1,\ 0)$ and $(e^{-t},\ 0)$, $t_0=0$. Compute $M=\int_0^tA(\tau)\,d\tau$, test the commutation, and compare the entry $(2,1)$ of $e^{M}$ at $t=1$ with the true value $\Phi_{21}(1,0)=\tfrac12(1-e^{-2})$.
> $M$ has rows $(-t,\ 0)$ and $(1-e^{-t},\ 0)$.
> $A(t)M$ has rows $(t,\ 0)$ and $(-te^{-t},\ 0)$. $MA(t)$ has rows $(t,\ 0)$ and $(-(1-e^{-t}),\ 0)$. The entries $(2,1)$ differ ($te^{-t}\ne 1-e^{-t}$ for $t\neq 0$). They do not commute, so Fact 5 does not apply.
> $e^{M}$ anyway: $M^2=-tM$, so $M^k=(-t)^{k-1}M$ and $e^{M}=I+\tfrac{1-e^{-t}}{t}M$. Entry $(2,1)$: $\tfrac{(1-e^{-t})^2}{t}$.
> At $t=1$: $(1-e^{-1})^2\approx 0.400$. True value: $\tfrac12(1-e^{-2})\approx 0.432$. Different, so $e^{\int A}$ is not the state transition matrix here.
> The true $\Phi$ comes from solving the two scalar equations one after another (question on slide 106).

> [!question]- Check (slide 109, example): $A(t)$ has rows $(1,\ t)$ and $(0,\ 1)$. Use the method of the slide example to find $\Phi(t,t_0)$.
> $A(t)=I+tN$ with $N$ with rows $(0,\ 1)$ and $(0,\ 0)$, $N^2=0$.
> $M=\int_{t_0}^{t}A(\tau)\,d\tau=(t-t_0)I+cN$ with $c=\tfrac{t^2-t_0^2}{2}$.
> $A(t)$ and $M$ contain only $I$ and $N$, so they commute. Fact 5 applies.
> $(t-t_0)I$ commutes with $cN$, so $e^{M}=e^{t-t_0}\,e^{cN}=e^{t-t_0}(I+cN)$:
> $$\Phi(t,t_0)=e^{t-t_0}\begin{bmatrix}1&\tfrac{t^2-t_0^2}{2}\\0&1\end{bmatrix}.$$
> Check: $\Phi(t_0,t_0)=I$. Entry $(1,2)$: $\tfrac{\partial}{\partial t}\bigl(e^{t-t_0}c\bigr)=e^{t-t_0}c+e^{t-t_0}t$, and row 1 of $A(t)$ times column 2 of $\Phi$ is $1\cdot e^{t-t_0}c+t\cdot e^{t-t_0}$. Equal.

> [!question]- Check (slide 109, equivalence): Take the slide example $A(t)$ with rows $(0,\ 0)$ and $(t,\ 0)$ and the new state $\hat{\mathbf{x}}=P(t)\mathbf{x}$, where $P(t)$ has rows $(1,\ 0)$ and $(-t^2/2,\ 1)$. Compute the new system matrix $(PA+\dot P)P^{-1}$. Why this result?
> $PA$: rows $(0,\ 0)$ and $(t,\ 0)$. $\dot P$: rows $(0,\ 0)$ and $(-t,\ 0)$.
> $PA+\dot P=0$, so $(PA+\dot P)P^{-1}=0$. The new unforced equation is $\dot{\hat{\mathbf{x}}}=\mathbf{0}$: the new state is constant.
> Reason: $P(t)=\Phi(0,t)=\Phi(t,0)^{-1}$. Then $\hat{\mathbf{x}}(t)=\Phi(0,t)\mathbf{x}(t)=\mathbf{x}(0)$, the initial state, which does not move.
> The term $\dot P$ is new compared with the LTI case. With a constant $P$ the formula becomes the usual $PAP^{-1}$.

## 6. Extras in our notes (not on these slides)
No slide pages. Written from the `.tex` alone (standard material, Chen Ch. 4).

- **Peano-Baker series.** Always valid: $\Phi(t,t_0)=I+\int_{t_0}^{t}A(\sigma_1)d\sigma_1+\int_{t_0}^{t}A(\sigma_1)\int_{t_0}^{\sigma_1}A(\sigma_2)\,d\sigma_2\,d\sigma_1+\cdots$. The latest time stands on the left. If everything commutes it collapses to $e^{\int A}$.
- **Adjoint system.** $\dot{\mathbf{z}}=-A(t)^{\mathsf T}\mathbf{z}$ has $\Phi_a(t,t_0)=\Phi(t_0,t)^{\mathsf T}$: swap the arguments and transpose. $\mathbf{z}^{\mathsf T}\mathbf{x}$ stays constant.
- **Discrete time.** $\mathbf{x}[k+1]=A[k]\mathbf{x}[k]+B[k]\mathbf{u}[k]$ has $\Phi[k,k_0]=A[k-1]\cdots A[k_0]$ (newest on the left) and
$$\mathbf{x}[k]=\Phi[k,k_0]\mathbf{x}_0+\sum_{m=k_0}^{k-1}\Phi[k,m+1]B[m]\mathbf{u}[m].$$
  Unlike continuous time, $\Phi[k,k_0]$ can be singular.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Fundamental matrix | $\dot X=A(t)X$, $X(t_0)$ nonsingular; then nonsingular for all $t$ |
| State transition matrix | $\Phi(t,t_0)=X(t)X(t_0)^{-1}$; $\partial_t\Phi=A(t)\Phi$, $\Phi(t_0,t_0)=I$ |
| Properties | $\Phi(t,t_0)=\Phi(t,t_1)\Phi(t_1,t_0)$, $\Phi(t,t_0)^{-1}=\Phi(t_0,t)$, $\partial_\tau\Phi(t,\tau)=-\Phi(t,\tau)A(\tau)$ |
| Solution | $\mathbf{x}(t)=\Phi(t,t_0)\mathbf{x}_0+\int_{t_0}^{t}\Phi(t,\tau)B(\tau)\mathbf{u}(\tau)\,d\tau$ |
| Impulse response | $G(t,\tau)=C(t)\Phi(t,\tau)B(\tau)+D(t)\delta(t-\tau)$ |
| Commuting case | $A(t)\int A=\int A\,A(t)\Rightarrow\Phi=e^{\int_{t_0}^{t}A}$ |
| Adjoint | $\Phi_a(t,t_0)=\Phi(t_0,t)^{\mathsf T}$ |
| Discrete | $\Phi[k,k_0]=A[k-1]\cdots A[k_0]$ |

## Check yourself
> [!question]- 1. Solve $\dot x=-\tfrac{1}{1+t}x+1$, $x(0)=1$.
> $\alpha(t)=-\ln(1+t)$, integrating factor $1+t$: $\tfrac{d}{dt}\bigl((1+t)x\bigr)=1+t$. So $(1+t)x=1+t+\tfrac{t^2}{2}$ and $x(t)=1+\tfrac{t^2}{2(1+t)}$.

> [!question]- 2. $\dot x_1=0$, $\dot x_2=t\,x_1$, runs from $(1,2)$ and $(2,4)$ at $t_0=0$. Fundamental matrix?
> $X(t)=\begin{bmatrix}1&2\\2+\tfrac{t^2}{2}&4+t^2\end{bmatrix}$, $\det X(t)=0$ for every $t$. Not fundamental: the starts are dependent, and they stay dependent.

> [!question]- 3. $A(t)$ has rows $(0,\ 2t)$ and $(0,\ 0)$. Find $\Phi(t,t_0)$.
> $x_2$ is constant, $x_1(t)=x_1(t_0)+(t^2-t_0^2)x_2(t_0)$. So $\Phi(t,t_0)=\begin{bmatrix}1&t^2-t_0^2\\0&1\end{bmatrix}$.

> [!question]- 4. $A(t)$ has rows $(0,\ 0)$ and $(t,\ 0)$, $B=(1,\ 0)^{\mathsf T}$, $C=(0,\ 1)$, $\mathbf{x}(0)=\mathbf{0}$, $u\equiv 1$. Find $\mathbf{x}(t)$, $y(t)$.
> $\Phi(t,\tau)B=(1,\tfrac{t^2-\tau^2}{2})^{\mathsf T}$. Integrate over $\tau\in[0,t]$: $\mathbf{x}(t)=(t,\ t^3/3)^{\mathsf T}$, $y=t^3/3$.

> [!question]- 5. $A(t)=\operatorname{diag}(t,1)$. Does the commuting formula apply? Find $\Phi(t,t_0)$.
> Yes, diagonal matrices commute. $\Phi(t,t_0)=\operatorname{diag}\bigl(e^{(t^2-t_0^2)/2},\ e^{t-t_0}\bigr)$.

> [!question]- 6. Write $\Phi(t,t_0)^{-1}$ for the slide example without computing.
> Swap the arguments: $\Phi(t_0,t)=\begin{bmatrix}1&0\\ \tfrac{t_0^2-t^2}{2}&1\end{bmatrix}$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L09 - LTI state equation solution]]. Next: [[EE502 L11 - Equivalence and realization]]
- Used later in: [[EE502 L12 - Stability]], [[EE502 L13 - Controllability]], [[EE502 L14 - Observability]] (Gramians)
- Full step-by-step notes (PDF): [EE502_Lecture_10_LTV_Solution.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_10/EE502_Lecture_10_LTV_Solution.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_10/EE502_Lecture_10_LTV_Solution.pdf`
- Original slides (PDF, pp. 103-109): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: 103 (section title).
