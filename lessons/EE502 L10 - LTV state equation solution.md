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

## 2. Fundamental matrix (slide 105)
![[ee502_eee501alllecturenotesabo_p105.jpg]]

**Notes.** Take the unforced equation $\dot{\mathbf{x}}=A(t)\mathbf{x}$. Solve it from $n$ initial vectors and put the solutions side by side: $X(t)=[\mathbf{x}_1(t)\ \cdots\ \mathbf{x}_n(t)]$. Then $\dot X=A(t)X$. $X$ is a **fundamental matrix** when $X(t_0)$ is nonsingular (independent starting vectors).

**Fact 2.** A fundamental matrix is nonsingular for all $t\ge t_0$. Proof: if $X(t_1)\boldsymbol{\alpha}=\mathbf{0}$ with $\boldsymbol{\alpha}\ne\mathbf{0}$, then $\mathbf{x}(t)=X(t)\boldsymbol{\alpha}$ is a solution that is zero at $t_1$, so it is zero for all $t$ by uniqueness. That contradicts $X(t_0)\boldsymbol{\alpha}\ne\mathbf{0}$.

Quantitative version (our notes): $\det X(t)=\det X(t_0)\exp\bigl(\int_{t_0}^{t}\operatorname{tr}A(\tau)\,d\tau\bigr)$.

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

> [!question]- 3. $A(t)=\begin{bmatrix}0&2t\\0&0\end{bmatrix}$. Find $\Phi(t,t_0)$.
> $x_2$ is constant, $x_1(t)=x_1(t_0)+(t^2-t_0^2)x_2(t_0)$. So $\Phi(t,t_0)=\begin{bmatrix}1&t^2-t_0^2\\0&1\end{bmatrix}$.

> [!question]- 4. $A(t)=\begin{bmatrix}0&0\\t&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}0&1\end{bmatrix}$, $\mathbf{x}(0)=\mathbf{0}$, $u\equiv 1$. Find $\mathbf{x}(t)$, $y(t)$.
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
