---
course: EE 502 Linear System Theory
lecture: 12
title: Stability
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 114-129)
full_notes: lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf
---
# EE 502 · Lecture 12 · Stability: BIBO and internal

> [!summary] In short
> - BIBO stability (input to output): every bounded input gives a bounded output. For LTI: $\int_0^\infty\lvert g\rvert<\infty$, or all poles of $\hat g(s)$ strictly in the left half-plane.
> - Internal stability (the state): all eigenvalues of $A$ have negative real part. Marginal stability allows eigenvalues on the imaginary axis with index 1.
> - Poles are a subset of the eigenvalues. So BIBO-stable does not imply internally stable.
> - Tests without root-finding: the Lyapunov equation $A^{\mathsf T}M+MA=-N$ and the Routh table.
> - LTV: decide from $\Phi(t,t_0)$, never from the frozen eigenvalues of $A(t)$.

Slide numbers below are pages of the 220-page ABO file.

## 1. BIBO stability, single input and output (slides 115-117)
![[ee502_eee501alllecturenotesabo_p115.jpg]]
![[ee502_eee501alllecturenotesabo_p116.jpg]]
![[ee502_eee501alllecturenotesabo_p117.jpg]]

**Notes.** A relaxed LTI system has impulse response $g(t)$ and transfer function $\hat g(s)$:
$$y(t)=\int_0^t g(t-\tau)u(\tau)\,d\tau,\qquad \hat g(s)=\int_0^\infty g(t)e^{-st}\,dt .$$
It is **BIBO-stable** if $\lvert u(t)\rvert\le M$ for all $t$ implies $\lvert y(t)\rvert\le N$ for all $t$, for some $N$.

**Fact 1.** Equivalent:
1. the system is BIBO-stable;
2. $g$ is absolutely integrable: $\int_0^t\lvert g(\tau)\rvert\,d\tau\le K$ for all $t$;
3. all poles of $\hat g(s)$ are in the open left half-plane (for rational $\hat g$).

Proof ideas: (2) $\Rightarrow$ (1): $\lvert y(t)\rvert\le M\int_0^t\lvert g\rvert\le MK$. (1) $\Rightarrow$ (2): the input $u(t_1-\tau)=\operatorname{sign}g(\tau)$ gives $y(t_1)=\int_0^{t_1}\lvert g\rvert$. (3) $\Rightarrow$ (2): partial fractions give terms $t^ke^{\alpha t}$ with $\alpha<0$, each absolutely integrable.

Recipe: cancel common factors, find the poles, all with $\operatorname{Re}<0$ means BIBO-stable. A pole on the imaginary axis already fails. Zeros do not matter.

> [!warning] Slide error (p. 117 example)
> For $\hat g(s)=\dfrac{s+3}{(s+2)(s+1)^3}$ the slide's expansion is wrong. Correct:
> $$\hat g(s)=\frac{2}{(s+1)^3}-\frac{1}{(s+1)^2}+\frac{1}{s+1}-\frac{1}{s+2},\qquad g(t)=(t^2-t+1)e^{-t}-e^{-2t}.$$
> In the triangle-inequality bound every term enters with a plus sign: $\int_0^\infty\lvert g\rvert\le 2+1+1+\tfrac12=\tfrac92$, not $\tfrac{11}{2}$. The exact area is $\tfrac32$. The conclusion (BIBO-stable, poles $-1,-2$) is unaffected.

> [!warning] Watch out
> $g(t)\to 0$ is not enough: $1/(1+t)\to 0$ but $\int_0^T\tfrac{dt}{1+t}=\ln(1+T)\to\infty$.

> [!info] Why (2) implies (3) (slide 117, first lines)
> Take any $s$ with $\operatorname{Re}s\ge 0$. Then $\lvert e^{-st}\rvert=e^{-\operatorname{Re}\{s\}t}\le 1$ for $t\ge 0$, so
> $$\lvert\hat g(s)\rvert\le\int_0^\infty\lvert g(t)\rvert\,\lvert e^{-st}\rvert\,dt\le\int_0^\infty\lvert g(t)\rvert\,dt\le K .$$
> A pole is a point where $\lvert\hat g(s)\rvert\to\infty$. So there is no pole with $\operatorname{Re}s\ge 0$: all poles are in the open left half-plane.

> [!info] Steady-state response of a BIBO-stable system (beyond the slides)
> Let $\hat g(s)$ be BIBO-stable (Chen, Theorem 5.2).
> - Step input $u(t)=a$: $\hat y(s)=\hat g(s)\dfrac{a}{s}=\dfrac{\hat g(0)\,a}{s}+(\text{terms with the poles of }\hat g)$. The terms with the stable poles decay, so $y(t)\to\hat g(0)\,a$.
> - Sinusoid $u(t)=a\sin\omega_0t$: $y(t)\to a\,\lvert\hat g(j\omega_0)\rvert\sin\bigl(\omega_0t+\angle\hat g(j\omega_0)\bigr)$. Same frequency, amplitude scaled by $\lvert\hat g(j\omega_0)\rvert$, phase shifted by $\angle\hat g(j\omega_0)$.
>
> Without BIBO stability these limits do not exist in general, because the terms of the poles of $\hat g$ do not decay.

> [!question]- Check (slide 115): Which of these are BIBO-stable: (a) $\dfrac{s-2}{s^2+2s+5}$, (b) $\dfrac{1}{s(s+3)}$, (c) $\dfrac{s-1}{(s-1)(s+4)}$?
> (a) Poles: $s^2+2s+5=0$ gives $s=-1\pm 2j$. Both have real part $-1<0$: BIBO-stable. The zero at $s=+2$ does not matter.
> (b) Poles $0$ and $-3$. The pole at $0$ is on the imaginary axis, not in the open left half-plane: not BIBO-stable.
> (c) First cancel the common factor: $\hat g(s)=\dfrac{1}{s+4}$. The only pole is $-4$: BIBO-stable. The point $s=1$ is not a pole, because $\lvert\hat g(s)\rvert$ stays finite there.

> [!question]- Check (slide 116): A system has $g(t)=\cos t$, so $\hat g(s)=\dfrac{s}{s^2+1}$. Use the slide's input to show it is not BIBO-stable, then find the output for the bounded input $u(t)=\cos t$.
> The poles are $\pm j$, on the imaginary axis.
> Slide's input: fix $t_1$ and set $u(t_1-\tau)=+1$ where $\cos\tau\ge 0$ and $-1$ where $\cos\tau<0$. Then $\lvert u\rvert\le 1$ and
> $$y(t_1)=\int_0^{t_1}\lvert\cos\tau\rvert\,d\tau .$$
> One period gives $\int_0^{2\pi}\lvert\cos\tau\rvert\,d\tau=4$. So $t_1=2\pi n$ gives $y(t_1)=4n$, which grows without bound. For these $t_1$ the input is always the same square wave $u(t)=\operatorname{sign}(\cos t)$, because $\cos(2\pi n-\tau)=\cos\tau$. So one bounded input gives an unbounded output.
> A simpler bounded input also works. With $u(t)=\cos t$:
> $$y(t)=\int_0^t\cos(t-\tau)\cos\tau\,d\tau=\tfrac12\int_0^t\bigl[\cos t+\cos(t-2\tau)\bigr]d\tau=\tfrac12\,t\cos t+\tfrac12\sin t .$$
> The term $\tfrac12t\cos t$ is unbounded. The input pushes the system exactly at its own frequency (resonance).

> [!question]- Check (slide 117): For $\hat g(s)=\dfrac{s+5}{(s+1)(s+3)^2}$ find $g(t)$, bound $\int_0^\infty\lvert g\rvert\,dt$ with the triangle inequality, and compare the bound with $\lvert\hat g(0)\rvert$.
> Partial fractions:
> $$\hat g(s)=\frac{1}{s+1}-\frac{1}{s+3}-\frac{1}{(s+3)^2},\qquad g(t)=e^{-t}-e^{-3t}-te^{-3t}.$$
> Triangle inequality (every term enters with a plus sign):
> $$\int_0^\infty\lvert g\rvert\,dt\le\int_0^\infty e^{-t}dt+\int_0^\infty e^{-3t}dt+\int_0^\infty te^{-3t}dt=1+\tfrac13+\tfrac19=\tfrac{13}{9}.$$
> So $g$ is absolutely integrable and the system is BIBO-stable (poles $-1,-3,-3$).
> Check of (2) $\Rightarrow$ (3) at $s=0$: $\hat g(0)=\dfrac{5}{1\cdot 9}=\tfrac59\le\tfrac{13}{9}$. Correct.
> Here $g(t)\ge 0$ for all $t\ge 0$ (because $e^{2t}\ge 1+t$), so the exact area is $\int_0^\infty g\,dt=\hat g(0)=\tfrac59$. The triangle bound is not tight, but it only has to be finite.

> [!question]- Check (slide 117, steady state, beyond the slides): $\hat g(s)=\dfrac{4}{s+2}$. What does $y(t)$ approach for (a) $u(t)=3$, (b) $u(t)=\sin 2t$? Why is the answer meaningless for $\hat g(s)=\dfrac{4}{s-2}$?
> The pole is $-2$, so the system is BIBO-stable and the steady-state formulas hold.
> (a) $y(t)\to\hat g(0)\cdot 3=\tfrac42\cdot 3=6$.
> (b) $\hat g(j2)=\dfrac{4}{2+2j}$. Magnitude: $\dfrac{4}{\sqrt{2^2+2^2}}=\dfrac{4}{2\sqrt2}=\sqrt2\approx 1.414$. Phase: $-\arctan\tfrac22=-45^\circ$. So $y(t)\to\sqrt2\,\sin(2t-45^\circ)$.
> For $\dfrac{4}{s-2}$ the pole is $+2$. The output contains a term $e^{2t}$ that grows, so $y(t)$ has no steady state. The number $\hat g(0)=-2$ exists but describes nothing.

## 2. BIBO stability, multivariable case (slide 118)
![[ee502_eee501alllecturenotesabo_p118.jpg]]

**Notes.** Same definition with vector norms $\lVert\mathbf{u}(t)\rVert$, $\lVert\mathbf{y}(t)\rVert$.

**Fact 2.** A MIMO system is BIBO-stable iff every entry $g_{ij}(t)$ of $G(t)$ is absolutely integrable iff every entry of $\hat G(s)$ has all its poles in the open left half-plane. One bad channel is enough to fail.

> [!example] Slide example
> $G(t)=\begin{bmatrix}1+e^{-2t}&e^{-t}\end{bmatrix}$ is not BIBO-stable: $\int_0^\infty\lvert 1+e^{-2t}\rvert\,dt=\infty$. In the $s$-domain, $\hat G(s)=\begin{bmatrix}\dfrac{2s+2}{s(s+2)}&\dfrac{1}{s+1}\end{bmatrix}$ has a pole at $s=0$.

> [!question]- Check (slide 118): A system with 2 inputs and 2 outputs has $\hat g_{11}=\dfrac{1}{s+1}$, $\hat g_{12}=\dfrac{2}{s+3}$, $\hat g_{21}=\dfrac{1}{s^2+4s+13}$, $\hat g_{22}=\dfrac{s+1}{s(s+2)}$. Is it BIBO-stable? If not, give a bounded input with an unbounded output.
> Check every entry. $\hat g_{11}$: pole $-1$. $\hat g_{12}$: pole $-3$. $\hat g_{21}$: poles $-2\pm 3j$. These three are fine.
> $\hat g_{22}$ has poles $0$ and $-2$. The pole at $0$ is on the imaginary axis, so the system is not BIBO-stable. One bad entry is enough.
> The bad channel goes from input 2 to output 2. Take $u_1=0$, $u_2(t)=1$ (bounded). With $\hat g_{22}(s)=\dfrac{1/2}{s}+\dfrac{1/2}{s+2}$, so $g_{22}(t)=\tfrac12+\tfrac12e^{-2t}$:
> $$y_2(t)=\int_0^tg_{22}(\tau)\,d\tau=\frac t2+\frac14\bigl(1-e^{-2t}\bigr)\to\infty .$$

## 3. Internal stability: poles and eigenvalues (slides 119-120)
![[ee502_eee501alllecturenotesabo_p119.jpg]]
![[ee502_eee501alllecturenotesabo_p120.jpg]]

**Notes.** For $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$:
$$\hat G(s)=\frac{C\operatorname{adj}(sI-A)B+D\det(sI-A)}{\det(sI-A)},\qquad\{\text{poles of }\hat G\}\subseteq\{\text{eigenvalues of }A\}.$$
Cancellations can remove eigenvalues from $\hat G$.

> [!example] Slide example
> $\dot x=x+u$, $y=0.5u$: eigenvalue $1$, no poles ($\hat g=0.5$). BIBO-stable, but $x(t)$ grows without bound.

**Definition.** With zero input, $\mathbf{x}(t)=e^{At}\mathbf{x}_0$.
- **Stable in the sense of Lyapunov (marginally stable):** $\mathbf{x}(t)$ is bounded for every $\mathbf{x}_0$.
- **Internally (asymptotically) stable:** $\mathbf{x}(t)\to\mathbf{0}$ for every $\mathbf{x}_0$.

**Fact.**
- Marginally stable iff all eigenvalues have $\operatorname{Re}\lambda\le 0$ and each eigenvalue with $\operatorname{Re}\lambda=0$ has index 1 (simple root of the minimal polynomial, largest Jordan block $1\times 1$).
- Asymptotically stable iff all eigenvalues have $\operatorname{Re}\lambda<0$.

Reason: the entries of $e^{At}$ are combinations of $t^{j}e^{\lambda_it}$, $j<m_i$ (see [[EE502 L09 - LTI state equation solution]]).

For a repeated eigenvalue on the axis, compare the number of independent eigenvectors $n-\operatorname{rank}(A-\lambda I)$ with the multiplicity. Equal means index 1.

> [!warning] Watch out
> - BIBO-stable does not imply internally stable (hidden eigenvalues). Asymptotically stable does imply BIBO-stable.
> - Marginally stable does not imply BIBO-stable (the integrator $1/s$).
> - The slide says "for every nonzero initial state and for every input" $x\to\infty$. Read it as the generic case.

> [!info] What "index" means and why it decides the axis case
> The index $m_i$ of an eigenvalue $\lambda_i$ is the size of its largest Jordan block. It is also the power of $(s-\lambda_i)$ in the minimal polynomial. A Jordan block of size $m$ puts the terms $e^{\lambda t},te^{\lambda t},\dots,t^{m-1}e^{\lambda t}$ into $e^{At}$.
> - $\operatorname{Re}\lambda<0$: every $t^{k}e^{\lambda t}\to 0$, for any block size. The index does not matter.
> - $\operatorname{Re}\lambda=0$: $\lvert t^{k}e^{\lambda t}\rvert=t^{k}$. Bounded only for $k=0$, so the block must be $1\times 1$ (index 1).
> - $\operatorname{Re}\lambda>0$: $e^{\lambda t}$ already grows. Unstable.

> [!question]- Check (slide 119): $A$ has rows $(0,\ 1)$ and $(2,\ -1)$, $B=(0,\ 1)^{\mathsf T}$, $C=(-1,\ 1)$, $D=0$. Find the eigenvalues and $\hat g(s)$. Is the system BIBO-stable? Internally stable? What does the output show for $\mathbf{x}_0=(1,\ 1)^{\mathsf T}$, $u=0$?
> $\det(sI-A)=s(s+1)-2=s^2+s-2=(s-1)(s+2)$. Eigenvalues $1$ and $-2$.
> $(sI-A)^{-1}B=\dfrac{1}{(s-1)(s+2)}\begin{bmatrix}1\\ s\end{bmatrix}$, so
> $$\hat g(s)=C(sI-A)^{-1}B=\frac{-1+s}{(s-1)(s+2)}=\frac{1}{s+2}.$$
> The factor $(s-1)$ cancels. The only pole is $-2$: BIBO-stable. The eigenvalue $+1$ is hidden, so the system is not internally stable.
> $\mathbf{x}_0=(1,1)^{\mathsf T}$ is an eigenvector for $\lambda=1$: $A\mathbf{x}_0=(1,\ 2-1)^{\mathsf T}=\mathbf{x}_0$. So $\mathbf{x}(t)=e^{t}(1,1)^{\mathsf T}$, which grows without bound. But $y(t)=C\mathbf{x}(t)=e^{t}(-1+1)=0$. The output stays at zero while the state blows up.

> [!question]- Check (slide 120): $A_1=\operatorname{diag}(0,\ 0,\ -1)$. $A_2$ has rows $(0,\ 1,\ 0)$, $(0,\ 0,\ 0)$, $(0,\ 0,\ -1)$. Both have eigenvalues $0,\ 0,\ -1$. Classify each one.
> No eigenvalue has positive real part, and neither matrix is asymptotically stable (eigenvalue $0$). The double eigenvalue $0$ is on the imaginary axis, so its index decides.
> Count the independent eigenvectors for $\lambda=0$: $n-\operatorname{rank}(A-0\cdot I)=3-\operatorname{rank}A$.
> - $A_1$: rank $1$, so $3-1=2$ eigenvectors, equal to the multiplicity $2$. Index 1. Marginally stable. Indeed $e^{A_1t}=\operatorname{diag}(1,\ 1,\ e^{-t})$ is bounded.
> - $A_2$: rank $2$, so $3-2=1$ eigenvector, fewer than $2$. There is a $2\times 2$ Jordan block, index 2. Not marginally stable (unstable). Indeed $e^{A_2t}$ has rows $(1,\ t,\ 0)$, $(0,\ 1,\ 0)$, $(0,\ 0,\ e^{-t})$, and the entry $t$ is unbounded. For example $\mathbf{x}_0=(0,1,0)^{\mathsf T}$ gives $x_1(t)=t$.
>
> Minimal polynomials: $s(s+1)$ for $A_1$ ($0$ is a simple root), $s^2(s+1)$ for $A_2$. The eigenvalues alone cannot separate the two cases.

## 4. Lyapunov theorem (slides 121-123)
![[ee502_eee501alllecturenotesabo_p121.jpg]]
![[ee502_eee501alllecturenotesabo_p122.jpg]]
![[ee502_eee501alllecturenotesabo_p123.jpg]]

**Notes.** **Theorem.** $\dot{\mathbf{x}}=A\mathbf{x}$ is asymptotically stable iff for any symmetric $N>0$ there is a unique $M>0$ with
$$A^{\mathsf T}M+MA=-N .$$
- Only if: $M=\int_0^\infty e^{A^{\mathsf T}t}Ne^{At}\,dt$ is positive definite and satisfies the equation, because $\tfrac{d}{dt}\bigl[e^{A^{\mathsf T}t}Ne^{At}\bigr]$ integrates to $-N$.
- If: for an eigenpair $A\mathbf{v}=\lambda\mathbf{v}$, $-\mathbf{v}^*N\mathbf{v}=2\operatorname{Re}\{\lambda\}\,\mathbf{v}^*M\mathbf{v}$, so $\operatorname{Re}\lambda<0$.
- Lemma (uniqueness): $AM+MB=C$ has a unique solution for every $C$ iff $\lambda_i+\mu_j\ne 0$ for all eigenvalues $\lambda_i$ of $A$, $\mu_j$ of $B$.

One $N$ is enough (Remark 2): solve $A^{\mathsf T}M+MA=-I$ and check $M>0$. A matrix with all eigenvalues in the open left half-plane is called **Hurwitz**.

> [!example] $A=\begin{bmatrix}0&1\\-2&-3\end{bmatrix}$, $N=I$
> Unknown $M=\begin{bmatrix}m_1&m_2\\m_2&m_3\end{bmatrix}$. The three equations give $M=\begin{bmatrix}5/4&1/4\\1/4&1/4\end{bmatrix}$. Minors: $\tfrac54>0$, $\det M=\tfrac14>0$. So $M>0$ and $A$ is Hurwitz (eigenvalues $-1,-2$).
> For $A=\begin{bmatrix}0&1\\-2&1\end{bmatrix}$ the unique solution is $M=\begin{bmatrix}-7/4&1/4\\1/4&-3/4\end{bmatrix}$, not positive definite: not Hurwitz.

> [!warning] Slide misprint (Remark 1)
> The third term of $\mathbf{v}^*M\mathbf{v}$ is printed as $-j\mathbf{v}_r^{\mathsf T}M\mathbf{v}_r$. Correct: $\mathbf{v}^*M\mathbf{v}=\mathbf{v}_r^{\mathsf T}M\mathbf{v}_r+j\mathbf{v}_r^{\mathsf T}M\mathbf{v}_i-j\mathbf{v}_i^{\mathsf T}M\mathbf{v}_r+\mathbf{v}_i^{\mathsf T}M\mathbf{v}_i$, and the two imaginary terms cancel.

> [!info] The energy picture (beyond the slides)
> Take $V(\mathbf{x})=\mathbf{x}^{\mathsf T}M\mathbf{x}$ with $M>0$. Think of it as an energy: it is positive for every $\mathbf{x}\ne\mathbf{0}$. Along a solution of $\dot{\mathbf{x}}=A\mathbf{x}$:
> $$\dot V=\dot{\mathbf{x}}^{\mathsf T}M\mathbf{x}+\mathbf{x}^{\mathsf T}M\dot{\mathbf{x}}=\mathbf{x}^{\mathsf T}(A^{\mathsf T}M+MA)\mathbf{x}=-\mathbf{x}^{\mathsf T}N\mathbf{x}<0 .$$
> The energy always decreases, so the state must go to $\mathbf{0}$. The Lyapunov equation says exactly: "there is an energy $M$ that decreases at the rate $N$".
> To solve it by hand for $n=2$: write $M$ symmetric with unknowns $m_1,m_2,m_3$, multiply out, and compare the entries $(1,1)$, $(1,2)$, $(2,2)$. That gives 3 linear equations. Test $M>0$ with the leading minors: $m_1>0$ and $\det M>0$.

> [!question]- Check (slide 121): Scalar case $\dot x=-ax$ with $a>0$ and $N=n>0$. Compute $M$ from the slide's integral and check the Lyapunov equation. What changes for $a<0$?
> Here $A=-a$, so $e^{A^{\mathsf T}t}Ne^{At}=n\,e^{-2at}$ and
> $$M=\int_0^\infty n\,e^{-2at}\,dt=\frac{n}{2a}>0 .$$
> Lyapunov equation: $A^{\mathsf T}M+MA=-2aM=-2a\cdot\dfrac{n}{2a}=-n$. Correct.
> For $a<0$ the integrand $n\,e^{-2at}$ grows, so the integral diverges and the formula for $M$ is not defined. The algebraic equation $-2aM=-n$ still has the unique solution $M=\dfrac{n}{2a}$, but now it is negative. A negative $M$ signals an unstable $A$.

> [!question]- Check (slide 122): Solve $A^{\mathsf T}M+MA=-I$ for the $A$ with rows $(-1,\ 2)$ and $(0,\ -3)$. Is $M$ positive definite? What does that say about $A$?
> Let $M$ have rows $(m_1,\ m_2)$ and $(m_2,\ m_3)$. Then
> $$A^{\mathsf T}M+MA=\begin{bmatrix}-2m_1&2m_1-4m_2\\2m_1-4m_2&4m_2-6m_3\end{bmatrix}=\begin{bmatrix}-1&0\\0&-1\end{bmatrix}.$$
> Entry $(1,1)$: $-2m_1=-1$, so $m_1=\tfrac12$.
> Entry $(1,2)$: $2m_1-4m_2=0$, so $m_2=\tfrac14$.
> Entry $(2,2)$: $4m_2-6m_3=-1$, so $6m_3=2$ and $m_3=\tfrac13$.
> $$M=\begin{bmatrix}1/2&1/4\\1/4&1/3\end{bmatrix}.$$
> Leading minors: $\tfrac12>0$ and $\det M=\tfrac16-\tfrac1{16}=\tfrac5{48}>0$. So $M>0$ and $A$ is asymptotically stable. This agrees with the eigenvalues $-1,-3$ (triangular matrix).
> The solution is unique because no two eigenvalues add to zero: the sums are $-2,-4,-6$.

> [!question]- Check (slide 122, lemma): For $A=\operatorname{diag}(1,\ -1)$ and $N=I$, how many solutions does $A^{\mathsf T}M+MA=-I$ have? Connect the result to the lemma.
> With $M$ as before: $A^{\mathsf T}M+MA$ has entries $(1,1)$: $2m_1$, $(1,2)$: $m_2-m_2=0$, $(2,2)$: $-2m_3$.
> Equations: $2m_1=-1$, $0=0$, $-2m_3=-1$. So $m_1=-\tfrac12$, $m_3=\tfrac12$, and $m_2$ is free: infinitely many solutions.
> Lemma (with $A^{\mathsf T}$ in the place of $A$ and $A$ in the place of $B$): the solution is unique iff $\lambda_i+\lambda_j\ne 0$ for all pairs. Here $\lambda_1+\lambda_2=1+(-1)=0$, so uniqueness fails.
> For a Hurwitz $A$ every sum $\lambda_i+\lambda_j$ has a negative real part, so it is never zero. That is why the theorem can say "unique".
> No solution here is positive definite, because $m_1=-\tfrac12<0$. $A$ is not Hurwitz.

> [!question]- Check (slide 123): Find the mistake. "For the $A$ with rows $(1,\ 2)$ and $(0,\ -3)$ the equation $A^{\mathsf T}M+MA=-I$ has a unique solution $M$, so $A$ is Hurwitz."
> A unique solution is not enough. The test is that $M$ is positive definite (Remark 2: solve for one $N>0$, for example $N=I$, then check $M>0$).
> Solve: $A^{\mathsf T}M+MA$ has entries $(1,1)$: $2m_1$, $(1,2)$: $2m_1-2m_2$, $(2,2)$: $4m_2-6m_3$.
> $2m_1=-1$ gives $m_1=-\tfrac12$. $2m_1-2m_2=0$ gives $m_2=-\tfrac12$. $4m_2-6m_3=-1$ gives $6m_3=-1$, $m_3=-\tfrac16$.
> $$M=\begin{bmatrix}-1/2&-1/2\\-1/2&-1/6\end{bmatrix},\qquad m_1<0,\quad\det M=\tfrac1{12}-\tfrac14=-\tfrac16<0 .$$
> $M$ is not positive definite, so $A$ is not Hurwitz. The eigenvalues are $1$ and $-3$. The solution is still unique because the sums $2,\ -2,\ -6$ are all nonzero.

## 5. Routh-Hurwitz criterion (slide 124)
![[ee502_eee501alllecturenotesabo_p124.jpg]]

**Notes.** For $\Delta(s)=a_0s^n+a_1s^{n-1}+\dots+a_n$, $a_0>0$: first row $a_0,a_2,a_4,\dots$, second row $a_1,a_3,a_5,\dots$. Each new row comes from the two rows above:
$$b_1=\frac{a_1a_2-a_0a_3}{a_1},\quad b_2=\frac{a_1a_4-a_0a_5}{a_1},\quad c_1=\frac{b_1a_3-a_1b_2}{b_1},\ \dots$$
If the first column has no zero, the number of right half-plane roots equals the number of sign changes in the first column.

> [!example] Slide example: $\Delta(s)=s^4+3s^3+5s^2+11s+8$
> | | | | |
> |---|---|---|---|
> | $s^4$ | $1$ | $5$ | $8$ |
> | $s^3$ | $3$ | $11$ | |
> | $s^2$ | $4/3$ | $8$ | |
> | $s^1$ | $-7$ | | |
> | $s^0$ | $8$ | | |
>
> First column $1,3,\tfrac43,-7,8$: two sign changes, two right half-plane eigenvalues ($0.1241\pm j1.8822$). The others are $-2.2483$ and $-1$.

Quick facts: all roots stable implies all coefficients positive. For $n=2$ that is also sufficient. For $n=3$: stable iff $a_1,a_2,a_3>0$ and $a_1a_2>a_3$ (monic). Example from our notes: $s(s+1)(s+2)+K$ is stable iff $0<K<6$.

> [!warning] Watch out
> Positive coefficients do not prove stability for $n\ge 3$: the slide's polynomial has only positive coefficients and two unstable roots.

> [!question]- Check (slide 124): A $4\times 4$ matrix in the slide's companion form has last row $(-5,\ -4,\ -3,\ -2)$. Write $\det(sI-A)$, build the Routh table, and count the eigenvalues in the right half-plane.
> In this form the last row holds the coefficients with a minus sign, lowest power first: $\det(sI-A)=s^4+2s^3+3s^2+4s+5$.
> Rows: $s^4$: $1,\ 3,\ 5$. $s^3$: $2,\ 4$.
> $s^2$: $b_1=\dfrac{2\cdot 3-1\cdot 4}{2}=1$, $b_2=\dfrac{2\cdot 5-1\cdot 0}{2}=5$.
> $s^1$: $c_1=\dfrac{1\cdot 4-2\cdot 5}{1}=-6$.
> $s^0$: $5$.
> First column: $1,\ 2,\ 1,\ -6,\ 5$. Sign changes: $1\to-6$ and $-6\to 5$, two in total. So two eigenvalues are in the right half-plane and $A$ is not Hurwitz, although all coefficients are positive.
> The actual roots are about $0.288\pm j1.416$ and $-1.288\pm j0.858$.

## 6. BIBO stability of LTV systems (slides 126-127)
![[ee502_eee501alllecturenotesabo_p126.jpg]]
![[ee502_eee501alllecturenotesabo_p127.jpg]]

**Notes.** A relaxed LTV system: $y(t)=\int_{t_0}^{t}g(t,\tau)u(\tau)\,d\tau$. It is BIBO-stable iff there is one $K$ with
$$\int_{t_0}^{t}\lvert g(t,\tau)\rvert\,d\tau\le K\quad\text{for all }t\ge t_0 .$$
Multivariable: $\int_{t_0}^{t}\lVert G(t,\tau)\rVert\,d\tau\le K$ with any matrix norm (induced 2-norm, or Frobenius $\lVert A\rVert_F^2=\operatorname{tr}(A^*A)$). All norms are equivalent, so this is the same as "every entry is absolutely integrable". There is no pole test for LTV systems.

> [!info] Reading the LTV condition
> $g(t,\tau)$ is the output at time $t$ caused by a unit impulse applied at time $\tau$. For an LTI system it depends only on $t-\tau$. For an LTV system it does not, so the integral $\int_{t_0}^{t}\lvert g(t,\tau)\rvert\,d\tau$ is a new function of $t$ for each $t$. The important word is "one $K$": the same bound must hold for all $t$. An integral that is finite for each $t$ but grows with $t$ fails the test.

> [!question]- Check (slide 126): With $t_0=0$, decide BIBO stability for (a) $g(t,\tau)=e^{-2t+\tau}$ and (b) $g(t,\tau)=t\,e^{-(t-\tau)}$.
> (a) $\displaystyle\int_0^te^{-2t+\tau}\,d\tau=e^{-2t}(e^{t}-1)=e^{-t}-e^{-2t}$. This is $0$ at $t=0$, goes to $0$ as $t\to\infty$, and has its maximum at $t=\ln 2$ with value $\tfrac12-\tfrac14=\tfrac14$. So $K=\tfrac14$ works: BIBO-stable.
> (b) $\displaystyle\int_0^tt\,e^{-(t-\tau)}\,d\tau=t\,(1-e^{-t})$. Finite for every $t$, but it grows like $t$. No single $K$ bounds it: not BIBO-stable. For example $u=1$ gives exactly $y(t)=t(1-e^{-t})$.

> [!question]- Check (slide 127): For the $A$ with rows $(1,\ 1)$ and $(0,\ 1)$ compute $\lVert A\rVert_F$ and $\lVert A\rVert_2$. Then decide: is $G(t,\tau)=\bigl(e^{-(t-\tau)},\ \tfrac{1}{1+\tau}\bigr)$ BIBO-stable ($t_0=0$)?
> $A^{\mathsf T}A$ has rows $(1,\ 1)$ and $(1,\ 2)$.
> Frobenius: $\lVert A\rVert_F^2=\operatorname{tr}(A^{\mathsf T}A)=1+2=3$, so $\lVert A\rVert_F=\sqrt3\approx 1.732$ (the sum of the squared entries, $1+1+0+1$).
> Induced 2-norm: the square root of the largest eigenvalue of $A^{\mathsf T}A$. $\lambda^2-3\lambda+1=0$ gives $\lambda=\tfrac{3\pm\sqrt5}{2}$, so $\lVert A\rVert_2=\sqrt{\tfrac{3+\sqrt5}{2}}=\tfrac{1+\sqrt5}{2}\approx 1.618$.
> The two numbers differ, but they bound each other: $\lVert A\rVert_2\le\lVert A\rVert_F\le\sqrt n\,\lVert A\rVert_2$. So one is bounded iff the other is. This is what "equivalent norms" means, and it is why the choice of norm does not change the answer.
> For $G$: use the entry test. $\int_0^te^{-(t-\tau)}d\tau=1-e^{-t}\le 1$, fine. $\int_0^t\tfrac{d\tau}{1+\tau}=\ln(1+t)\to\infty$. One entry is not absolutely integrable: not BIBO-stable.

## 7. Stability of LTV state representations (slides 128-129)
![[ee502_eee501alllecturenotesabo_p128.jpg]]
![[ee502_eee501alllecturenotesabo_p129.jpg]]

**Notes.** With $G(t,\tau)=C(t)\Phi(t,\tau)B(\tau)+D(t)\delta(t-\tau)$, BIBO-stable iff
$$\int_{t_0}^{t}\lVert C(t)\Phi(t,\tau)B(\tau)\rVert\,d\tau\le M_1,\qquad\lVert D(t)\rVert\le M_2\quad\text{for all }t\ge t_0 .$$
Zero-input response: $\mathbf{x}(t)=\Phi(t,t_0)\mathbf{x}_0$.
- Marginally stable iff $\lVert\Phi(t,t_0)\rVert\le\kappa$ for all $t_0$ and all $t\ge t_0$.
- Asymptotically stable iff, in addition, $\lVert\Phi(t,t_0)\rVert\to 0$ as $t\to\infty$.

Both kinds of stability are kept by Lyapunov transformations (slide exercise): $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$ with $P$, $P^{-1}$ bounded. See [[EE502 L11 - Equivalence and realization]].

> [!example] Two cautions (our notes)
> - $A(t)=\begin{bmatrix}-1&e^{2t}\\0&-1\end{bmatrix}$ has eigenvalues $-1,-1$ for every $t$, but $\Phi_{12}(t,0)=\sinh t$ is unbounded: unstable.
> - $\dot x=-\tfrac{1}{1+t}x+u$, $y=x$: $\Phi(t,\tau)=\tfrac{1+\tau}{1+t}\to 0$, asymptotically stable. But $\int_0^t\Phi(t,\tau)\,d\tau=\tfrac{t+t^2/2}{1+t}$ is unbounded: not BIBO-stable.

> [!info] Proof of the slide exercise (beyond the slides)
> A Lyapunov transformation has $\lVert P(t)\rVert\le p_1$ and $\lVert P(t)^{-1}\rVert\le p_2$ for all $t$. From $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$:
> $$\lVert\hat\Phi(t,t_0)\rVert\le\lVert P(t)\rVert\,\lVert\Phi(t,t_0)\rVert\,\lVert P(t_0)^{-1}\rVert\le p_1p_2\,\lVert\Phi(t,t_0)\rVert .$$
> So $\Phi$ bounded gives $\hat\Phi$ bounded, and $\Phi\to 0$ gives $\hat\Phi\to 0$. The other direction is the same argument with $\Phi(t,t_0)=P(t)^{-1}\hat\Phi(t,t_0)P(t_0)$. Without the bounds on $P$ and $P^{-1}$ the argument fails, and an ordinary equivalence transformation can change stability.

> [!question]- Check (slide 128): $\dot x=-2x+e^{t}u$ with $t_0=0$. Is it BIBO-stable for (a) $y=x$, (b) $y=e^{-t}x$, (c) $y=e^{-t}x+t\,u$?
> Here $\Phi(t,\tau)=e^{-2(t-\tau)}$ and $B(\tau)=e^{\tau}$.
> (a) $C=1$, $D=0$: $\displaystyle\int_0^te^{-2(t-\tau)}e^{\tau}\,d\tau=e^{-2t}\,\frac{e^{3t}-1}{3}=\frac{e^{t}-e^{-2t}}{3}\to\infty$. Not BIBO-stable. The state equation $\dot x=-2x$ is asymptotically stable, but $B(t)=e^{t}$ is unbounded.
> (b) $C(t)=e^{-t}$: the integral is multiplied by $e^{-t}$: $\dfrac{1-e^{-3t}}{3}\le\dfrac13$. So $M_1=\tfrac13$, and $D=0$: BIBO-stable.
> (c) Same integral as (b), but $\lvert D(t)\rvert=t$ is unbounded. The second condition fails: not BIBO-stable ($u=1$ gives the term $t$ in $y$).
> For LTV systems the test needs $C(t)$, $\Phi(t,\tau)$, $B(\tau)$ together, and $D(t)$ separately.

> [!question]- Check (slide 129): Classify the scalar systems (a) $\dot x=(\cos t)\,x$ and (b) $\dot x=(-1+\cos t)\,x$ with the fact on the slide.
> For a scalar system $\Phi(t,t_0)=\exp\Bigl(\int_{t_0}^{t}a(\sigma)\,d\sigma\Bigr)$.
> (a) $\Phi(t,t_0)=e^{\sin t-\sin t_0}$. Since $-2\le\sin t-\sin t_0\le 2$, we get $e^{-2}\le\Phi\le e^{2}$ for all $t_0$ and $t$. Bounded, so marginally stable. $\Phi$ does not go to $0$ (it keeps oscillating), so it is not asymptotically stable.
> (b) $\Phi(t,t_0)=e^{-(t-t_0)}\,e^{\sin t-\sin t_0}\le e^{2}\,e^{-(t-t_0)}$. Bounded and $\to 0$ as $t\to\infty$: asymptotically stable.
> In (a) the "frozen eigenvalue" $\cos t$ is positive half of the time, and the system is still stable. In (b) it reaches $0$, and the system is still asymptotically stable. The sign of $a(t)$ at single times decides nothing. Only $\Phi$ decides.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| BIBO (LTI) | $\int_0^\infty\lvert g\rvert<\infty$ $\iff$ poles of $\hat g$ in $\operatorname{Re}s<0$ |
| Poles and eigenvalues | $\{\text{poles}\}\subseteq\{\text{eigenvalues of }A\}$ |
| Asymptotic (LTI) | all $\operatorname{Re}\lambda<0$ (Hurwitz) |
| Marginal (LTI) | $\operatorname{Re}\lambda\le 0$, index 1 on the imaginary axis |
| Lyapunov equation | $A^{\mathsf T}M+MA=-N$, $N>0$; Hurwitz iff $M>0$ |
| Routh | sign changes in the first column = number of right half-plane roots |
| Cubic rule | $s^3+a_1s^2+a_2s+a_3$ stable iff all $a_i>0$ and $a_1a_2>a_3$ |
| BIBO (LTV) | $\int_{t_0}^{t}\lVert G(t,\tau)\rVert\,d\tau\le K$ for all $t$ |
| Internal (LTV) | $\lVert\Phi(t,t_0)\rVert$ bounded (marginal), and $\to 0$ (asymptotic) |
| Implications (LTI) | asymptotic $\Rightarrow$ BIBO; BIBO $\not\Rightarrow$ asymptotic; marginal $\not\Rightarrow$ BIBO |

## Check yourself
> [!question]- 1. Is $\hat g(s)=\dfrac{s-1}{(s+1)(s+2)}$ BIBO-stable? Find $g(t)$.
> Poles $-1,-2$: BIBO-stable (the zero at $+1$ does not matter). $g(t)=-2e^{-t}+3e^{-2t}$, and $\int_0^\infty\lvert g\rvert\le 2+\tfrac32=\tfrac72$.

> [!question]- 2. Is $\hat g(s)=\dfrac{1}{s^2+4}$ BIBO-stable? Give a bounded input with unbounded output.
> Poles $\pm 2j$ on the axis: not BIBO-stable. $u=\sin 2t$ gives $y(t)=\tfrac18(\sin 2t-2t\cos 2t)$, unbounded.

> [!question]- 3. $A=\operatorname{diag}(-1,2)$, $B=(1,0)^{\mathsf T}$, $C=(1,\ 1)$. BIBO-stable? Internally stable?
> $\hat g(s)=\tfrac{1}{s+1}$: BIBO-stable. Eigenvalue $2$: not internally stable. The input never reaches $x_2$, so $\hat g$ cannot see it.

> [!question]- 4. Classify the $A$ with rows $(-1,\ 1)$ and $(0,\ -1)$, and the $A$ with rows $(0,\ 0)$ and $(0,\ -2)$.
> First: double eigenvalue $-1$, asymptotically stable (the index matters only on the axis). Second: eigenvalues $0,-2$, the $0$ is simple: marginally stable.

> [!question]- 5. Solve $A^{\mathsf T}M+MA=-I$ for the $A$ with rows $(0,\ 1)$ and $(-1,\ -2)$. Hurwitz?
> Equations: $-2m_2=-1$, $m_1-2m_2-m_3=0$, $2m_2-4m_3=-1$. So $M=\begin{bmatrix}3/2&1/2\\1/2&1/2\end{bmatrix}$, minors $\tfrac32$ and $\tfrac12$, both positive: Hurwitz.

> [!question]- 6. For which $K$ are all roots of $s^3+2s^2+3s+K$ in the open left half-plane?
> First column $1,\ 2,\ \tfrac{6-K}{2},\ K$: all positive iff $0<K<6$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L11 - Equivalence and realization]]. Next: [[EE502 L13 - Controllability]]
- Needs: [[EE502 L08 - Positive definiteness and SVD]] (positive definite $M$), [[EE502 L10 - LTV state equation solution]] ($\Phi$)
- Full step-by-step notes (PDF): [EE502_Lecture_12_Stability.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf`
- Original slides (PDF, pp. 114-129): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L12 - Stability - quiz]]

Our notes also cover discrete-time stability (unit disk, $A^{\mathsf T}MA-M=-N$), which is not on these slides. See the PDF.

Slides not embedded: 114, 125 (section titles).
