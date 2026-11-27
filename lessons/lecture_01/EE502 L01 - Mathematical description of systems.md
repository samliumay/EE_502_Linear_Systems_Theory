---
course: EE 502 Linear System Theory
lecture: 1
title: Mathematical description of systems
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 1-11)
full_notes: lecture_notes/lecture_01/EE502_Lecture_01_Systems.pdf
---
# EE 502 · Lecture 1 · Mathematical description of systems

> [!summary] In short
> - We replace a physical system by a model, and the model by equations. Analysis studies the equations, design changes them.
> - Suspension: Newton's law gives $m\ddot x_o+b\dot x_o+kx_o=b\dot x_i+kx_i$ and $G(s)=\dfrac{bs+k}{ms^2+bs+k}$.
> - A system is an operator $\mathbf{y}=H\mathbf{u}$ from whole input signals to whole output signals.
> - Memoryless: $\mathbf{y}(t_1)$ uses only $\mathbf{u}(t_1)$. Causal: it never uses $\mathbf{u}(t)$ with $t>t_1$.
> - The state $\mathbf{x}(t_0)$ replaces the whole input history before $t_0$. In circuits: capacitor voltages and inductor currents.
> - Lumped means finitely many states. A pure delay is distributed.

## 1. Course frame (slides 2-4)
![[ee502_eee501alllecturenotesabo_p002.jpg]]
![[ee502_eee501alllecturenotesabo_p003.jpg]]
![[ee502_eee501alllecturenotesabo_p004.jpg]]

**Notes.** The slides are A. B. Özgüler's Bilkent EEE 501 set, based on Chen, *Linear System Theory and Design*. The whole course is about continuous-time systems. Topic order: description of systems, linear algebra review, state-space representations, realization, input-output stability, stability of state-space models, controllability and observability (LTI, then time-varying), state feedback, Luenberger observer, separation principle.

> [!warning] Watch out
> The instructor, assistant and grading on slide 2 are Bilkent's, not EE 502's. Use the EE 502 syllabus for grading.

## 2. Objective: model-based analysis and design (slide 6)
![[ee502_eee501alllecturenotesabo_p006.jpg]]

**Notes.** Two levels of abstraction: physical system → model → mathematical representation. Example rows: a metal pipeline on a battery → a resistor driven by a voltage source → $V=RI$. A car suspension → spring-mass-damper → a 2nd-order differential equation.

- **Analysis**: study the system as it is. Classify it (linear, time-invariant, ...), write the equations, look at the response to test inputs.
- **Design**: change the model (a parameter, feedback, ...) so that it behaves closer to what we want.

> [!question]- Check (slide 6): A water tank with an outlet valve is drawn as "a capacitor that discharges through a resistor" and described by $RC\,\dot v+v=0$. Name the three levels of the slide for this case. Then say whether each action is analysis or design: (a) computing how fast $v$ decays, (b) choosing a larger valve so that the tank empties faster.
> Physical system: the tank with its valve. Model: the capacitor and the resistor (idealized elements). Mathematical representation: the equation $RC\,\dot v+v=0$.
> (a) is analysis: the system stays as it is and we study its response.
> (b) is design: we change a parameter ($R$ becomes smaller) so that the behaviour is closer to what we want.

## 3. Example: automobile suspension (slides 7-8)
![[ee502_eee501alllecturenotesabo_p007.jpg]]
![[ee502_eee501alllecturenotesabo_p008.jpg]]

**Notes.** $x_i(t)$ is the tyre position (set by the road), $x_o(t)$ the body position, both measured from equilibrium, so gravity drops out. $D=\frac{d}{dt}$. $m$ is the mass, $k$ the spring constant, $b$ the damper constant.

Forces on the body: spring $-k(x_o-x_i)$, damper $-b(Dx_o-Dx_i)$. Newton's law:

$$mD^2x_o+b(Dx_o-Dx_i)+k(x_o-x_i)=0 \;\Longrightarrow\; m\ddot x_o+b\dot x_o+kx_o=b\dot x_i+kx_i$$

Laplace transform with zero initial conditions ($D\to s$):

$$G(s)=\frac{X_o(s)}{X_i(s)}=\frac{bs+k}{ms^2+bs+k}\qquad\text{(2nd order)}$$

Check: $G(0)=1$. If the road rises by a constant, the body ends up rising by the same amount.

**Test inputs.** A sinusoid models a smooth road, a square wave a bumpy road.

- Sinusoid (stable $G$): $\sin\omega t \mapsto |G(j\omega)|\sin\bigl(\omega t+\angle G(j\omega)\bigr)$. Same frequency, new amplitude and phase.
- Square wave: the roots of $ms^2+bs+k$ decide. With $\omega_n=\sqrt{k/m}$ (natural frequency) and $\zeta=\dfrac{b}{2\sqrt{km}}$ (damping ratio), the roots are $s=-\zeta\omega_n\pm\omega_n\sqrt{\zeta^2-1}$.

| $\zeta$ | Roots | Name | Step response |
|---|---|---|---|
| $<1$ | complex pair | underdamped | overshoots, rings |
| $=1$ | double real root $-\omega_n$ | critically damped | fastest without overshoot |
| $>1$ | two real roots | overdamped | creeps, no overshoot |

> [!example] Numbers (ours, beyond the slides)
> $m=300$, $k=30000$, $b=1000$, road $x_i=\sin 10t$. $G(j10)=\dfrac{30000+10000j}{10000j}=1-3j$, so $|G|=\sqrt{10}\approx3.16$, angle $\approx-71.6^\circ$: $x_o\approx3.16\sin(10t-71.6^\circ)$.
> Damping: $\omega_n=10$ rad/s, $2\sqrt{km}=6000$. $b=1000$: $\zeta\approx0.167$, roots $\approx-1.67\pm9.86j$ (underdamped). $b=6000$: $\zeta=1$, double root $-10$. $b=9000$: $\zeta=1.5$, roots $-3.82$ and $-26.18$ (overdamped).

> [!question]- Check (slide 7): Suppose the damper is connected between the body and a fixed frame, not between the body and the tyre. The spring stays between body and tyre. Write the new equation of motion and the new transfer function. What changes in the numerator, and is $G(0)$ still 1?
> The damper now feels the absolute body velocity $Dx_o$, so its force is $-b\,Dx_o$. The spring force is still $-k(x_o-x_i)$.
> Newton's law: $mD^2x_o+b\,Dx_o+k(x_o-x_i)=0$, so $m\ddot x_o+b\dot x_o+kx_o=kx_i$.
> Laplace transform with zero initial conditions: $(ms^2+bs+k)X_o(s)=kX_i(s)$.
> $$G(s)=\frac{k}{ms^2+bs+k}$$
> The term $bs$ in the numerator is gone, because the road velocity $Dx_i$ no longer pushes on the body. The denominator is the same. $G(0)=k/k=1$, still 1.

> [!question]- Check (slide 8): Look at the two graphs. (a) In which graph does the body $x_o$ go above the road level $x_i$ after an up-step, and what does that say about the roots of $ms^2+bs+k$? (b) A car has $m=250$, $k=10000$. Which graph belongs to $b=2000$ and which to $b=4000$?
> (a) The top graph (underdamped). The body overshoots and oscillates around the road level, so the roots are a complex pair. In the bottom graph (overdamped) the body approaches the road level without oscillation, so the roots are two real negative numbers.
> (b) The roots are complex when $b^2<4mk$. Here $4mk=4\cdot250\cdot10000=10^7$, so the border is $b=\sqrt{10^7}\approx3162$.
> $b=2000$: $b^2=4\cdot10^6<10^7$, complex roots, top graph. ($\zeta=2000/3162\approx0.63$.)
> $b=4000$: $b^2=1.6\cdot10^7>10^7$, real roots, bottom graph. ($\zeta=4000/3162\approx1.26$, roots $-8\pm2\sqrt6\approx-3.10$ and $-12.90$.)
> Caution (beyond the slides): the graphs are sketches. Because of the zero $bs+k$ in the numerator, the exact step response for $b=4000$ goes a little above the road level once (peak about $1.10$ times the step) and then comes back without oscillating. For $b=2000$ the peak is about $1.24$ and the body oscillates. So the sure sign of complex roots is the oscillation around the road level, not one single overshoot.

## 4. Systems as operators: memoryless and causal (slide 9)
![[ee502_eee501alllecturenotesabo_p009.jpg]]

**Notes.** A multi-input multi-output (MIMO) system has $p$ inputs and $q$ outputs, stacked in vectors $\mathbf{u}$ and $\mathbf{y}$, with $\mathbf{y}=H\mathbf{u}$. $H$ is an operator: it maps whole functions of time to whole functions of time. $t_0$ is the initial time.

- **Memoryless**: $\mathbf{y}(t_1)$ depends only on $\mathbf{u}(t_1)$.
- **Causal** (non-anticipatory): $\mathbf{y}(t_1)$ does not depend on $\mathbf{u}(t)$ for any $t>t_1$.

Test: fix $t_1$, list every input value that $y(t_1)$ uses. Only $u(t_1)$: memoryless. All times $\le t_1$: causal.

Examples: resistor $v=Ri$ is memoryless. Capacitor $v(t)=\frac1C\int_{-\infty}^t i(\tau)\,d\tau$ has memory but is causal. $y(t)=u(t+1)$ is not causal.

> [!warning] Watch out
> - Memoryless implies causal. Causal does not imply memoryless (the capacitor).
> - Slide 9 writes "does not depend on $\mathbf{u}(t)$ for any $t\ge t_1$". With $\ge$ even $\mathbf{u}(t_1)$ would be forbidden. The correct condition is $t>t_1$ (as in Chen).
> - The same slide says "keeping track of $\mathbf{y}(t)$ for $t\le t_0$". It means the input history $\mathbf{u}(t)$.

> [!question]- Check (slide 9, operator): Take the suspension with both tyre positions as inputs and with the body position and the body velocity as outputs. What are $p$ and $q$? Why does the slide call $H$ an operator and not simply a function of the number $\mathbf{u}(t_1)$?
> $p=2$ (two inputs), $q=2$ (two outputs). So $\mathbf{u}(t)$ and $\mathbf{y}(t)$ are both $2\times1$ vectors.
> $H$ takes the whole input signal (a function of time) and returns the whole output signal. In general $\mathbf{y}(t_1)$ depends on many input values, not only on $\mathbf{u}(t_1)$. The body position now depends on the road profile of the last seconds. Only for a memoryless system is $\mathbf{y}(t_1)$ a function of the single value $\mathbf{u}(t_1)$.

> [!question]- Check (slide 9, classify): Memoryless? Causal? Give the reason. (a) $y(t)=t\,u(t)$, (b) $y(t)=\int_0^t e^{-(t-\tau)}u(\tau)\,d\tau$ for $t\ge0$, (c) $y(t)=u(2t)$.
> Fix a time $t_1$ and list the input values that $y(t_1)$ uses.
> (a) Only $u(t_1)$. Memoryless, hence causal. The factor $t$ changes with time, but it is not an input value.
> (b) $u(\tau)$ for $0\le\tau\le t_1$. It uses past values, so it has memory. It uses no future value, so it is causal.
> (c) $y(t_1)=u(2t_1)$. For $t_1=1$ it uses $u(2)$, a future value. Not causal. This holds for every $t_1>0$, because then $2t_1>t_1$. (For $t_1<0$ we have $2t_1<t_1$, a past value, but one time with a future value is enough.) A system that is not causal is also not memoryless.

## 5. State, and the parallel RLC circuit (slide 10)
![[ee502_eee501alllecturenotesabo_p010.jpg]]

**Notes.** The **state** $\mathbf{x}(t_0)$ is the information at $t_0$ that, together with $\mathbf{u}(t)$ for $t\ge t_0$, determines $\mathbf{y}(t)$ for all $t\ge t_0$. It summarizes the effect of the input before $t_0$.

Current-driven parallel RLC: input $i(t)$, output $v(t)=v_C$. All three elements share the voltage $v_C$. KCL at the top node: $i=i_R+i_L+i_C$.

$$Dv_C=\frac1C\Bigl(i-\frac{v_C}{R}-i_L\Bigr),\qquad Di_L=\frac{v_C}{L}$$

Two first-order equations need two initial conditions, so the states are $v_C$ and $i_L$. With $\mathbf{x}=\begin{bmatrix}v_C & i_L\end{bmatrix}^{\mathsf T}$ and $u=i$:

$$\dot{\mathbf{x}}=\begin{bmatrix}-\frac{1}{RC}&-\frac1C\\ \frac1L&0\end{bmatrix}\mathbf{x}+\begin{bmatrix}\frac1C\\0\end{bmatrix}u,\qquad y=\begin{bmatrix}1&0\end{bmatrix}\mathbf{x}$$

Transfer function, from $C_{\text{out}}(sI-A)^{-1}B$ (formula of Lecture 2):

$$\hat g(s)=\frac{s/C}{s^2+\frac{1}{RC}s+\frac{1}{LC}}=\frac{RLs}{RLCs^2+Ls+R}$$

Rule for circuits: states are the capacitor voltages and inductor currents (the energy stores). Resistors give no state.

> [!warning] Watch out
> State is not the same as output. One state-space model gives one transfer function, but many different $(A,B,C,D)$ give the same $\hat g(s)$.

> [!info] Two descriptions, and the mechanical analogue (beyond the slides)
> - **Input-output description**: one equation that contains only $u$ and $y$, for example a transfer function $\hat g(s)$. It assumes zero initial conditions (the system is at rest at $t_0$).
> - **State-space description**: first-order equations $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$. It also works for a nonzero initial state $\mathbf{x}(t_0)$.
>
> Mass-spring-damper with force input $u$ and position output $y$: $m\ddot y+b\dot y+ky=u$. The energy stores are the spring (position) and the mass (velocity), so the states are $x_1=y$ and $x_2=\dot y$. Then $\dot x_1=x_2$, and solving the equation for $\ddot y$ gives $\dot x_2$:
> $$\dot{\mathbf{x}}=\begin{bmatrix}0&1\\-\frac km&-\frac bm\end{bmatrix}\mathbf{x}+\begin{bmatrix}0\\\frac1m\end{bmatrix}u,\qquad y=\begin{bmatrix}1&0\end{bmatrix}\mathbf{x}$$
> The input-output description of the same system is $\hat g(s)=\dfrac{1}{ms^2+bs+k}$.

> [!question]- Check (slide 10, state): In the circuit of the slide take $R=2$, $L=0.5$, $C=0.25$. At $t_0=0$ you know $v_C(0)=2$, $i_L(0)=1$ and $i(0)=3$. Compute $Dv_C(0)$ and $Di_L(0)$. Why do you not need $i(t)$ for $t<0$?
> $Dv_C=\frac1C\bigl(i-\frac{v_C}{R}-i_L\bigr)=\frac{1}{0.25}\bigl(3-\frac22-1\bigr)=4\cdot1=4$ V/s.
> $Di_L=\frac{v_C}{L}=\frac{2}{0.5}=4$ A/s.
> The past input acts on the future only through the charge on the capacitor and the flux in the inductor. These are given by $v_C(0)$ and $i_L(0)$. So the state $(v_C(0),i_L(0))$ already summarizes the input before $t_0$.

> [!question]- Check (slide 10, state equations): A mass-spring-damper has $m=2$, $b=6$, $k=8$, force input $u$ and position output $y$. Choose state variables, write $A$, $B$, $C$, and give the input-output description.
> Equation: $2\ddot y+6\dot y+8y=u$. States: $x_1=y$ (position), $x_2=\dot y$ (velocity). Two states, because the equation is of second order and needs two initial conditions.
> $\dot x_1=x_2$. $\dot x_2=\ddot y=\frac12(u-6x_2-8x_1)=-4x_1-3x_2+0.5u$.
> $$A=\begin{bmatrix}0&1\\-4&-3\end{bmatrix},\qquad B=\begin{bmatrix}0\\0.5\end{bmatrix},\qquad C=\begin{bmatrix}1&0\end{bmatrix}$$
> Input-output description (zero initial conditions): $(2s^2+6s+8)Y(s)=U(s)$, so $\hat g(s)=\dfrac{1}{2s^2+6s+8}=\dfrac{0.5}{s^2+3s+4}$.

## 6. Lumped and distributed systems (slide 11)
![[ee502_eee501alllecturenotesabo_p011.jpg]]

**Notes.** A system is **lumped** (finite-dimensional) if the number of its states is finite, **distributed** (infinite-dimensional) otherwise.

Unit delay $y(t)=u(t-1)$: for $t\in[t_0,t_0+1)$ the output is the input on $[t_0-1,t_0)$. So the future output needs the whole segment $\{u(t),\ t_0-1\le t<t_0\}$: infinitely many initial values. The delay is distributed.

The bottom of the slide states linearity (superposition of states and inputs). It is treated in [[EE502 L02 - LTI models and linearization]].

> [!warning] Watch out
> - The slide writes $t_0-1\ge t\ge t_0$, a typo (no $t$ satisfies it). Read $t_0-1\le t<t_0$.
> - A system with memory is not automatically distributed: the RLC circuit has memory and only two states.

> [!info] How to read the linearity line of slide 11 (beyond the slides)
> An output on $t\ge t_0$ is fixed by a pair: the initial state $\mathbf{x}(t_0)$ and the input $\mathbf{u}(t)$, $t\ge t_0$. Let pair 1 give $\mathbf{y}_1$ and pair 2 give $\mathbf{y}_2$. The system is **linear** if the combined pair $\alpha_1\mathbf{x}_1(t_0)+\alpha_2\mathbf{x}_2(t_0)$, $\alpha_1\mathbf{u}_1+\alpha_2\mathbf{u}_2$ gives $\alpha_1\mathbf{y}_1+\alpha_2\mathbf{y}_2$, for all real $\alpha_1,\alpha_2$. This is superposition. State and input are scaled and added together.
>
> Test for a system given by an input-output equation (zero initial state):
> 1. Apply $u_1$ and $u_2$ separately, get $y_1$ and $y_2$.
> 2. Apply $\alpha_1u_1+\alpha_2u_2$ and compute the output.
> 3. Linear only if the result equals $\alpha_1y_1+\alpha_2y_2$ for all inputs and all $\alpha_1,\alpha_2$.
>
> Quick consequence ($\alpha_1=\alpha_2=0$): zero state and zero input must give zero output. One counterexample is enough to show that a system is not linear.

> [!question]- Check (slide 11, lumped): Lumped or distributed? How many states? (a) $\dot y(t)+2y(t)=u(t)$, (b) $y(t)=3u(t)$, (c) $y(t)=u(t)+u(t-0.5)$.
> (a) Lumped, one state. One number, $y(t_0)$, together with $u(t)$ for $t\ge t_0$ fixes the solution of a first-order equation.
> (b) Lumped, zero states. The system is memoryless, so nothing from the past is needed.
> (c) Distributed. For $t\in[t_0,t_0+0.5)$ the term $u(t-0.5)$ is the input on $[t_0-0.5,t_0)$. One must store this whole segment, which is infinitely many values.

> [!question]- Check (slide 11, linear): Test with superposition (zero initial state): (a) $y(t)=2u(t)+1$, (b) $y(t)=u(t)^2$, (c) $y(t)=t\,u(t)$, (d) $y(t)=u(t-1)$.
> (a) Not linear. $u_1+u_2$ gives $2(u_1+u_2)+1$, but $y_1+y_2=2(u_1+u_2)+2$. Also zero input gives $y=1\ne0$.
> (b) Not linear. $2u$ gives $(2u)^2=4u^2$, but $2y=2u^2$.
> (c) Linear. $t(\alpha_1u_1+\alpha_2u_2)=\alpha_1tu_1+\alpha_2tu_2=\alpha_1y_1+\alpha_2y_2$. The factor $t$ makes it time-varying, not nonlinear.
> (d) Linear. $\alpha_1u_1(t-1)+\alpha_2u_2(t-1)=\alpha_1y_1+\alpha_2y_2$. So the unit delay is linear and distributed at the same time.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Mechanical blocks | $m\ddot x=\sum F$, spring $k\cdot$stretch, damper $b\cdot$relative velocity |
| Circuit blocks | $v=Ri$, $i=C\dot v$, $v=L\dot i$, KCL, KVL |
| Suspension | $G(s)=\dfrac{bs+k}{ms^2+bs+k}$, $\omega_n=\sqrt{k/m}$, $\zeta=\dfrac{b}{2\sqrt{km}}$ |
| Sinusoid response | $\sin\omega t\mapsto\lvert G(j\omega)\rvert\sin(\omega t+\angle G(j\omega))$, stable $G$ |
| Operator | $\mathbf{y}=H\mathbf{u}$, $p$ inputs, $q$ outputs |
| Memoryless | $\mathbf{y}(t_1)$ uses only $\mathbf{u}(t_1)$ |
| Causal | $\mathbf{y}(t_1)$ uses no $\mathbf{u}(t)$ with $t>t_1$ |
| State | information at $t_0$ that, with the future input, fixes the future output |
| Parallel RLC | $\hat g(s)=\dfrac{RLs}{RLCs^2+Ls+R}$ |
| Lumped / distributed | finitely many states / not |

## Check yourself
> [!question]- 1. Same car ($m=300$, $k=30000$, $b=1000$), road $x_i=\sin 20t$. Amplified or reduced?
> $G(j20)=\dfrac{30000+20000j}{-90000+20000j}=\dfrac{3+2j}{-9+2j}$. $|G|=\sqrt{13}/\sqrt{85}\approx0.39$. **Reduced to 39%** (angle $\approx-133.8^\circ$).

> [!question]- 2. Which damper $b$ gives $\zeta=0.7$ for $m=300$, $k=30000$? Where are the poles?
> $b=2\zeta\sqrt{km}=2\cdot0.7\cdot3000=4200$ N s/m. Poles $-\zeta\omega_n\pm j\omega_n\sqrt{1-\zeta^2}=-7\pm7.14j$.

> [!question]- 3. Memoryless? Causal? (a) $y(t)=u(t-2)$, (b) $y(t)=3u(t)+1$, (c) $y(t)=\int_{t-1}^{t+1}u(\tau)\,d\tau$
> (a) Has memory, causal. (b) Memoryless, hence causal. (c) Has memory, not causal (it uses $u(\tau)$ with $\tau>t$).

> [!question]- 4. Parallel RLC with $R=L=C=1$: find $A$, $B$ and $\hat g(s)$.
> $A=\begin{bmatrix}-1&-1\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $\det(sI-A)=s^2+s+1$, $\hat g(s)=\dfrac{s}{s^2+s+1}$.

> [!question]- 5. How many states does a series RLC circuit driven by a voltage source have?
> Two: $i_L$ and $v_C$. KVL: $Di_L=\frac1L(v_s-Ri_L-v_C)$, capacitor: $Dv_C=\frac1C i_L$.

> [!question]- 6. The road steps up by 5 cm. Where does the body end?
> In steady state all derivatives are zero, so $kx_o=kx_i$ ($G(0)=1$). The body ends 5 cm higher.

## Links
- Course index: [[EE502 Home]]
- Next: [[EE502 L02 - LTI models and linearization]]
- Used by Quiz 1 (modelling), together with the state-space part of Lecture 2.
- Full step-by-step notes (PDF): [EE502_Lecture_01_Systems.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_01/EE502_Lecture_01_Systems.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_01/EE502_Lecture_01_Systems.pdf`
- Original slides (PDF, pp. 1-11): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L01 - Mathematical description of systems - quiz]]

Slides not embedded: 1, 5 (title pages).
