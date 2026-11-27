---
course: EE 502 Linear System Theory
lesson: EE502 L02 - LTI models and linearization
type: quiz
questions: 21
---

# EE502 L02 - LTI models and linearization - quiz

Lesson note: [[EE502 L02 - LTI models and linearization]]. One question per check question of the lesson. Pick an option, then open the answer.

## 1. Linearity and input-linearity (slide 15)

### Q1 (slide 15)

![[ee502_eee501alllecturenotesabo_p015.jpg]]

The input is written as a staircase $u(t)\cong\sum_i u(t_i)\,\delta_\Delta(t-t_i)\,\Delta$, where $\delta_\Delta(t-t_i)$ is a pulse of height $1/\Delta$ on $[t_i,\,t_i+\Delta)$. Take $u(t)=t^2$, $\Delta=0.1$ and $t_i=0.5$. What is the height of the term $u(t_i)\,\delta_\Delta(t-t_i)\,\Delta$, and what does the factor $\Delta$ do?

- A) Height $2.5$. The factor $\Delta$ cancels the pulse height $1/\Delta$.
- B) Height $0.25$. The factor $\Delta$ cancels the pulse height $1/\Delta$.
- C) Height $0.25$. The factor $\Delta$ makes the area of each block equal to 1.
- D) Height $2.5$. The factor $\Delta$ makes the area of each block equal to 1.

> [!success]- Answer
> **B.** The pulse has height $1/\Delta=10$. $u(t_i)=0.5^2=0.25$.
> Term height: $0.25\cdot10\cdot0.1=0.25$. The factor $\Delta$ cancels the $1/\Delta$, so each block has height $u(t_i)$ and the blocks form the staircase.
> - A: $2.5=0.25\cdot10$ forgets the factor $\Delta$. Then the staircase would be 10 times too high.
> - C: The height is right, but the block area is $u(t_i)\,\Delta=0.025$, not 1. Only the pulse $\delta_\Delta$ has area 1.
> - D: Both parts are wrong: $\Delta$ is forgotten in the height, and the block area is not 1.

## 2. Impulse response (slides 16-18)

### Q2 (slide 16)

A system has impulse response $g(t,\tau)=\tau\,e^{-(t-\tau)}$ for $t\ge\tau$ and $0$ otherwise. Here $t$ is the time of observation and $\tau$ the time of the impulse. Find $g(3,2)$ and $g(2,1)$, and decide what the two values show.

- A) $g(3,2)\approx0.736$, $g(2,1)\approx0.368$. The system is time-invariant.
- B) $g(3,2)\approx1.104$, $g(2,1)\approx0.736$. The system is time-invariant.
- C) $g(3,2)\approx1.104$, $g(2,1)\approx0.736$. The system is time-varying.
- D) $g(3,2)\approx0.736$, $g(2,1)\approx0.368$. The system is time-varying.

> [!success]- Answer
> **D.** $g(3,2)=2\,e^{-1}\approx0.736$ and $g(2,1)=1\cdot e^{-1}\approx0.368$.
> Both are seen 1 second after the impulse, but the values differ. The response depends on when the impulse is applied, so the system is time-varying.
> - A: The values are right, but equal elapsed time with different outputs means time-varying.
> - B: The factor in front was taken as $t$ instead of $\tau$ ($3e^{-1}$, $2e^{-1}$), and the conclusion is wrong too.
> - C: The conclusion is right, but the factor in front is $\tau$ (impulse time), not $t$.

### Q3 (slide 17)

A causal system has $g(t,\tau)=e^{-2(t-\tau)}$ for $t\ge\tau$ and $0$ otherwise. It is relaxed at $t_0=1$, and $u(t)=4$ for $t\ge1$. The output is $y(t)=\int_{t_0}^{t}g(t,\tau)u(\tau)\,d\tau$. Find $y(t)$ for $t\ge1$ and $y(2)$.

- A) $y(t)=4-4e^{-2(t-1)}$, $y(2)\approx3.459$
- B) $y(t)=4-4e^{-2t}$, $y(2)\approx3.927$
- C) $y(t)=2-2e^{-2t}$, $y(2)\approx1.963$
- D) $y(t)=2-2e^{-2(t-1)}$, $y(2)\approx1.729$

> [!success]- Answer
> **D.** $y(t)=4e^{-2t}\int_1^t e^{2\tau}\,d\tau=4e^{-2t}\cdot\dfrac{e^{2t}-e^{2}}{2}=2-2e^{-2(t-1)}$.
> $y(2)=2-2e^{-2}\approx1.729$. Lower limit $1$: relaxed at $t_0=1$. Upper limit $t$: causal.
> - A: The factor $\tfrac12$ from $\int e^{2\tau}d\tau=\tfrac12e^{2\tau}$ is lost.
> - B: Both slips: the factor $\tfrac12$ is lost and the lower limit is $0$ instead of $t_0=1$.
> - C: The lower limit is $0$ instead of $t_0=1$. The input starts at $t=1$.

### Q4 (slide 18)

A relaxed, causal system has 2 inputs and 3 outputs: $\mathbf{y}(t)=\int_{t_0}^{t}G(t,\tau)\,\mathbf{u}(\tau)\,d\tau$ with $\mathbf{u}\in\mathbb{R}^2$, $\mathbf{y}\in\mathbb{R}^3$, and $g_{ij}$ is the entry in row $i$, column $j$. What is the size of $G$, and which entry describes how input 2 acts on output 3?

- A) $G$ is $2\times3$. The entry is $g_{32}$.
- B) $G$ is $3\times2$. The entry is $g_{32}$.
- C) $G$ is $2\times3$. The entry is $g_{23}$.
- D) $G$ is $3\times2$. The entry is $g_{23}$.

> [!success]- Answer
> **B.** $G\mathbf{u}$ must be a $3$-vector and $\mathbf{u}$ is a $2$-vector, so $G$ is $q\times p=3\times2$.
> $y_3=\int\bigl(g_{31}u_1+g_{32}u_2\bigr)d\tau$, so input 2 reaches output 3 through $g_{32}$ (row = output, column = input).
> - A: The size is swapped. A $2\times3$ matrix cannot multiply a $2$-vector.
> - C: Size and index are both swapped (input $\times$ output instead of output $\times$ input).
> - D: The size is right, but $g_{23}$ is row 2, column 3. Column 3 does not exist with 2 inputs.

## 3. Time invariance (slides 19-20)

### Q5 (slide 19)

![[ee502_eee501alllecturenotesabo_p019.jpg]]

The figure shows the test: apply the shifted input $u(t-T)$ with the same state, and compare the response with the shifted output $y(t-T)$. Apply it to $y(t)=e^{-t}u(t)$ with $T>0$. What is the response to $u(t-T)$, and what is the verdict?

- A) Response $e^{-t}u(t-T)$. Not time-invariant.
- B) Response $e^{-(t-T)}u(t-T)$. Time-invariant.
- C) Response $e^{-t}u(t-T)$. Time-invariant.
- D) Response $e^{-(t-T)}u(t-T)$. Not time-invariant.

> [!success]- Answer
> **A.** The system multiplies its present input by $e^{-t}$, so the input $u(t-T)$ gives $e^{-t}u(t-T)$.
> The shifted output is $y(t-T)=e^{-(t-T)}u(t-T)=e^{T}e^{-t}u(t-T)$. They differ by $e^{T}\ne1$: not time-invariant.
> - B: $e^{-(t-T)}u(t-T)$ is the shifted output $y(t-T)$, not the response. Comparing it with itself always passes.
> - C: The response is right, but it is not equal to $y(t-T)$, so the test fails.
> - D: The verdict is right, but the response was replaced by the shifted output.

### Q6 (slide 20)

A causal time-invariant system has $g(t,0)=5e^{-3t}$ for $t\ge0$, so $g(t,\tau)=g(t-\tau)$. Find $g(5,7)$ and the output for $u(t)=e^{-t}$, $t\ge0$, with zero initial conditions.

- A) $g(5,7)=5e^{6}$; $y(t)=\tfrac52\,e^{-t}$
- B) $g(5,7)=0$; $y(t)=\tfrac52\,e^{-t}$
- C) $g(5,7)=5e^{6}$; $y(t)=\tfrac52\bigl(e^{-t}-e^{-3t}\bigr)$
- D) $g(5,7)=0$; $y(t)=\tfrac52\bigl(e^{-t}-e^{-3t}\bigr)$

> [!success]- Answer
> **D.** $g(5,7)=g(-2)=0$: causal means no response before the impulse. (Also $g(7,5)=g(2)=5e^{-6}$.)
> $y(t)=\int_0^t5e^{-3(t-\tau)}e^{-\tau}d\tau=5e^{-3t}\cdot\dfrac{e^{2t}-1}{2}=\tfrac52\bigl(e^{-t}-e^{-3t}\bigr)$.
> - A: $5e^{6}$ puts $-2$ into $5e^{-3t}$ and ignores causality. The $y$ forgets the lower limit term $-1$.
> - B: $g(5,7)$ is right, but the lower limit $\tau=0$ of $\int e^{2\tau}d\tau$ was dropped. Then $y(0)\ne0$.
> - C: $y$ is right, but $g(t)=0$ for $t<0$ in a causal system.

## 4. Example: feedback loop with a unit delay (slide 21)

### Q7 (slide 21)

Negative feedback with gain $a$ and a unit delay: $y(t)=\sum_{i\ge1}(-1)^{i-1}a^i\,r(t-i)$. Take $a=2$ and the unit step $r(t)=1$ for $t\ge0$. Find $y$ on $[1,2)$, $[2,3)$, $[3,4)$, and say what happens as $t$ grows.

- A) $2,\ -4,\ 8$. The output settles at $a/(1+a)=2/3$.
- B) $2,\ -4,\ 8$. The sign alternates and the size grows.
- C) $2,\ -2,\ 6$. The sign alternates and the size grows.
- D) $2,\ -2,\ 6$. The output settles at $a/(1+a)=2/3$.

> [!success]- Answer
> **C.** Term $i$ is on when $t\ge i$. $[1,2)$: $2$. $[2,3)$: $2-4=-2$. $[3,4)$: $2-4+8=6$. Next: $6-16=-10$.
> Each trip around the loop multiplies the echo by $-a=-2$. The echoes die out only when $\lvert a\rvert<1$, so here they grow.
> - A: These are the single echoes $(-1)^{i-1}2^i$, not their running sum, and $a/(1+a)$ is the limit only for $\lvert a\rvert<1$.
> - B: The behaviour is right, but $y$ is the sum of all echoes switched on so far, not the newest echo.
> - D: The values are right, but $a/(1+a)$ needs $\lvert a\rvert<1$. With $a=2$ the series diverges.

## 5. Transfer function and transfer matrix (slides 22-23)

### Q8 (slide 22)

In the derivation of $\hat y=\hat g\hat u$ the substitution $\mu=t-\tau$ gives an inner integral from $\mu=-\tau$, and the next line starts it at $\mu=0$. Take $g(t)=2e^{-3t}$, $t\ge0$. Why is the move allowed, and what is the unit-step response?

- A) Causal: $g(\mu)=0$ for $\mu<0$. $y(t)=\tfrac23\bigl(1-e^{-3t}\bigr)$.
- B) Relaxed: $u(\tau)=0$ for $\tau<0$. $y(t)=2\bigl(1-e^{-3t}\bigr)$.
- C) Causal: $g(\mu)=0$ for $\mu<0$. $y(t)=2\bigl(1-e^{-3t}\bigr)$.
- D) Relaxed: $u(\tau)=0$ for $\tau<0$. $y(t)=\tfrac23\bigl(1-e^{-3t}\bigr)$.

> [!success]- Answer
> **A.** The cut part is $\int_{-\tau}^{0}g(\mu)\dots d\mu$, and $g(\mu)=0$ for $\mu<0$ by causality.
> $\hat g=\dfrac{2}{s+3}$, $\hat y=\dfrac{2}{s(s+3)}=\dfrac{2/3}{s}-\dfrac{2/3}{s+3}$, so $y=\tfrac23\bigl(1-e^{-3t}\bigr)$.
> - B: Relaxedness fixes the limits in $\tau$, not in $\mu$. The step response also loses the division by $3$ in the partial fractions.
> - C: The reason is right, but $\hat y=\dfrac{2}{s(s+3)}$ has residue $2/3$ at $s=0$, not $2$.
> - D: The response is right, but the cut integral is over $g(\mu)$, so causality is the reason.

### Q9 (slide 23)

A 2-input, 2-output system has $g_{11}=e^{-t}$, $g_{12}=0$, $g_{21}=2$, $g_{22}=e^{-3t}$ for $t\ge0$ (row = output, column = input). Input 1 is a unit step and input 2 is $\delta(t)$. What is $y_2(t)$ for $t\ge0$?

- A) $y_2(t)=2t+e^{-3t}$
- B) $y_2(t)=2+e^{-3t}$
- C) $y_2(t)=e^{-3t}$
- D) $y_2(t)=2t+\tfrac13-\tfrac13e^{-3t}$

> [!success]- Answer
> **A.** $\hat g_{21}=\dfrac2s$, $\hat g_{22}=\dfrac{1}{s+3}$, $\hat u_1=\dfrac1s$, $\hat u_2=1$.
> $\hat y_2=\hat g_{21}\hat u_1+\hat g_{22}\hat u_2=\dfrac{2}{s^2}+\dfrac{1}{s+3}$, so $y_2=2t+e^{-3t}$.
> - B: $\hat g_{21}$ was taken as $2$ instead of the Laplace transform $2/s$ of the constant $2$.
> - C: Column 2 was used instead of row 2: $\hat g_{12}\hat u_1+\hat g_{22}\hat u_2$.
> - D: Input 2 was treated as a step ($\hat u_2=1/s$) instead of an impulse.

## 6. Rational vs irrational, poles and zeros (slides 24-26)

### Q10 (slide 24)

A room adds one echo: $y(t)=u(t)+0.5\,u(t-2)$. Find $\hat g(s)$ and decide if the system is lumped or distributed.

- A) $\hat g(s)=1+0.5\,e^{2s}$. Distributed.
- B) $\hat g(s)=1+0.5\,e^{2s}$. Lumped.
- C) $\hat g(s)=1+0.5\,e^{-2s}$. Lumped.
- D) $\hat g(s)=1+0.5\,e^{-2s}$. Distributed.

> [!success]- Answer
> **D.** $g(t)=\delta(t)+0.5\,\delta(t-2)$. Sifting: $\int_0^\infty\delta(t-2)e^{-st}dt=e^{-2s}$.
> $\hat g=1+0.5\,e^{-2s}$ is not a ratio of polynomials. A lumped system always has a rational $\hat g$, so this one is distributed.
> - A: A delay of $2$ gives $e^{-2s}$, not $e^{+2s}$ (sign slip).
> - B: Wrong sign in the exponent and wrong class.
> - C: $\hat g$ is right, but it is irrational, which rules out lumped.

### Q11 (slide 25)

Take $\hat g(s)=\dfrac{3s^2+3}{s^2+2s+5}$. Find $\hat g(\infty)$, the poles and the zeros.

- A) $\hat g(\infty)=3$; poles $-1\pm2j$; zeros $\pm j$
- B) $\hat g(\infty)=3$; poles $1\pm2j$; zeros $\pm1$
- C) $\hat g(\infty)=3/5$; poles $-1\pm2j$; zeros $\pm1$
- D) $\hat g(\infty)=3/5$; poles $1\pm2j$; zeros $\pm j$

> [!success]- Answer
> **A.** $\deg N=\deg D=2$: biproper, $\hat g(\infty)=3/1=3$ (leading coefficients).
> Poles: $s=\dfrac{-2\pm\sqrt{4-20}}{2}=-1\pm2j$. Zeros: $3s^2+3=0$, $s^2=-1$, $s=\pm j$. No common root, nothing cancels.
> - B: Sign slip in the poles ($-b/2a$ is $-1$), and $s^2=-1$ was solved as $s^2=1$.
> - C: $3/5$ is $\hat g(0)$ (constant terms), not $\hat g(\infty)$. And $s^2=-1$ gives $\pm j$, not $\pm1$.
> - D: $3/5$ is $\hat g(0)$, and the poles have a sign slip.

### Q12 (slide 26)

A transfer function has a double zero at $-1$, poles at $-2\pm j$ and $\hat g(0)=2$. In zero-pole-gain form $\hat g(s)=k\,\dfrac{(s+1)^2}{(s+2-j)(s+2+j)}$. Find $k$. Then remove one of the two zeros (same $k$): how many zeros at infinity does the new $\hat g$ have?

- A) $k=2$; no zeros at infinity
- B) $k=10$; one zero at infinity
- C) $k=2$; one zero at infinity
- D) $k=10$; no zeros at infinity

> [!success]- Answer
> **B.** $(s+2-j)(s+2+j)=s^2+4s+5$. At $s=0$: $k\cdot\dfrac15=2$, so $k=10$.
> Without one zero, $\hat g=k\dfrac{s+1}{s^2+4s+5}$: $\deg D-\deg N=1$, strictly proper, one zero at infinity.
> - A: $k=\hat g(0)$ forgets the factor $1/5$, and removing a zero does change properness.
> - C: The count is right, but $\hat g(0)=k/5$, not $k$.
> - D: $k$ is right, but "no zeros at infinity" holds for the original $\hat g$ (degree 2 over 2), not for the new one.

## 7. Transfer matrix terminology, blocking zeros (slides 27-28)

### Q13 (slide 27)

$\hat G(s)=\begin{bmatrix}\dfrac{s-1}{s+2}&\dfrac{s-1}{(s+2)(s+3)}\\0&\dfrac{2(s-1)}{s+3}\end{bmatrix}$. Find the poles (with multiplicity), the class (proper, strictly proper or biproper) and the blocking zeros.

- A) Poles $-2,-3$; biproper; blocking zero $1$
- B) Poles $-2,-2,-3,-3$; strictly proper; blocking zero $1$
- C) Poles $-2,-2,-3,-3$; biproper; no blocking zero
- D) Poles $-2,-3$; strictly proper; no blocking zero

> [!success]- Answer
> **A.** The least common multiple of the denominators is $(s+2)(s+3)$: poles $-2$ and $-3$.
> $K=\hat G(\infty)=\begin{bmatrix}1&0\\0&2\end{bmatrix}$: nonzero and $\det K=2\ne0$, so biproper.
> $\hat G(1)=0$: every entry vanishes at $s=1$ ($\hat g_{21}$ is zero everywhere). Blocking zero $1$.
> - B: The product of the denominators is not their lcm, and $K\ne0$, so not strictly proper.
> - C: Product instead of lcm, and $\hat g_{21}\equiv0$ does not prevent $\hat G(1)=0$.
> - D: $\hat g_{12}\to0$ does not make $K=0$; the diagonal limits are $1$ and $2$. And $\hat G(1)=0$.

### Q14 (slide 28)

For $\hat g(s)=\dfrac{s-z_0}{s-p}$ and $u=e^{zt}$ ($z\ne z_0$, $z\ne p$) the output is $y=Ae^{pt}+Be^{zt}$ with $A=\dfrac{p-z_0}{p-z}$, $B=\dfrac{z-z_0}{z-p}$. Take $\hat g(s)=\dfrac{s+1}{s+4}$ and $u=e^{-2t}$. Find $A$, $B$, and the input exponent $z$ for which the term $Be^{zt}$ disappears.

- A) $A=-\tfrac32$, $B=\tfrac12$; $z=-1$
- B) $A=\tfrac32$, $B=-\tfrac12$; $z=-4$
- C) $A=-\tfrac32$, $B=\tfrac12$; $z=-4$
- D) $A=\tfrac32$, $B=-\tfrac12$; $z=-1$

> [!success]- Answer
> **D.** $z_0=-1$, $p=-4$, $z=-2$. $A=\dfrac{-4+1}{-4+2}=\dfrac32$, $B=\dfrac{-2+1}{-2+4}=-\dfrac12$.
> Check: $y(0)=A+B=1=\hat g(\infty)u(0)$. $B=0$ needs $z=z_0=-1$: the zero blocks the input mode $e^{-t}$.
> - A: The denominators $p-z$ and $z-p$ were swapped (sign slip): $A+B=-1\ne1$.
> - B: $A$, $B$ are right, but $z=p=-4$ is the pole. The term vanishes at the zero.
> - C: Sign slip in $A$, $B$, and the pole taken instead of the zero.

## 8. State-space representation of LTI systems (slides 29-30)

### Q15 (slide 29)

Write $\dot x_1=-x_1+2x_2+u_1$, $\dot x_2=-3x_2+u_1-u_2$, $y=x_1+4u_2$ as $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $y=C\mathbf{x}+D\mathbf{u}$ with $\mathbf{x}=[x_1\ x_2]^{\mathsf T}$, $\mathbf{u}=[u_1\ u_2]^{\mathsf T}$. Which $B$ and $D$ are correct?

- A) $B=\begin{bmatrix}1&1\\0&-1\end{bmatrix}$, $D=\begin{bmatrix}0&4\end{bmatrix}$
- B) $B=\begin{bmatrix}1&0\\1&-1\end{bmatrix}$, $D=\begin{bmatrix}0&4\end{bmatrix}$
- C) $B=\begin{bmatrix}1&1\\0&-1\end{bmatrix}$, $D=\begin{bmatrix}4&0\end{bmatrix}$
- D) $B=\begin{bmatrix}1&0\\1&-1\end{bmatrix}$, $D=\begin{bmatrix}4&0\end{bmatrix}$

> [!success]- Answer
> **B.** Row $i$ of $B$ holds the input coefficients of $\dot x_i$: row 1 is $[1\ \ 0]$, row 2 is $[1\ \ {-1}]$.
> $D$ is $q\times p=1\times2$ and holds the input coefficients of $y$: $0\cdot u_1+4u_2$, so $D=[0\ \ 4]$. ($A=\begin{bmatrix}-1&2\\0&-3\end{bmatrix}$, $C=[1\ \ 0]$.)
> - A: $B$ is transposed (columns written as rows).
> - C: $B$ is transposed, and the $4$ multiplies $u_2$, so it goes in column 2 of $D$.
> - D: $B$ is right, but the $4$ was put in the $u_1$ column of $D$.

### Q16 (slide 30)

$\dot x_1=x_1+2x_2$, $\dot x_2=3x_1-4x_2+u$, $y=x_1+x_2+2u$. So $A=\begin{bmatrix}1&2\\3&-4\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$, $C=\begin{bmatrix}1&1\end{bmatrix}$, $D=2$. What is $\hat g(s)=C(sI-A)^{-1}B+D$?

- A) $\dfrac{2s^2+7s-18}{(s-2)(s+5)}$
- B) $\dfrac{s+1}{(s-2)(s+5)}$
- C) $\dfrac{2s^2+7s-19}{(s-2)(s+5)}$
- D) $\dfrac{2s^2-5s-21}{(s+2)(s-5)}$

> [!success]- Answer
> **C.** $\det(sI-A)=(s-1)(s+4)-6=(s-2)(s+5)$. $\operatorname{adj}(sI-A)=\begin{bmatrix}s+4&2\\3&s-1\end{bmatrix}$.
> $\operatorname{adj}\cdot B=\begin{bmatrix}2\\s-1\end{bmatrix}$, $C\cdot$ that $=s+1$.
> $\hat g=\dfrac{s+1}{(s-2)(s+5)}+2=\dfrac{2s^2+7s-19}{(s-2)(s+5)}$. Poles $2,-5$, $\hat g(\infty)=2=D$.
> - A: $B$ and $C$ were swapped ($B^{\mathsf T}(sI-A)^{-1}C^{\mathsf T}$ gives $s+2$ on top).
> - B: $D=2$ was forgotten. Then $\hat g(\infty)=0\ne D$.
> - D: Sign error: $(sI+A)^{-1}$ was used, so the poles became $-2$ and $5$.

## 9. Example: mass-spring-damper (slide 31)

### Q17 (slide 31)

Series RLC circuit: $L\,\dfrac{di}{dt}+Ri+v_C=u$ and $C\,\dfrac{dv_C}{dt}=i$, with $R=5$, $L=1$, $C=0.25$. Input: source voltage $u$. Output: $y=v_C$. States $x_1=v_C$, $x_2=i$. What is $\hat g(s)=\hat y/\hat u$ (zero initial state)?

- A) $\dfrac{s}{(s+1)(s+4)}$
- B) $\dfrac{0.25}{s^2+5s+0.25}$
- C) $\dfrac{-4}{(s-1)(s-4)}$
- D) $\dfrac{4}{(s+1)(s+4)}$

> [!success]- Answer
> **D.** $\dot x_1=\tfrac1C x_2=4x_2$, $\dot x_2=-x_1-5x_2+u$: $A=\begin{bmatrix}0&4\\-1&-5\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$, $C_{out}=[1\ \ 0]$, $D=0$.
> $\det(sI-A)=s^2+5s+4=(s+1)(s+4)$. $\operatorname{adj}\cdot B=\begin{bmatrix}4\\s\end{bmatrix}$, first entry $4$.
> $\hat g=\dfrac{4}{(s+1)(s+4)}$, $g(t)=\tfrac43\bigl(e^{-t}-e^{-4t}\bigr)$. Check: $\hat g(0)=1$.
> - A: The output matrix picked $x_2=i$ (the current), not $x_1=v_C$.
> - B: $C$ was used instead of $1/C$ in $\dot x_1$. Then $\hat g(0)=1$ still, but the poles are wrong.
> - C: Sign error: $(sI+A)^{-1}$ was used, so the poles moved to $1$ and $4$.

## 10. Linearization (slides 32-34)

### Q18 (slide 32)

A pendulum with friction obeys $ml^2\ddot\theta=-mgl\sin\theta-b\dot\theta+u$ with $m=0.5$, $l=2$, $g=9.81$, $b=0.4$. States $x_1=\theta$, $x_2=\dot\theta$. A constant torque $u_o$ holds it at $\theta_o=\pi/6$. Find $u_o$, the entry $a_{21}=\partial f_2/\partial x_1$ of $A$ at the operating point, and the eigenvalues of $A$.

- A) $u_o\approx2.453$; $a_{21}\approx-4.248$; $\lambda\approx-0.1\pm2.059j$
- B) $u_o\approx4.905$; $a_{21}\approx-4.248$; $\lambda\approx-0.1\pm2.059j$
- C) $u_o\approx4.905$; $a_{21}\approx-4.905$; $\lambda\approx-0.1\pm2.212j$
- D) $u_o\approx2.453$; $a_{21}\approx-4.905$; $\lambda\approx-0.1\pm2.212j$

> [!success]- Answer
> **B.** $ml^2=2$, $g/l=4.905$. Equilibrium: $\dot\theta=0$ and $mgl\sin\theta_o=u_o$, so $u_o=0.5\cdot9.81\cdot2\cdot0.5=4.905$.
> $f_2=-\tfrac gl\sin x_1-\tfrac{b}{ml^2}x_2+\tfrac{1}{ml^2}u$, so $a_{21}=-\tfrac gl\cos\theta_o=-4.905\cdot0.866=-4.248$, $a_{22}=-0.2$.
> $s^2+0.2s+4.248=0$: $\lambda=-0.1\pm2.059j$. Stable.
> - A: $u_o=\tfrac gl\sin\theta_o$ forgets the factor $ml^2=2$ (the torque is $ml^2$ times the angular term).
> - C: $u_o$ is right, but the Jacobian was evaluated at $\theta=0$ ($\cos0=1$) instead of $\pi/6$.
> - D: Both slips: factor $ml^2$ lost and Jacobian at the wrong point.

### Q19 (slide 33)

A tank: $\dot x=-2\sqrt{x}+u$, output $y=x^2$. The input is held at $u_o=4$. Linearize about the equilibrium ($\tilde x=x-x_o$, $\tilde u=u-u_o$, $\tilde y=y-y_o$). What is the transfer function $\hat g(s)$ from $\tilde u$ to $\tilde y$?

- A) $\dfrac{8}{s+0.5}$
- B) $\dfrac{32}{s+0.25}$
- C) $\dfrac{8}{s-0.5}$
- D) $\dfrac{16}{s+0.5}$

> [!success]- Answer
> **A.** $0=-2\sqrt{x_o}+4$ gives $x_o=4$.
> $A=\partial f/\partial x=-1/\sqrt{x}=-0.5$, $B=1$, $C=\partial h/\partial x=2x=8$, $D=0$.
> $\hat g=C(s-A)^{-1}B+D=\dfrac{8}{s+0.5}$.
> - B: $\sqrt{x_o}=4$ (the factor 2 forgotten) gives $x_o=16$, $A=-0.25$, $C=32$.
> - C: Sign slip in the derivative of $-2\sqrt x$: it is $-1/\sqrt x$, negative.
> - D: $C$ was taken as $h(x_o)=16$ instead of $\partial h/\partial x=8$.

### Q20 (slide 34)

$\dot x=-x^2+u$ with the operating trajectory $x_o(t)=\dfrac{1}{t+1}$, $u_o(t)=0$ (it satisfies $\dot x_o=-x_o^2$). Linearize: what is $A(t)$ in $\dot{\tilde x}=A(t)\tilde x+B(t)\tilde u$, and is the linear model time-invariant?

- A) $A(t)=-\dfrac{1}{(t+1)^2}$. Time-invariant, since $f$ has no explicit $t$.
- B) $A(t)=-\dfrac{2}{t+1}$. Time-invariant, since $f$ has no explicit $t$.
- C) $A(t)=-\dfrac{2}{t+1}$. Time-varying, since the operating point moves.
- D) $A(t)=-\dfrac{1}{(t+1)^2}$. Time-varying, since the operating point moves.

> [!success]- Answer
> **C.** $A(t)=\dfrac{\partial f}{\partial x}\Big\rvert_o=-2x_o=-\dfrac{2}{t+1}$, $B=1$.
> $A$ depends on $t$, so the model is linear time-varying. The reason is the moving operating point.
> - A: $-x_o^2$ is $f$ itself, not its derivative, and the verdict is wrong.
> - B: $A$ is right, but it depends on $t$. A time-invariant $f$ still gives a time-varying model about a moving trajectory.
> - D: The verdict is right, but $A$ is $\partial f/\partial x$, not $f$ at the trajectory.

## 11. Modelling example: double pendulum (slide 35)

### Q21 (slide 35)

The small-angle double pendulum has $\ddot\theta_1=-\dfrac{(m_1+m_2)g}{m_1l_1}\theta_1+\dfrac{m_2g}{m_1l_1}\theta_2$ and $\ddot\theta_2=-\dfrac{g}{l_2}\theta_2+\dfrac{1}{m_2l_2}u$. Take $m_1=2$, $m_2=1$, $l_1=1$, $l_2=0.5$, $g=10$ and states $(\theta_1,\dot\theta_1,\theta_2,\dot\theta_2)$. Find the eigenvalues of $A$ and the transfer function from $u$ to $\theta_1$.

- A) $\pm j\sqrt5,\ \pm j\sqrt{20}$; $\dfrac{10}{(s^2+5)(s^2+20)}$
- B) $\pm j\sqrt{15},\ \pm j\sqrt{20}$; $\dfrac{2.5}{(s^2+15)(s^2+20)}$
- C) $\pm j\sqrt{15},\ \pm j\sqrt{20}$; $\dfrac{10}{(s^2+15)(s^2+20)}$
- D) $\pm j\sqrt5,\ \pm j\sqrt{20}$; $\dfrac{2.5}{(s^2+5)(s^2+20)}$

> [!success]- Answer
> **C.** Entries: $-\tfrac{3\cdot10}{2}=-15$, $\tfrac{10}{2}=5$, $-\tfrac{10}{0.5}=-20$, $\tfrac{1}{0.5}=2$.
> $A$ is block upper triangular: $\det(sI-A)=(s^2+15)(s^2+20)$, eigenvalues $\pm j\sqrt{15}$, $\pm j\sqrt{20}$.
> $\hat\theta_2=\dfrac{2}{s^2+20}\hat u$, $\hat\theta_1=\dfrac{5}{s^2+15}\hat\theta_2$, so $\dfrac{\hat\theta_1}{\hat u}=\dfrac{10}{(s^2+15)(s^2+20)}$.
> - A: $m_2$ was used instead of $m_1+m_2$ in $a_{21}$, giving $-5$.
> - B: $B$ entry taken as $m_2l_2=0.5$ instead of $1/(m_2l_2)=2$: numerator $5\cdot0.5=2.5$.
> - D: Both slips: $m_2$ instead of $m_1+m_2$, and $m_2l_2$ instead of $1/(m_2l_2)$.
