---
course: EE 502 Linear System Theory
lesson: EE502 L09 - LTI state equation solution
type: quiz
questions: 8
---

# EE502 L09 - LTI state equation solution - quiz

Lesson note: [[EE502 L09 - LTI state equation solution]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. The system is $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$. "Unit step" means $u(t)=1$ for $t\ge 0$. The zero-input part is the answer with $u\equiv 0$, the zero-state part the answer with $\mathbf{x}(0)=\mathbf{0}$.

## 1. State trajectory and response (slide 90)

### Q1 (slide 90, derivation)

The solution of $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$ is $\mathbf{x}(t)=e^{At}\mathbf{x}(0)+\mathbf{z}(t)$ with $\mathbf{z}(t)=\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$. You differentiate $\mathbf{z}(t)$ with the Leibniz rule (the upper limit and the integrand both depend on $t$). Where does the term $B\mathbf{u}(t)$ in $\dot{\mathbf{x}}$ come from, and what does the $t$-derivative of the integrand give after the integration?

- A) From the lower limit $\tau=0$. The $t$-derivative of the integrand gives $+A\mathbf{z}(t)$.
- B) From the upper limit $\tau=t$. The $t$-derivative of the integrand gives $-A\mathbf{z}(t)$.
- C) From the lower limit $\tau=0$. The $t$-derivative of the integrand gives $-A\mathbf{z}(t)$.
- D) From the upper limit $\tau=t$. The $t$-derivative of the integrand gives $+A\mathbf{z}(t)$.

> [!success]- Answer
> **D.** Leibniz rule: $\tfrac{d}{dt}\int_0^t F(t,\tau)\,d\tau=F(t,t)+\int_0^t\tfrac{\partial F}{\partial t}(t,\tau)\,d\tau$ with $F=e^{A(t-\tau)}B\mathbf{u}(\tau)$.
> Upper limit: $F(t,t)=e^{A\cdot 0}B\mathbf{u}(t)=B\mathbf{u}(t)$.
> Integrand: $\tfrac{\partial}{\partial t}e^{A(t-\tau)}=Ae^{A(t-\tau)}$, so this part is $A\mathbf{z}(t)$.
> With $\tfrac{d}{dt}e^{At}\mathbf{x}(0)=Ae^{At}\mathbf{x}(0)$: $\dot{\mathbf{x}}=A\bigl[e^{At}\mathbf{x}(0)+\mathbf{z}(t)\bigr]+B\mathbf{u}(t)=A\mathbf{x}+B\mathbf{u}$.
> - A: The lower limit $0$ does not depend on $t$, so it adds nothing. The integrand there would be $e^{At}B\mathbf{u}(0)$, not $B\mathbf{u}(t)$.
> - B: $-A$ is the derivative of $e^{A(t-\tau)}$ with respect to $\tau$, not $t$. Then $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$ would fail.
> - C: Both slips: the lower limit adds nothing, and the derivative was taken with respect to $\tau$.

### Q2 (slide 90, computation)

$A$ has the rows $(0,\ 1)$ and $(-2,\ -3)$, $B=(0,\ 1)^{\mathsf T}$, $\mathbf{x}(0)=(1,\ 0)^{\mathsf T}$, unit step input. You are given $e^{At}$ with the rows $(2e^{-t}-e^{-2t},\ e^{-t}-e^{-2t})$ and $(-2e^{-t}+2e^{-2t},\ -e^{-t}+2e^{-2t})$. What is the second state $x_2(t)$?

- A) $x_2(t)=e^{-t}-e^{-2t}$
- B) $x_2(t)=2e^{-t}-2e^{-2t}$
- C) $x_2(t)=-e^{-t}+e^{-2t}$
- D) $x_2(t)=-2e^{-t}+2e^{-2t}$

> [!success]- Answer
> **C.** Zero-input part: $e^{At}\mathbf{x}(0)$ is the first column of $e^{At}$. Its second entry is $-2e^{-t}+2e^{-2t}$.
> Zero-state part: $\int_0^t e^{A(t-\tau)}B\,d\tau=\int_0^t e^{A\sigma}B\,d\sigma$ with $\sigma=t-\tau$. $e^{A\sigma}B$ is the second column. Its second entry integrates to $-(1-e^{-t})+(1-e^{-2t})=e^{-t}-e^{-2t}$.
> Sum: $x_2=-e^{-t}+e^{-2t}$. (Also $x_1=\tfrac12+e^{-t}-\tfrac12e^{-2t}$.) Check: $\dot x_2=e^{-t}-2e^{-2t}=-2x_1-3x_2+1$.
> - A: Only the zero-state part. The zero-input part $e^{At}\mathbf{x}(0)$ was forgotten.
> - B: $e^{At}\mathbf{x}(0)$ taken as the first row, not the first column: $(e^{-t}-e^{-2t})+(e^{-t}-e^{-2t})$.
> - D: Only the zero-input part. The integral (the input term) was forgotten.

## 2. Zero-input and zero-state parts, Laplace form (slide 91)

### Q3 (slide 91, superposition)

A linear system gives $y(t)=3e^{-t}$ for the initial state $\mathbf{x}_a$ with $u\equiv 0$. It gives $y(t)=2-2e^{-t}$ for $\mathbf{x}(0)=\mathbf{0}$ with a unit step. What is $y(t)$ for $\mathbf{x}(0)=2\mathbf{x}_a$ and a step of height $5$?

- A) $y(t)=10-7e^{-t}$
- B) $y(t)=10-4e^{-t}$
- C) $y(t)=2+4e^{-t}$
- D) $y(t)=4+11e^{-t}$

> [!success]- Answer
> **B.** The zero-input response is linear in $\mathbf{x}(0)$: $2\cdot 3e^{-t}=6e^{-t}$.
> The zero-state response is linear in $u$: $5(2-2e^{-t})=10-10e^{-t}$.
> Sum: $6e^{-t}+10-10e^{-t}=10-4e^{-t}$.
> - A: The factor $2$ on $\mathbf{x}(0)$ was dropped: $3e^{-t}+10-10e^{-t}$.
> - C: The step height $5$ was dropped: $6e^{-t}+2-2e^{-t}$.
> - D: The two factors were swapped: $5\cdot 3e^{-t}+2(2-2e^{-t})$.

### Q4 (slide 91, transfer function)

$A$ has the rows $(0,\ 1)$ and $(-2,\ -3)$, $B=(0,\ 1)^{\mathsf T}$, $C=(1,\ 0)$, $D=1$. Let $y(t)$ be the zero-state response to a unit step. What are $y(0^+)$ and $\lim_{t\to\infty}y(t)$?

- A) $y(0^+)=0$ and $y(t)\to\tfrac12$
- B) $y(0^+)=1$ and $y(t)\to\tfrac12$
- C) $y(0^+)=1$ and $y(t)\to\tfrac32$
- D) $y(0^+)=0$ and $y(t)\to\tfrac32$

> [!success]- Answer
> **C.** $(sI-A)^{-1}$ has the rows $(s+3,\ 1)$ and $(-2,\ s)$, divided by $(s+1)(s+2)$. $C(sI-A)^{-1}B$ is the entry $(1,2)$: $\tfrac{1}{(s+1)(s+2)}$.
> So $G(s)=\tfrac{1}{(s+1)(s+2)}+1$ and $H(t)=e^{-t}-e^{-2t}+\delta(t)$.
> Step response: $y(t)=\int_0^t(e^{-\sigma}-e^{-2\sigma})\,d\sigma+1=\tfrac32-e^{-t}+\tfrac12e^{-2t}$.
> $y(0^+)=\tfrac32-1+\tfrac12=1$: the jump is the term $Du$. For $t\to\infty$: $y\to G(0)=\tfrac32$.
> - A: The term $D\mathbf{u}$ was forgotten. Then $y(0^+)=0$ and $y\to\tfrac12$.
> - B: $(sI+A)^{-1}$ was used: its entry $(1,2)$ is $\tfrac{-1}{s^2-3s+2}$, which is $-\tfrac12$ at $s=0$, so $y\to-\tfrac12+1=\tfrac12$.
> - D: $y(0^+)=C\mathbf{x}(0)=0$ forgets that $D\mathbf{u}$ jumps to $1$ at once. Zero state does not mean zero output.

## 3. Solution via the Laplace transform (slide 92)

### Q5 (slide 92, verify)

$A$ has the rows $(1,\ 1)$ and $(-1,\ 1)$, $B=(1,\ 0)^{\mathsf T}$, unit step, $\mathbf{x}(0)=\mathbf{0}$. So $\dot x_1=x_1+x_2+1$ and $\dot x_2=-x_1+x_2$. Write $P(t)=\tfrac12\bigl(e^{t}(\cos t+\sin t)-1\bigr)$ and $Q(t)=\tfrac12\bigl(e^{t}(\cos t-\sin t)-1\bigr)$. Which vector is the zero-state solution $\mathbf{x}_f(t)$? Check by substitution.

- A) $\mathbf{x}_f(t)=\bigl(P(t),\ Q(t)\bigr)^{\mathsf T}$
- B) $\mathbf{x}_f(t)=\bigl(Q(t),\ P(t)\bigr)^{\mathsf T}$
- C) $\mathbf{x}_f(t)=\bigl(P(t),\ P(t)\bigr)^{\mathsf T}$
- D) $\mathbf{x}_f(t)=\bigl(Q(t),\ Q(t)\bigr)^{\mathsf T}$

> [!success]- Answer
> **A.** All four vectors are $\mathbf{0}$ at $t=0$, so only the equations decide.
> Product rule: $\dot P=e^{t}\cos t$ and $\dot Q=-e^{t}\sin t$. Also $P+Q=e^{t}\cos t-1$ and $Q-P=-e^{t}\sin t$.
> Row 1: $\dot P=e^{t}\cos t=P+Q+1$. Row 2: $\dot Q=-e^{t}\sin t=-P+Q$. Both hold.
> - B: Entries swapped. Row 1: $\dot Q=-e^{t}\sin t$, but $Q+P+1=e^{t}\cos t$.
> - C: In entry 2 the numerator $s-2$ was split as $(s-1)+1$, not $(s-1)-1$. Row 1: $\dot P=e^{t}\cos t$, but $2P+1=e^{t}(\cos t+\sin t)$.
> - D: In entry 1 the numerator $s$ was split as $(s-1)-1$, not $(s-1)+1$. Row 1: $\dot Q=-e^{t}\sin t$, but $2Q+1=e^{t}(\cos t-\sin t)$.

### Q6 (slide 92, new system)

$A$ has the rows $(0,\ 1)$ and $(-4,\ 0)$, $B=(0,\ 1)^{\mathsf T}$, $\mathbf{x}(0)=\mathbf{0}$, unit step. Use the Laplace method. What is $x_1(t)$?

- A) $x_1(t)=\tfrac14(1-\cos 2t)$
- B) $x_1(t)=\tfrac12(1-\cos 2t)$
- C) $x_1(t)=-\tfrac14(1-\cos 2t)$
- D) $x_1(t)=1-\cos 2t$

> [!success]- Answer
> **A.** $(sI-A)^{-1}=\tfrac{1}{s^2+4}\begin{bmatrix}s&1\\-4&s\end{bmatrix}$, so $\hat{\mathbf{x}}=(sI-A)^{-1}B\tfrac1s=\tfrac{1}{s(s^2+4)}\begin{bmatrix}1\\s\end{bmatrix}$.
> Partial fractions: $\tfrac{1}{s(s^2+4)}=\tfrac{1}{4s}-\tfrac14\tfrac{s}{s^2+4}$, so $x_1=\tfrac14(1-\cos 2t)$. Also $x_2=\tfrac12\sin 2t$.
> Check: $\dot x_1=\tfrac12\sin 2t=x_2$ and $\dot x_2=\cos 2t=-4x_1+1$.
> - B: $\tfrac{1}{s^2+4}$ was taken as $\sin 2t$ (the factor $\tfrac12$ is missing). Then $x_1=\int_0^t\sin 2\sigma\,d\sigma=\tfrac12(1-\cos 2t)$.
> - C: $(sI+A)^{-1}$ was used. Its entry $(1,2)$ is $\tfrac{-1}{s^2+4}$, so the sign flips.
> - D: The partial fractions lost the factor $\tfrac14$: $\tfrac1s-\tfrac{s}{s^2+4}$ is $\tfrac{4}{s(s^2+4)}$, four times too big.

## 4. Modes of the zero-input response (slide 93)

### Q7 (slide 93, single mode)

$A$ has the rows $(-1,\ 2)$ and $(0,\ -3)$, and $u\equiv 0$. Which initial state $\mathbf{x}(0)$ gives a solution $\mathbf{x}(t)=e^{At}\mathbf{x}(0)$ that contains only the mode $e^{-3t}$? Scale $\mathbf{x}(0)$ so that $x_1(0)=1$.

- A) $\mathbf{x}(0)=(1,\ 0)^{\mathsf T}$
- B) $\mathbf{x}(0)=(1,\ -3)^{\mathsf T}$
- C) $\mathbf{x}(0)=(1,\ 1)^{\mathsf T}$
- D) $\mathbf{x}(0)=(1,\ -1)^{\mathsf T}$

> [!success]- Answer
> **D.** $A$ is triangular: eigenvalues $-1$ and $-3$, distinct, so the modes are $e^{-t}$ and $e^{-3t}$.
> Only an eigenvector of $-3$ excites $e^{-3t}$ alone. $(A+3I)\mathbf{v}=\mathbf{0}$ gives $2v_1+2v_2=0$, so $\mathbf{v}=(1,\ -1)^{\mathsf T}$ with $v_1=1$.
> Then $\mathbf{x}(t)=e^{-3t}(1,\ -1)^{\mathsf T}$.
> - A: $(1,\ 0)^{\mathsf T}$ is the eigenvector of $-1$. It gives $\mathbf{x}(t)=e^{-t}(1,\ 0)^{\mathsf T}$.
> - B: The companion-form eigenvector $(1,\ \lambda)^{\mathsf T}$ was used, but $A$ is not in companion form. It gives $\bigl(-2e^{-t}+3e^{-3t},\ -3e^{-3t}\bigr)^{\mathsf T}$: both modes.
> - C: $2v_1+2v_2=0$ was solved as $v_1=v_2$. It gives $\bigl(2e^{-t}-e^{-3t},\ e^{-3t}\bigr)^{\mathsf T}$: both modes.

### Q8 (slide 93, hidden mode)

$A$ has the rows $(-1,\ 2)$ and $(0,\ -3)$, $B=(0,\ 1)^{\mathsf T}$, $C=(0,\ 1)$, $D=0$. Which modes appear in the zero-input response $y(t)=Ce^{At}\mathbf{x}(0)$, over all $\mathbf{x}(0)$, and what is $G(s)$?

- A) Both $e^{-t}$ and $e^{-3t}$. $G(s)=\tfrac{1}{s+3}$.
- B) Only $e^{-3t}$. $G(s)=\tfrac{1}{s+3}$.
- C) Both $e^{-t}$ and $e^{-3t}$. $G(s)=\tfrac{1}{(s+1)(s+3)}$.
- D) Only $e^{-3t}$. $G(s)=\tfrac{1}{(s+1)(s+3)}$.

> [!success]- Answer
> **B.** $y=x_2$, and $\dot x_2=-3x_2+u$ does not contain $x_1$. So $y(t)=e^{-3t}x_2(0)$ for $u\equiv 0$: only $e^{-3t}$.
> $(sI-A)^{-1}=\tfrac{1}{(s+1)(s+3)}\begin{bmatrix}s+3&2\\0&s+1\end{bmatrix}$. $G(s)$ is the entry $(2,2)$: $\tfrac{s+1}{(s+1)(s+3)}=\tfrac{1}{s+3}$.
> The eigenvalue $-1$ is not a pole of $G$. The mode $e^{-t}$ lives in $x_1$, which $C$ does not see.
> - A: The modes rule says which functions *may* appear. Here $C$ gives $e^{-t}$ the coefficient $0$ for every $\mathbf{x}(0)$.
> - C: Both slips: all eigenvalue modes assumed in $y$, and the adjugate entry $s+1$ forgotten in $G$.
> - D: Only $\det(sI-A)$ was kept. The numerator $s+1$ of the adjugate entry was forgotten, so the cancellation was missed.
