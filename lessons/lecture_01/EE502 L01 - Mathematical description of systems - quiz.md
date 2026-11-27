---
course: EE 502 Linear System Theory
lesson: EE502 L01 - Mathematical description of systems
type: quiz
questions: 9
---

# EE502 L01 - Mathematical description of systems - quiz

Lesson note: [[EE502 L01 - Mathematical description of systems]]. One question per check question of the lesson. Pick an option, then open the answer.

## 2. Objective: model-based analysis and design (slide 6)

### Q1 (slide 6)

The slide uses three levels: physical system, then model (idealized elements), then mathematical representation (equations). Analysis studies the system as it is. Design changes the model so that it behaves closer to what we want. A water tank with an outlet valve is drawn as "a capacitor that discharges through a resistor" and described by $RC\,\dot v+v=0$. What is the model level, and what are the two actions (a) computing how fast $v$ decays, (b) choosing a larger valve so that the tank empties faster?

- A) Model: the equation $RC\,\dot v+v=0$. (a) is analysis, (b) is design.
- B) Model: the capacitor and the resistor. (a) is analysis, (b) is design.
- C) Model: the capacitor and the resistor. (a) is design, (b) is analysis.
- D) Model: the equation $RC\,\dot v+v=0$. (a) is design, (b) is analysis.

> [!success]- Answer
> **B.** Physical system: the tank with its valve. Model: the idealized capacitor and resistor. Mathematical representation: $RC\,\dot v+v=0$.
> (a) leaves the system as it is and studies its response: analysis.
> (b) changes a parameter ($R$ becomes smaller) to get a wanted behaviour: design.
> - A: The equation is the third level, the mathematical representation, not the model.
> - C: The model is right, but (a) and (b) are swapped. Computing a decay rate changes nothing.
> - D: Both parts are wrong: the equation is the representation, and (a) and (b) are swapped.

## 3. Example: automobile suspension (slides 7-8)

### Q2 (slide 7)

Car suspension: $x_i(t)$ is the tyre position (set by the road), $x_o(t)$ the body position, both measured from equilibrium. The body has mass $m$. A spring $k$ connects body and tyre. On the slide the damper $b$ also connects body and tyre, with force $-b(\dot x_o-\dot x_i)$ on the body, and $G(s)=\dfrac{bs+k}{ms^2+bs+k}$. Now the damper connects the body to a fixed frame; the spring stays. With zero initial conditions, what is the new $G(s)=X_o(s)/X_i(s)$?

- A) $G(s)=\dfrac{k}{ms^2+bs+k}$
- B) $G(s)=\dfrac{bs+k}{ms^2+bs+k}$
- C) $G(s)=\dfrac{bs+k}{ms^2+k}$
- D) $G(s)=\dfrac{k}{ms^2+k}$

> [!success]- Answer
> **A.** The frame does not move, so the damper feels only the body velocity: force $-b\,\dot x_o$. The spring force is still $-k(x_o-x_i)$.
> Newton: $m\ddot x_o=-b\dot x_o-k(x_o-x_i)$, so $m\ddot x_o+b\dot x_o+kx_o=kx_i$.
> Laplace: $(ms^2+bs+k)X_o=kX_i$. The $bs$ in the numerator is gone, the denominator is the same, and $G(0)=k/k=1$ still.
> - B: This is the old model. The road velocity no longer pushes on the body through the damper.
> - C: From $-b(\dot x_o-\dot x_i)$ you deleted the body term $\dot x_o$ and kept the road term. It is the other way round.
> - D: You dropped the damper. A damper fixed to a frame still gives the force $-b\dot x_o$.

### Q3 (slide 8)

![[ee502_eee501alllecturenotesabo_p008.jpg]]

The graphs show the body $x_o$ for a square-wave road $x_i$. The roots of $ms^2+bs+k$ (the denominator of $G(s)$) are complex when $b^2<4mk$ and real when $b^2>4mk$. A car has $m=250$, $k=10000$. Which graph belongs to $b=2000$, and what are the roots for $b=4000$?

- A) $b=2000$: top graph. For $b=4000$ the roots are $-8\pm4.90j$.
- B) $b=2000$: bottom graph. For $b=4000$ the roots are $-3.10$ and $-12.90$.
- C) $b=2000$: bottom graph. For $b=4000$ the roots are $-8\pm4.90j$.
- D) $b=2000$: top graph. For $b=4000$ the roots are $-3.10$ and $-12.90$.

> [!success]- Answer
> **D.** $4mk=4\cdot250\cdot10000=10^7$, so the border is $b=\sqrt{10^7}\approx3162$.
> $b=2000$: $b^2=4\cdot10^6<10^7$, complex roots, oscillation around the road level: top graph.
> $b=4000$: $s=\dfrac{-4000\pm\sqrt{1.6\cdot10^7-10^7}}{500}=-8\pm4.90$, so $-3.10$ and $-12.90$ (real, bottom graph).
> - A: The $b=2000$ part is right, but for $b=4000$ you wrote $\pm j\sqrt{4mk-b^2}$ without checking the sign. Here $b^2>4mk$, so the roots are real.
> - B: You used the border $b=\sqrt{mk}\approx1581$ (the factor 4 is missing). Then $b=2000$ looks overdamped.
> - C: You reversed the test (complex when $b^2>4mk$). Then $b=2000$ looks real and $b=4000$ complex.

## 4. Systems as operators: memoryless and causal (slide 9)

### Q4 (slide 9, operator)

A system is written $\mathbf{y}=H\mathbf{u}$, where $p$ is the number of inputs and $q$ the number of outputs. Take the suspension with both tyre positions as inputs and with the body position and the body velocity as outputs. What are $p$ and $q$, and why is $H$ called an operator?

- A) $p=1$, $q=1$; $H$ is a matrix that multiplies the vector $\mathbf{u}(t_1)$.
- B) $p=2$, $q=2$; $H$ is a matrix that multiplies the vector $\mathbf{u}(t_1)$.
- C) $p=2$, $q=2$; $H$ maps the whole input signal to the whole output signal.
- D) $p=1$, $q=1$; $H$ maps the whole input signal to the whole output signal.

> [!success]- Answer
> **C.** Two tyre positions give $p=2$. Body position and body velocity give $q=2$. So $\mathbf{u}(t)$ and $\mathbf{y}(t)$ are $2\times1$ vectors.
> The body position at $t_1$ depends on the road profile of the last seconds, not only on $\mathbf{u}(t_1)$. So $H$ takes the whole input function and returns the whole output function.
> - A: You counted each vector as one signal. And a matrix acting on $\mathbf{u}(t_1)$ only describes a memoryless system.
> - B: The counts are right, but the suspension has memory, so $\mathbf{y}(t_1)$ is not a function of $\mathbf{u}(t_1)$ alone.
> - D: The reason is right, but $p$ and $q$ count the entries of the vectors: 2 and 2.

### Q5 (slide 9, classify)

Memoryless: $y(t_1)$ uses only $u(t_1)$. Causal: $y(t_1)$ uses no $u(t)$ with $t>t_1$. "Causal with memory" means causal but not memoryless. Classify (a) $y(t)=t\,u(t)$, (b) $y(t)=\int_0^t e^{-(t-\tau)}u(\tau)\,d\tau$ for $t\ge0$, (c) $y(t)=u(2t)$.

- A) (a) causal with memory; (b) not causal; (c) not causal.
- B) (a) memoryless; (b) not causal; (c) memoryless.
- C) (a) memoryless; (b) causal with memory; (c) not causal.
- D) (a) causal with memory; (b) causal with memory; (c) memoryless.

> [!success]- Answer
> **C.** Fix $t_1$ and list the input values that $y(t_1)$ uses.
> (a) Only $u(t_1)$: memoryless, hence causal. The factor $t$ is not an input value.
> (b) $u(\tau)$ for $0\le\tau\le t_1$: past values, no future value. Causal with memory.
> (c) $y(1)=u(2)$, a future value. Not causal, so also not memoryless.
> - A: In (a) you counted the factor $t$ as memory. In (b) you read the $t$ in $e^{-(t-\tau)}$ as a future input; the inputs used are only $u(\tau)$, $\tau\le t_1$.
> - B: (b) has the same slip as in A. In (c) you saw one input value and called it memoryless, but that value is at time $2t_1$, not $t_1$.
> - D: (a) has the slip with the factor $t$, and (c) the slip with the single value at $2t_1$.

## 5. State, and the parallel RLC circuit (slide 10)

### Q6 (slide 10, state)

A current source $i(t)$ drives $R$, $L$, $C$ in parallel. KCL at the top node: $i=\dfrac{v_C}{R}+i_L+C\,Dv_C$. Inductor: $v_C=L\,Di_L$. Take $R=2$, $L=0.5$, $C=0.25$. At $t_0=0$: $v_C(0)=2$, $i_L(0)=1$, $i(0)=3$. Find $Dv_C(0)$ and $Di_L(0)$. Why is $i(t)$ for $t<0$ not needed?

- A) $4$ V/s and $4$ A/s; the state $(v_C(0),i_L(0))$ sums up the past input.
- B) $12$ V/s and $1$ A/s; the state $(v_C(0),i_L(0))$ sums up the past input.
- C) $4$ V/s and $1$ A/s; the circuit was at rest, so the past input was zero.
- D) $12$ V/s and $4$ A/s; the circuit was at rest, so the past input was zero.

> [!success]- Answer
> **A.** $Dv_C=\dfrac1C\Bigl(i-\dfrac{v_C}{R}-i_L\Bigr)=4\,(3-1-1)=4$ V/s.
> $Di_L=\dfrac{v_C}{L}=\dfrac{2}{0.5}=4$ A/s.
> The past input acts on the future only through the capacitor charge and the inductor flux, that is through $v_C(0)$ and $i_L(0)$.
> - B: $12=4\,(3-1+1)$: sign slip on $i_L$ when solving KCL. $1=2\cdot0.5$: you multiplied by $L$ instead of dividing.
> - C: Same $L$ slip. And the circuit was not at rest: $v_C(0)=2\neq0$.
> - D: Same $i_L$ sign slip, and the same wrong "at rest" reason.

### Q7 (slide 10, state equations)

A mass-spring-damper obeys $m\ddot y+b\dot y+ky=u$ with $m=2$, $b=6$, $k=8$, force input $u$, position output $y$. Take $x_1=y$, $x_2=\dot y$, so $\dot{\mathbf{x}}=A\mathbf{x}+B u$, $y=\begin{bmatrix}1&0\end{bmatrix}\mathbf{x}$. Which $A$ and which $\hat g(s)=Y(s)/U(s)$ (zero initial conditions) are right?

- A) $A=\begin{bmatrix}0&1\\-8&-6\end{bmatrix}$, $\hat g(s)=\dfrac{1}{s^2+6s+8}$
- B) $A=\begin{bmatrix}0&1\\-4&-3\end{bmatrix}$, $\hat g(s)=\dfrac{0.5}{s^2+3s+4}$
- C) $A=\begin{bmatrix}0&1\\-4&-3\end{bmatrix}$, $\hat g(s)=\dfrac{1}{s^2+3s+4}$
- D) $A=\begin{bmatrix}0&1\\-8&-6\end{bmatrix}$, $\hat g(s)=\dfrac{0.5}{s^2+6s+8}$

> [!success]- Answer
> **B.** $\dot x_1=x_2$. $\dot x_2=\ddot y=\tfrac12(u-6x_2-8x_1)=-4x_1-3x_2+0.5u$.
> So $A=\begin{bmatrix}0&1\\-4&-3\end{bmatrix}$ and $B=\begin{bmatrix}0\\0.5\end{bmatrix}$.
> $(2s^2+6s+8)Y=U$, so $\hat g(s)=\dfrac{1}{2s^2+6s+8}=\dfrac{0.5}{s^2+3s+4}$.
> - A: You did not divide by $m$ at all, as if $m=1$.
> - C: $A$ is right, but you did not divide $u$ by $m$ ($B=[0\ \ 1]^{\mathsf T}$).
> - D: You divided only $u$ by $m$, not the terms $6x_2$ and $8x_1$.

## 6. Lumped and distributed systems (slide 11)

### Q8 (slide 11, lumped)

The state at $t_0$ is the information that, with $u(t)$ for $t\ge t_0$, fixes $y(t)$ for $t\ge t_0$. A system is lumped if it needs finitely many state values, distributed if it needs infinitely many. Classify (a) $\dot y(t)+2y(t)=u(t)$, (b) $y(t)=3u(t)$, (c) $y(t)=u(t)+u(t-0.5)$.

- A) (a) lumped, 1 state; (b) lumped, 0 states; (c) distributed.
- B) (a) lumped, 1 state; (b) lumped, 1 state; (c) lumped, 1 state.
- C) (a) lumped, 2 states; (b) lumped, 0 states; (c) lumped, 1 state.
- D) (a) lumped, 2 states; (b) lumped, 1 state; (c) distributed.

> [!success]- Answer
> **A.** (a) A first-order equation needs one number, $y(t_0)$: lumped, 1 state.
> (b) Memoryless: nothing from the past is needed, 0 states.
> (c) For $t\in[t_0,t_0+0.5)$ the term $u(t-0.5)$ is the input on $[t_0-0.5,t_0)$. That whole segment, infinitely many values, must be stored: distributed.
> - B: In (b) you gave every system at least one state. In (c) you stored only the single value $u(t_0-0.5)$.
> - C: In (a) you also counted $u(t_0)$, but $u$ for $t\ge t_0$ is given. (c) has the same slip as in B.
> - D: (a) has the $u(t_0)$ slip, (b) the "at least one state" slip.

### Q9 (slide 11, linear)

Zero initial state. A system is linear if, for all inputs $u_1,u_2$ with outputs $y_1,y_2$ and all real $\alpha_1,\alpha_2$, the input $\alpha_1u_1+\alpha_2u_2$ gives $\alpha_1y_1+\alpha_2y_2$. Which of these are linear: (a) $y(t)=2u(t)+1$, (b) $y(t)=u(t)^2$, (c) $y(t)=t\,u(t)$, (d) $y(t)=u(t-1)$?

- A) Linear: (a), (b) and (d).
- B) None of the four is linear.
- C) Linear: (a), (b) and (c).
- D) Linear: (c) and (d) only.

> [!success]- Answer
> **D.** (a) $u_1+u_2$ gives $2(u_1+u_2)+1$, but $y_1+y_2=2(u_1+u_2)+2$. Also $u=0$ gives $y=1\neq0$. Not linear.
> (b) $2u$ gives $4u^2$, but $2y=2u^2$. Not linear.
> (c) $t(\alpha_1u_1+\alpha_2u_2)=\alpha_1tu_1+\alpha_2tu_2$. Linear (and time-varying).
> (d) $\alpha_1u_1(t-1)+\alpha_2u_2(t-1)=\alpha_1y_1+\alpha_2y_2$. Linear (and distributed).
> - A: You counted the constant offset in (a) as linear, for (b) you only checked that $u=0$ gives $y=0$, and you took the factor $t$ in (c) as nonlinear.
> - B: You took the factor $t$ in (c) and the delay in (d) as nonlinear. They make the system time-varying and distributed, not nonlinear.
> - C: The same slips in (a) and (b), and the delay in (d) taken as nonlinear.
