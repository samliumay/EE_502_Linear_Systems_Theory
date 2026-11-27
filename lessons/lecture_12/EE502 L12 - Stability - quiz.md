---
course: EE 502 Linear System Theory
lesson: EE502 L12 - Stability
type: quiz
questions: 16
---

# EE502 L12 - Stability - quiz

Lesson note: [[EE502 L12 - Stability]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. A relaxed system has $\mathbf{x}(0)=\mathbf{0}$. BIBO-stable means: every bounded input gives a bounded output. The model is $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$. With $u=0$ it is marginally stable if $\mathbf{x}(t)$ stays bounded for every $\mathbf{x}(0)$, and asymptotically (internally) stable if $\mathbf{x}(t)\to\mathbf{0}$ for every $\mathbf{x}(0)$.

## 1. BIBO stability, single input and output (slides 115-117)

### Q1 (slide 115)

Three relaxed systems have the transfer functions (a) $\hat g(s)=\dfrac{s-2}{s^2+2s+5}$, (b) $\hat g(s)=\dfrac{1}{s(s+3)}$, (c) $\hat g(s)=\dfrac{s-1}{(s-1)(s+4)}$. Which of them are BIBO-stable?

- A) (a) and (b) only
- B) (b) and (c) only
- C) (a) and (c) only
- D) none of the three

> [!success]- Answer
> **C.** BIBO-stable iff all poles of the reduced $\hat g$ have $\operatorname{Re}s<0$. Zeros do not matter.
> (a) $s^2+2s+5=0$ gives $s=-1\pm2j$: stable. (b) Poles $0$ and $-3$: the pole $0$ is on the axis, not stable. (c) Cancel $s-1$: $\hat g=\dfrac{1}{s+4}$, pole $-4$: stable.
> - A: Two slips: the pole $0$ is accepted ($\operatorname{Re}\le0$ instead of $<0$), and (c) is judged from the unreduced denominator, which has the root $+1$.
> - B: Two slips: the pole $0$ is accepted, and (a) is rejected for its zero at $+2$.
> - D: Two slips: (a) is rejected for its zero at $+2$, and (c) is judged from the unreduced denominator.

### Q2 (slide 116)

A relaxed system has the impulse response $g(t)=\cos t$, so $y(t)=\displaystyle\int_0^t\cos(t-\tau)\,u(\tau)\,d\tau$. Find $y(t)$ for the bounded input $u(t)=\cos t$.

- A) $y(t)=\tfrac12t\cos t-\tfrac12\sin t$
- B) $y(t)=\tfrac12t\cos t+\tfrac12\sin t$
- C) $y(t)=\tfrac12\sin t$
- D) $y(t)=\tfrac12\cos t+\tfrac12\sin t$

> [!success]- Answer
> **B.** $\cos(t-\tau)\cos\tau=\tfrac12\bigl[\cos t+\cos(t-2\tau)\bigr]$.
> $\tfrac12\int_0^t\cos t\,d\tau=\tfrac12t\cos t$, since $\cos t$ is a constant in $\tau$.
> $\tfrac12\int_0^t\cos(t-2\tau)\,d\tau=\tfrac12\Bigl[-\tfrac12\sin(t-2\tau)\Bigr]_0^t=\tfrac12\sin t$.
> The term $\tfrac12t\cos t$ is unbounded, so the system is not BIBO-stable (poles $\pm j$, resonance).
> - A: Sign slip in the antiderivative: $+\tfrac12\sin(t-2\tau)$ instead of $-\tfrac12\sin(t-2\tau)$.
> - C: The constant term $\tfrac12\cos t$ is dropped, as if it averaged out.
> - D: $\int_0^t\cos t\,d\tau$ is taken as $\cos t$, without the factor $t$.

### Q3 (slide 117)

A relaxed system has $\hat g(s)=\dfrac{s+5}{(s+1)(s+3)^2}$. Expand it in partial fractions and find $g(t)$. Then bound $\int_0^\infty\lvert g(t)\rvert\,dt$ with the triangle inequality, that is, by the sum of the integrals of the absolute values of the terms of $g$. What is the value of this sum?

- A) $\tfrac59$
- B) $\tfrac{13}{9}$
- C) $\tfrac53$
- D) $\tfrac43$

> [!success]- Answer
> **B.** $\hat g(s)=\dfrac{1}{s+1}-\dfrac{1}{s+3}-\dfrac{1}{(s+3)^2}$, so $g(t)=e^{-t}-e^{-3t}-te^{-3t}$.
> Triangle bound: $\int_0^\infty e^{-t}dt+\int_0^\infty e^{-3t}dt+\int_0^\infty te^{-3t}dt=1+\tfrac13+\tfrac19=\tfrac{13}{9}$.
> The bound is finite, so the system is BIBO-stable. It is not tight: $g(t)\ge0$, so the exact area is $\hat g(0)=\tfrac59$.
> - A: The signs are kept: $1-\tfrac13-\tfrac19=\tfrac59=\hat g(0)$. That is the signed sum (here the exact area), not the triangle sum of absolute values the question asks for.
> - C: $\int_0^\infty te^{-3t}dt$ is taken as $\tfrac13$, like $\int_0^\infty e^{-3t}dt$. The right value is $\tfrac1{3^2}=\tfrac19$.
> - D: The term $te^{-3t}$ from the double pole is dropped: $1+\tfrac13$.

### Q4 (slide 117, steady state, beyond the slides)

A relaxed system has $\hat g(s)=\dfrac{4}{s+2}$. What does $y(t)$ approach for (a) $u(t)=3$ and (b) $u(t)=\sin 2t$?

- A) (a) $y\to12$, (b) $y\to\sqrt2\sin(2t+45^\circ)$
- B) (a) $y\to6$, (b) $y\to\sqrt2\sin(2t+45^\circ)$
- C) (a) $y\to12$, (b) $y\to\sqrt2\sin(2t-45^\circ)$
- D) (a) $y\to6$, (b) $y\to\sqrt2\sin(2t-45^\circ)$

> [!success]- Answer
> **D.** The pole is $-2$, so the system is BIBO-stable and the steady-state formulas hold.
> (a) $y\to\hat g(0)\cdot3=\tfrac42\cdot3=6$.
> (b) $\hat g(j2)=\dfrac{4}{2+2j}$: magnitude $\dfrac{4}{2\sqrt2}=\sqrt2$, phase $-\arctan\tfrac22=-45^\circ$. So $y\to\sqrt2\sin(2t-45^\circ)$.
> - A: Both slips of B and C.
> - B: The phase sign is lost. A factor in the denominator gives a negative phase.
> - C: $\hat g(0)$ is taken as the numerator $4$, without the denominator $s+2=2$.

## 2. BIBO stability, multivariable case (slide 118)

### Q5 (slide 118)

A relaxed system with 2 inputs and 2 outputs has $\hat g_{11}=\dfrac{1}{s+1}$, $\hat g_{12}=\dfrac{2}{s+3}$, $\hat g_{21}=\dfrac{1}{s^2+4s+13}$, $\hat g_{22}=\dfrac{s+1}{s(s+2)}$. Take the bounded input $u_1=0$, $u_2(t)=1$ for $t\ge0$. Find $y_2(t)$.

- A) $y_2(t)=\tfrac t2-\tfrac14\bigl(1-e^{-2t}\bigr)$
- B) $y_2(t)=\tfrac t2+\tfrac14\bigl(1-e^{-2t}\bigr)$
- C) $y_2(t)=\tfrac12-\tfrac12e^{-2t}$
- D) $y_2(t)=\tfrac12+\tfrac12e^{-2t}$

> [!success]- Answer
> **B.** $\hat g_{22}=\dfrac{1/2}{s}+\dfrac{1/2}{s+2}$ (residues $\tfrac{0+1}{0+2}=\tfrac12$ and $\tfrac{-2+1}{-2}=\tfrac12$), so $g_{22}(t)=\tfrac12+\tfrac12e^{-2t}$.
> With $u_2=1$: $y_2(t)=\int_0^tg_{22}(\tau)\,d\tau=\tfrac t2+\tfrac14\bigl(1-e^{-2t}\bigr)\to\infty$.
> The pole $0$ of $\hat g_{22}$ makes the system not BIBO-stable. The other three entries have poles $-1$, $-3$, $-2\pm3j$ and are fine. One bad entry is enough.
> - A: Sign slip in the residue at $-2$: $g_{22}=\tfrac12-\tfrac12e^{-2t}$, then integrated.
> - C: The residue sign slip of A, and the impulse response is given instead of the step response.
> - D: $g_{22}(t)$ itself, the response to an impulse, not to $u_2=1$. The step response is its integral.

## 3. Internal stability: poles and eigenvalues (slides 119-120)

### Q6 (slide 119)

$A$ has the rows $(0,\ 1)$ and $(2,\ -1)$, $B=(0,\ 1)^{\mathsf T}$, $C=(-1,\ 1)$, $D=0$. Is the system BIBO-stable? Is it internally (asymptotically) stable?

- A) BIBO-stable: yes. Internally stable: no.
- B) BIBO-stable: no. Internally stable: no.
- C) BIBO-stable: yes. Internally stable: yes.
- D) BIBO-stable: no. Internally stable: yes.

> [!success]- Answer
> **A.** $\det(sI-A)=s(s+1)-2=(s-1)(s+2)$: eigenvalues $1$ and $-2$.
> $(sI-A)^{-1}B=\dfrac{1}{(s-1)(s+2)}(1,\ s)^{\mathsf T}$, so $\hat g(s)=\dfrac{s-1}{(s-1)(s+2)}=\dfrac{1}{s+2}$.
> The only pole is $-2$: BIBO-stable. The eigenvalue $+1$ is hidden by the cancellation: not internally stable. For $\mathbf{x}(0)=(1,1)^{\mathsf T}$, $u=0$, the state is $e^{t}(1,1)^{\mathsf T}$ but $y=0$.
> - B: BIBO judged from the eigenvalues of $A$. The eigenvalue $+1$ is not a pole of $\hat g$.
> - C: Internal stability judged from the poles of $\hat g$. The cancelled eigenvalue $+1$ is missed.
> - D: The two tests are swapped: BIBO from the eigenvalues, internal from the poles.

### Q7 (slide 120)

$A_1=\operatorname{diag}(0,\ 0,\ -1)$. $A_2$ has the rows $(0,\ 1,\ 0)$, $(0,\ 0,\ 0)$, $(0,\ 0,\ -1)$. Both have the eigenvalues $0,\ 0,\ -1$. Classify $\dot{\mathbf{x}}=A_1\mathbf{x}$ and $\dot{\mathbf{x}}=A_2\mathbf{x}$ (unstable means: not marginally stable).

- A) $A_1$ marginally stable, $A_2$ unstable
- B) $A_1$ marginally stable, $A_2$ marginally stable
- C) $A_1$ unstable, $A_2$ unstable
- D) $A_1$ unstable, $A_2$ marginally stable

> [!success]- Answer
> **A.** The double eigenvalue $0$ is on the imaginary axis, so its largest Jordan block decides. Independent eigenvectors for $\lambda=0$: $3-\operatorname{rank}A$.
> $A_1$: rank $1$, so $2$ eigenvectors $=$ multiplicity $2$. Blocks $1\times1$, $e^{A_1t}=\operatorname{diag}(1,\ 1,\ e^{-t})$ is bounded: marginally stable.
> $A_2$: rank $2$, so $1$ eigenvector. One $2\times2$ block, $e^{A_2t}$ has the entry $t$: unstable.
> - B: The repeated eigenvalue $0$ is judged marginally stable without checking the Jordan block size.
> - C: Every repeated eigenvalue on the axis is judged unstable. Index $1$ ($1\times1$ blocks) is enough.
> - D: The number of eigenvectors is taken as $\operatorname{rank}A$ instead of $3-\operatorname{rank}A$.

## 4. Lyapunov theorem (slides 121-123)

### Q8 (slide 121)

Scalar case: $\dot x=-ax$ with $a>0$ and $N=n>0$. Compute $M=\displaystyle\int_0^\infty e^{A^{\mathsf T}t}Ne^{At}\,dt$. For $a<0$ this integral diverges. What does the equation $A^{\mathsf T}M+MA=-N$ give then?

- A) $M=\dfrac{n}{a}$. For $a<0$ the equation has no solution.
- B) $M=\dfrac{n}{2a}$. For $a<0$ it still gives $M=\dfrac{n}{2a}<0$.
- C) $M=\dfrac{n}{a}$. For $a<0$ it still gives $M=\dfrac{n}{a}<0$.
- D) $M=\dfrac{n}{2a}$. For $a<0$ the equation has no solution.

> [!success]- Answer
> **B.** $A=-a$, so $e^{A^{\mathsf T}t}Ne^{At}=n\,e^{-at}e^{-at}=n\,e^{-2at}$ and $M=\int_0^\infty n\,e^{-2at}dt=\dfrac{n}{2a}>0$.
> Check: $A^{\mathsf T}M+MA=-2aM=-n$.
> For $a<0$ the linear equation $-2aM=-n$ still has the unique solution $M=\dfrac{n}{2a}$, now negative. A negative $M$ signals an unstable $A$.
> - A: Only one factor $e^{-at}$ is kept (or only the term $MA$), which loses the $2$. A divergent integral does not mean the algebraic equation has no solution.
> - C: The lost factor $2$ of A. The part about $a<0$ is right.
> - D: $M$ is right, but the equation $-2aM=-n$ is solvable for every $a\ne0$.

### Q9 (slide 122)

$A$ has the rows $(-1,\ 2)$ and $(0,\ -3)$. Solve $A^{\mathsf T}M+MA=-I$ for the symmetric $M$.

- A) $M$ with rows $(\tfrac23,\ \tfrac1{12})$, $(\tfrac1{12},\ \tfrac16)$
- B) $M$ with rows $(-\tfrac12,\ -\tfrac14)$, $(-\tfrac14,\ -\tfrac13)$
- C) $M$ with rows $(-\tfrac23,\ -\tfrac1{12})$, $(-\tfrac1{12},\ -\tfrac16)$
- D) $M$ with rows $(\tfrac12,\ \tfrac14)$, $(\tfrac14,\ \tfrac13)$

> [!success]- Answer
> **D.** With $M$ having rows $(m_1,\ m_2)$, $(m_2,\ m_3)$: $A^{\mathsf T}M+MA$ has the entries $(1,1)$: $-2m_1$, $(1,2)$: $2m_1-4m_2$, $(2,2)$: $4m_2-6m_3$.
> $-2m_1=-1$ gives $m_1=\tfrac12$. $2m_1-4m_2=0$ gives $m_2=\tfrac14$. $4m_2-6m_3=-1$ gives $m_3=\tfrac13$.
> Minors $\tfrac12>0$, $\det M=\tfrac16-\tfrac1{16}=\tfrac5{48}>0$: $M>0$, so $A$ is Hurwitz (eigenvalues $-1,-3$).
> - A: $AM+MA^{\mathsf T}=-I$ is solved instead. That is the Lyapunov equation of $A^{\mathsf T}$, not of $A$.
> - B: Sign slip: $A^{\mathsf T}M+MA=+I$ is solved, which gives $-M$.
> - C: Both slips: $AM+MA^{\mathsf T}$ and $+I$.

### Q10 (slide 122, lemma)

$A=\operatorname{diag}(1,\ -1)$ and $N=I$. How many symmetric solutions $M$ does $A^{\mathsf T}M+MA=-I$ have?

- A) Infinitely many: $m_2$ is free, because $\lambda_1+\lambda_2=0$.
- B) Exactly one, $M=\operatorname{diag}(-\tfrac12,\ \tfrac12)$, since no $\lambda_i$ is $0$.
- C) None, because $A$ is not Hurwitz.
- D) None, because $\lambda_1+\lambda_2=0$ makes the equations inconsistent.

> [!success]- Answer
> **A.** $A^{\mathsf T}M+MA$ has the entries $(1,1)$: $2m_1$, $(1,2)$: $m_2-m_2=0$, $(2,2)$: $-2m_3$.
> Equations: $2m_1=-1$, $0=0$, $-2m_3=-1$. So $m_1=-\tfrac12$, $m_3=\tfrac12$, and $m_2$ is free.
> Lemma: the solution is unique iff $\lambda_i+\lambda_j\ne0$ for all pairs. Here $1+(-1)=0$. No solution is positive definite ($m_1<0$).
> - B: The condition is on the sums $\lambda_i+\lambda_j$, not on single eigenvalues. The $(1,2)$ equation $0=0$ does not fix $m_2$.
> - C: A non-Hurwitz $A$ can still give solutions. They are only not positive definite.
> - D: A zero sum can make the equations inconsistent, but here the right-hand entry $(1,2)$ of $-I$ is $0$, so $0=0$ holds.

### Q11 (slide 123)

Find the mistake in this claim: "For the $A$ with rows $(1,\ 2)$ and $(0,\ -3)$ the equation $A^{\mathsf T}M+MA=-I$ has a unique solution $M$, so $A$ is Hurwitz."

- A) No mistake: the equation has a unique solution only for a Hurwitz $A$.
- B) The solution is not unique, since the eigenvalue $1$ is positive.
- C) Using only $N=I$ is the mistake: the test needs every $N>0$.
- D) Uniqueness is not the test. Here $m_1=-\tfrac12<0$, so $A$ is not Hurwitz.

> [!success]- Answer
> **D.** The test is $M>0$ (Remark 2: one $N>0$, for example $N=I$, is enough).
> Entries: $(1,1)$: $2m_1=-1$, $(1,2)$: $2m_1-2m_2=0$, $(2,2)$: $4m_2-6m_3=-1$. So $m_1=m_2=-\tfrac12$, $m_3=-\tfrac16$.
> $m_1<0$ and $\det M=\tfrac1{12}-\tfrac14=-\tfrac16<0$: $M$ is not positive definite. Indeed the eigenvalues are $1$ and $-3$.
> - A: Uniqueness needs only $\lambda_i+\lambda_j\ne0$. Here the sums are $2,-2,-6$, so a non-Hurwitz $A$ has a unique $M$.
> - B: The solution is unique. The sums $2,-2,-6$ are all nonzero.
> - C: One $N>0$ is enough. The mistake is that $M>0$ was never checked.

## 5. Routh-Hurwitz criterion (slide 124)

### Q12 (slide 124)

A $4\times4$ matrix $A$ is in companion form: ones at the places $(1,2)$, $(2,3)$, $(3,4)$, last row $(-5,\ -4,\ -3,\ -2)$, zeros elsewhere. Build the Routh table of $\det(sI-A)$. What is its first column, and how many eigenvalues are in the right half-plane?

- A) First column $1,\ 5,\ \tfrac{17}{5},\ \tfrac1{17},\ 2$; no eigenvalue
- B) First column $1,\ 2,\ 1,\ 6,\ 5$; no eigenvalue
- C) First column $1,\ 2,\ 1,\ -6,\ 5$; two eigenvalues
- D) First column $1,\ 2,\ 1,\ -6,\ 5$; one eigenvalue

> [!success]- Answer
> **C.** The last row holds the coefficients with a minus sign, lowest power first: $\det(sI-A)=s^4+2s^3+3s^2+4s+5$.
> Rows $1,3,5$ and $2,4$. Then $b_1=\tfrac{2\cdot3-1\cdot4}{2}=1$, $b_2=\tfrac{2\cdot5-0}{2}=5$, $c_1=\tfrac{1\cdot4-2\cdot5}{1}=-6$, last $5$.
> Signs $1\to-6$ and $-6\to5$: two changes, two eigenvalues in the right half-plane (about $0.288\pm j1.416$).
> - A: The row is read highest power first: $s^4+5s^3+4s^2+3s+2$. That is a different polynomial.
> - B: The order in $c_1$ is swapped: $\tfrac{2\cdot5-1\cdot4}{1}=6$.
> - D: The negative entries are counted ($1$) instead of the sign changes ($2$).

## 6. BIBO stability of LTV systems (slides 126-127)

### Q13 (slide 126)

Relaxed LTV systems $y(t)=\displaystyle\int_0^tg(t,\tau)u(\tau)\,d\tau$. Decide BIBO stability for (a) $g(t,\tau)=e^{-2t+\tau}$ and (b) $g(t,\tau)=t\,e^{-(t-\tau)}$.

- A) (a) BIBO-stable, (b) not BIBO-stable
- B) (a) not BIBO-stable, (b) BIBO-stable
- C) (a) BIBO-stable, (b) BIBO-stable
- D) (a) not BIBO-stable, (b) not BIBO-stable

> [!success]- Answer
> **A.** The test: one $K$ with $\int_0^t\lvert g(t,\tau)\rvert\,d\tau\le K$ for all $t\ge0$.
> (a) $\int_0^te^{-2t+\tau}d\tau=e^{-t}-e^{-2t}$, largest at $t=\ln2$ with value $\tfrac14$. $K=\tfrac14$ works.
> (b) $\int_0^tt\,e^{-(t-\tau)}d\tau=t(1-e^{-t})$, which grows like $t$. No single $K$.
> - B: Both slips of C and D.
> - C: In (b) the integral is finite for each $t$, but one $K$ must bound it for all $t$.
> - D: (a) is rejected because $e^{\tau}$ grows. The factor $e^{-2t}$ with $\tau\le t$ keeps the integral at most $\tfrac14$.

### Q14 (slide 127)

$A$ has the rows $(1,\ 1)$ and $(0,\ 1)$. Find the induced 2-norm $\lVert A\rVert_2$. Then decide: is the relaxed system with $G(t,\tau)=\bigl(e^{-(t-\tau)},\ \tfrac{1}{1+\tau}\bigr)$ BIBO-stable ($t_0=0$)?

- A) $\lVert A\rVert_2=\tfrac{3+\sqrt5}{2}$; $G$ is BIBO-stable
- B) $\lVert A\rVert_2=\tfrac{3+\sqrt5}{2}$; $G$ is not BIBO-stable
- C) $\lVert A\rVert_2=\tfrac{1+\sqrt5}{2}$; $G$ is not BIBO-stable
- D) $\lVert A\rVert_2=\tfrac{1+\sqrt5}{2}$; $G$ is BIBO-stable

> [!success]- Answer
> **C.** $A^{\mathsf T}A$ has the rows $(1,\ 1)$, $(1,\ 2)$. $\lambda^2-3\lambda+1=0$ gives $\lambda_{\max}=\tfrac{3+\sqrt5}{2}$, so $\lVert A\rVert_2=\sqrt{\tfrac{3+\sqrt5}{2}}=\tfrac{1+\sqrt5}{2}\approx1.618$. (For comparison $\lVert A\rVert_F=\sqrt3$.)
> $G$: $\int_0^te^{-(t-\tau)}d\tau=1-e^{-t}\le1$, but $\int_0^t\tfrac{d\tau}{1+\tau}=\ln(1+t)\to\infty$. One entry fails: not BIBO-stable.
> - A: Both slips of B and D.
> - B: The square root is forgotten: $\lambda_{\max}(A^{\mathsf T}A)$ is $\lVert A\rVert_2^2$.
> - D: $\tfrac{1}{1+\tau}\to0$ is taken as enough. Its integral still grows like $\ln(1+t)$.

## 7. Stability of LTV state representations (slides 128-129)

### Q15 (slide 128)

$\dot x=-2x+e^{t}u$ with $t_0=0$, relaxed. Is it BIBO-stable for the output (a) $y=x$ and (b) $y=e^{-t}x+t\,u$?

- A) (a) BIBO-stable, (b) BIBO-stable
- B) (a) BIBO-stable, (b) not BIBO-stable
- C) (a) not BIBO-stable, (b) BIBO-stable
- D) (a) not BIBO-stable, (b) not BIBO-stable

> [!success]- Answer
> **D.** $\Phi(t,\tau)=e^{-2(t-\tau)}$, $B(\tau)=e^{\tau}$.
> (a) $\int_0^te^{-2(t-\tau)}e^{\tau}d\tau=\tfrac{e^{t}-e^{-2t}}{3}\to\infty$: not BIBO-stable.
> (b) $\int_0^te^{-t}e^{-2(t-\tau)}e^{\tau}d\tau=\tfrac{1-e^{-3t}}{3}\le\tfrac13$, but $\lvert D(t)\rvert=t$ is unbounded: not BIBO-stable ($u=1$ gives the term $t$).
> - A: Both slips of B and C.
> - B: (a) is judged from $\dot x=-2x$ alone. It is asymptotically stable, but $B(t)=e^{t}$ is unbounded.
> - C: Only the integral is checked in (b). The condition $\lvert D(t)\rvert\le M_2$ fails.

### Q16 (slide 129)

Classify the scalar systems (a) $\dot x=(\cos t)\,x$ and (b) $\dot x=(-1+\cos t)\,x$. "Marginally stable only" means bounded for all $t_0$ and $t\ge t_0$, but not going to $0$.

- A) (a) unstable, (b) asymptotically stable
- B) (a) marginally stable only, (b) marginally stable only
- C) (a) marginally stable only, (b) asymptotically stable
- D) (a) unstable, (b) marginally stable only

> [!success]- Answer
> **C.** Scalar case: $\Phi(t,t_0)=\exp\Bigl(\int_{t_0}^ta(\sigma)\,d\sigma\Bigr)$.
> (a) $\Phi=e^{\sin t-\sin t_0}\in[e^{-2},\ e^{2}]$: bounded, does not go to $0$. Marginally stable only.
> (b) $\Phi=e^{-(t-t_0)}e^{\sin t-\sin t_0}\le e^{2}e^{-(t-t_0)}\to0$: asymptotically stable.
> - A: The frozen eigenvalue $\cos t$ is positive half of the time, but $\Phi$ stays bounded. Only $\Phi$ decides.
> - B: The frozen eigenvalue $-1+\cos t$ reaches $0$, but $\Phi$ still decays like $e^{-(t-t_0)}$.
> - D: Both slips of A and B.
