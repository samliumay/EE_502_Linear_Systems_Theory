---
course: EE 502 Linear System Theory
lecture: 2
title: LTI models and linearization
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 12-35)
full_notes: lecture_notes/lecture_02/EE502_Lecture_02_LTI_Models.pdf
---
# EE 502 · Lecture 2 · LTI models and linearization

> [!summary] In short
> - Linear means superposition of the pair (initial state, input). With zero initial state it is input-linearity.
> - An input-linear system is described by its impulse response: $y(t)=\int g(t,\tau)u(\tau)\,d\tau$. Relaxed cuts the lower limit, causal cuts the upper limit.
> - Time-invariant: $g(t,\tau)=g(t-\tau)$, so the output is a convolution and $\hat y(s)=\hat g(s)\hat u(s)$.
> - Lumped systems have rational transfer functions. A delay gives $e^{-sT}$.
> - State space: $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$, with $\hat G(s)=C(sI-A)^{-1}B+D$.
> - Linearization: Jacobians of $\mathbf{f}$ and $\mathbf{h}$ at an operating point give a linear model for small deviations.

## 1. Linearity and input-linearity (slide 15)
![[ee502_eee501alllecturenotesabo_p015.jpg]]

**Notes.** **Linear** (slide 11): if state $\mathbf{x}_i(t_0)$ and input $\mathbf{u}_i$ give output $\mathbf{y}_i$ ($i=1,2$), then state $\alpha_1\mathbf{x}_1(t_0)+\alpha_2\mathbf{x}_2(t_0)$ with input $\alpha_1\mathbf{u}_1+\alpha_2\mathbf{u}_2$ gives $\alpha_1\mathbf{y}_1+\alpha_2\mathbf{y}_2$, for all real $\alpha_1,\alpha_2$.

**Input-linear**: with all initial conditions zero, $H(\alpha_1\mathbf{u}_1+\alpha_2\mathbf{u}_2)=\alpha_1\mathbf{y}_1+\alpha_2\mathbf{y}_2$.

For a linear system the output splits as $\mathbf{y}=\mathbf{y}_{zi}+\mathbf{y}_{zs}$: zero-input response (initial state alone) plus zero-state response (input alone).

The lower half of the slide prepares the impulse response. $\delta_\Delta(t-t_i)$ is a pulse of height $1/\Delta$ and width $\Delta$ (area 1), and any input is close to a staircase:

$$u(t)\cong\sum_{i=-\infty}^{\infty}u(t_i)\,\delta_\Delta(t-t_i)\,\Delta$$

> [!warning] Watch out
> - Adding inputs while keeping the same nonzero initial state is not a linearity test. Test on $\dot x=-x+u$: $(y_1+y_2)-y_3=e^{-t}x_0\neq0$.
> - An affine map such as $y=2u+3$ is not linear: zero input gives a nonzero output.

> [!question]- Check (slide 15): Take $u(t)=t^2$, $\Delta=0.1$ and $t_i=0.5$. What is the height of the pulse $\delta_\Delta(t-t_i)$, and what is the height of the term $u(t_i)\,\delta_\Delta(t-t_i)\,\Delta$? Why is the factor $\Delta$ needed in the sum?
> The pulse has height $1/\Delta=1/0.1=10$ and width $0.1$, so its area is 1.
> $u(t_i)=0.5^2=0.25$. The term has height $u(t_i)\cdot\frac{1}{\Delta}\cdot\Delta=0.25\cdot10\cdot0.1=0.25$ on $[0.5,\,0.6)$.
> The factor $\Delta$ cancels the height $1/\Delta$ of the pulse. Then each term is a block of height $u(t_i)$, and the sum of the blocks is the staircase in the right figure.
> The same factor $\Delta$ later becomes $d\tau$ when the sum turns into an integral.

## 2. Impulse response (slides 16-18)
![[ee502_eee501alllecturenotesabo_p016.jpg]]
![[ee502_eee501alllecturenotesabo_p017.jpg]]
![[ee502_eee501alllecturenotesabo_p018.jpg]]

**Notes.** Let $g_\Delta(t,t_i)$ be the response to the pulse $\delta_\Delta(t-t_i)$. By input-linearity the output is the same weighted sum of pulse responses. As $\Delta\to0$ the sum becomes an integral:

$$y(t)=\int_{-\infty}^{\infty}g(t,\tau)\,u(\tau)\,d\tau\qquad(1)$$

$g(t,\tau)$ is the **impulse response**: the output at time $t$ for a unit impulse applied at time $\tau$.

- **Relaxed** at $t_0$ (all initial conditions zero): $y(t)=\int_{t_0}^{\infty}g(t,\tau)u(\tau)\,d\tau$ (2).
- Relaxed and **causal**: $y(t)=\int_{t_0}^{t}g(t,\tau)u(\tau)\,d\tau$ (3).

Only input-linearity was used, so (1) to (3) hold for lumped and distributed systems.

Multivariable ($p$ inputs, $q$ outputs): $\mathbf{y}(t)=\int_{t_0}^{t}G(t,\tau)\mathbf{u}(\tau)\,d\tau$ with $G=[g_{ij}]$ a $q\times p$ matrix.

> [!warning] Watch out
> Slide 18 says $g_{ij}$ is the response "at the j-th output to an impulse at the i-th input". The matrix product gives $y_i=\sum_j\int g_{ij}u_j$, so the **row $i$ is the output, the column $j$ is the input** (Chen's convention). Slide 23 has the same swap for $\hat g_{ij}$.

> [!question]- Check (slide 16): A system has $g(t,\tau)=\tau\,e^{-(t-\tau)}$ for $t\ge\tau$ and $0$ otherwise. Find the output at $t=3$ for a unit impulse applied at $\tau=2$, and the output at $t=2$ for a unit impulse applied at $\tau=1$. What do the two values tell you?
> The first argument is the time when we look at the output. The second argument is the time when the impulse is applied.
> $g(3,2)=2\,e^{-(3-2)}=2e^{-1}\approx0.736$.
> $g(2,1)=1\cdot e^{-(2-1)}=e^{-1}\approx0.368$.
> In both cases the output is observed 1 second after the impulse, but the values are different. So the response depends on when the impulse is applied, not only on the elapsed time. This system is time-varying (section 3).

> [!question]- Check (slide 17): A causal system has $g(t,\tau)=e^{-2(t-\tau)}$ for $t\ge\tau$ and $0$ otherwise. It is relaxed at $t_0=1$ and the input is $u(t)=4$ for $t\ge1$. Find $y(t)$ for $t\ge1$ and the value $y(2)$. Which property gives each limit of the integral?
> Use (3): $y(t)=\int_{1}^{t}e^{-2(t-\tau)}\cdot4\,d\tau$.
> Take $e^{-2t}$ out: $y(t)=4e^{-2t}\int_1^t e^{2\tau}\,d\tau=4e^{-2t}\cdot\dfrac{e^{2t}-e^{2}}{2}=2-2e^{-2(t-1)}$.
> $y(2)=2-2e^{-2}\approx2-0.271=1.729$.
> Lower limit $t_0=1$: the system is relaxed, so inputs before $t_0$ have no effect. Upper limit $t$: the system is causal, so inputs after $t$ have no effect.

> [!question]- Check (slide 18): A relaxed, causal system has 2 inputs and 3 outputs. What is the size of $G(t,\tau)$? Which entry tells you how input 2 acts on output 3? What is the output vector if only input 1 is a unit impulse at time $\tau_0$?
> $G$ is $q\times p=3\times2$: one row per output, one column per input.
> Input 2 to output 3 is the entry in row 3, column 2: $g_{32}(t,\tau)$.
> With $\mathbf{u}(\tau)=\begin{bmatrix}\delta(\tau-\tau_0)\\0\end{bmatrix}$ the integral picks the first column: $\mathbf{y}(t)=\begin{bmatrix}g_{11}(t,\tau_0)\\g_{21}(t,\tau_0)\\g_{31}(t,\tau_0)\end{bmatrix}$ for $t\ge\tau_0$.
> So column $j$ of $G$ is the set of all output responses to an impulse at input $j$.

## 3. Time invariance (slides 19-20)
![[ee502_eee501alllecturenotesabo_p019.jpg]]
![[ee502_eee501alllecturenotesabo_p020.jpg]]

**Notes.** **Time-invariant**: if $\mathbf{x}(t_0)$ and $\mathbf{u}$ give $\mathbf{y}(t)$, then for every $T>0$ the same state at $t_0+T$ with the shifted input $\mathbf{u}(t-T)$ gives the shifted output $\mathbf{y}(t-T)$.

Consequences: take $t_0=0$, and $g(t,\tau)=g(t-\tau,0)=:g(t-\tau)$. Only the elapsed time matters. Causal means $g(t)=0$ for $t<0$. For an LTI, causal, relaxed system:

$$y(t)=\int_0^t g(t-\tau)\,u(\tau)\,d\tau=\int_0^t g(\sigma)\,u(t-\sigma)\,d\sigma$$

Test for time invariance: apply $u(t-T)$ and compare with $y(t-T)$.

| System | Memoryless | Causal | Linear | Time-invariant |
|---|---|---|---|---|
| $y=t\,u(t)$ | yes | yes | yes | no |
| $y=u(t)^2$ | yes | yes | no | yes |
| $y=u(t+1)$ | no | no | yes | yes |
| $\dot y=-y+u$ | no | yes | yes | yes |

> [!question]- Check (slide 19): In the figure, $u_2$ is $u_1$ shifted to the right by $T$, and the state at $t_0+T$ equals the old state at $t_0$. What must $y_2$ be for a time-invariant system? Use this test on $y(t)=e^{-t}u(t)$.
> For a time-invariant system $y_2(t)=y_1(t-T)$: the same waveform, shifted by $T$. This is what the last plot shows.
> Test. The response to the shifted input $u(t-T)$ is $e^{-t}u(t-T)$.
> The shifted output is $y(t-T)=e^{-(t-T)}u(t-T)=e^{T}e^{-t}u(t-T)$.
> The two differ by the factor $e^{T}\ne1$ for $T>0$. So $y(t)=e^{-t}u(t)$ is **not time-invariant** (it is linear and memoryless).

> [!question]- Check (slide 20): A causal time-invariant system has $g(t,0)=5e^{-3t}$ for $t\ge0$. Find $g(7,5)$ and $g(5,7)$. Then find the output for $u(t)=e^{-t}$, $t\ge0$, with zero initial conditions.
> Time-invariant: $g(t,\tau)=g(t-\tau)$. So $g(7,5)=g(2)=5e^{-6}\approx0.0124$.
> $g(5,7)=g(-2)=0$. Causal means $g(t)=0$ for $t<0$: no response before the impulse is applied.
> Convolution: $y(t)=\int_0^t5e^{-3(t-\tau)}e^{-\tau}\,d\tau=5e^{-3t}\int_0^te^{2\tau}\,d\tau=5e^{-3t}\cdot\dfrac{e^{2t}-1}{2}$.
> $y(t)=\dfrac52\left(e^{-t}-e^{-3t}\right)$ for $t\ge0$.

## 4. Example: feedback loop with a unit delay (slide 21)
![[ee502_eee501alllecturenotesabo_p021.jpg]]

**Notes.** Negative feedback, gain $a$ and a unit delay in the forward path. Loop equation: $y(t)=a\,r(t-1)-a\,y(t-1)$. With $r=\delta$ and a relaxed system, unrolling gives one echo per trip around the loop:

$$g_f(t)=\sum_{i=1}^{\infty}(-1)^{i-1}a^i\,\delta(t-i),\qquad y(t)=\sum_{i=1}^{\infty}(-1)^{i-1}a^i\,r(t-i)$$

In the $s$-domain: $\hat g_f(s)=\dfrac{ae^{-s}}{1+ae^{-s}}$. For a unit step and $a=0.5$ the output goes $0.5,\ 0.25,\ 0.375,\ 0.3125,\dots\to\frac{a}{1+a}=\frac13$. The echoes die out exactly when $|a|<1$. The system is LTI and causal but distributed.

> [!warning] Watch out
> Slide typos: the third term is printed $a^3(t-3)$, it is $a^3\delta(t-3)$. The integrand is printed $g_f(t)r(\tau)$, it is $g_f(t-\tau)r(\tau)$.

> [!info] Where the series comes from (beyond the slides)
> The signal after the summing point is $e(t)=r(t)-y(t)$. The gain gives $a\,e(t)$ and the unit delay gives $y(t)=a\,e(t-1)=a\,r(t-1)-a\,y(t-1)$.
> Unroll with $r=\delta$ and $y=0$ for $t<0$:
> - First trip: the impulse passes the gain and the delay. Output $a\,\delta(t-1)$.
> - This output comes back with a minus sign, passes the gain and the delay again. Output $-a^2\delta(t-2)$.
> - Third trip: $+a^3\delta(t-3)$. Each trip multiplies by $-a$ and adds one second of delay.
>
> In the $s$-domain each $\delta(t-i)$ becomes $e^{-is}$, so $\hat g_f(s)=\sum_{i\ge1}(-1)^{i-1}a^ie^{-is}$. This is a geometric series with first term $ae^{-s}$ and ratio $-ae^{-s}$. Its sum is $\dfrac{ae^{-s}}{1+ae^{-s}}$ (the series converges when $\lvert ae^{-s}\rvert<1$). This is the usual feedback formula $\dfrac{\text{forward}}{1+\text{loop}}$ with forward path $ae^{-s}$.

> [!question]- Check (slide 21): Take $a=2$ and a unit-step input $r(t)=1$ for $t\ge0$. Find $y(t)$ on the intervals $[1,2)$, $[2,3)$ and $[3,4)$. What happens as $t$ grows, and why?
> Use $y(t)=\sum_{i\ge1}(-1)^{i-1}a^i\,r(t-i)$. The term $i$ is switched on when $t\ge i$.
> $1\le t<2$: only $i=1$. $y=2$.
> $2\le t<3$: $i=1,2$. $y=2-4=-2$.
> $3\le t<4$: $i=1,2,3$. $y=2-4+8=6$.
> The next value is $6-16=-10$. The output changes sign every second and its size grows without bound.
> Reason: each trip around the loop multiplies the echo by $-a=-2$. The echoes die out only when $|a|<1$.

## 5. Transfer function and transfer matrix (slides 22-23)
![[ee502_eee501alllecturenotesabo_p022.jpg]]
![[ee502_eee501alllecturenotesabo_p023.jpg]]

**Notes.** Take the Laplace transform of the convolution, swap the order of integration, substitute $\mu=t-\tau$, and use $g(\mu)=0$ for $\mu<0$:

$$\hat y(s)=\hat g(s)\,\hat u(s),\qquad \hat g(s)=\int_0^\infty g(\mu)e^{-s\mu}\,d\mu$$

$\hat g(s)$ is the **transfer function**: the Laplace transform of the impulse response. For $p$ inputs and $q$ outputs, $\hat G(s)=\int_0^\infty G(t)e^{-st}\,dt=[\hat g_{ij}(s)]_{q\times p}$ is the **transfer matrix**, and $\hat g_{ij}$ is the transfer function from input $j$ to output $i$.

> [!warning] Watch out
> $\hat y=\hat g\hat u$ is only the zero-state response. A nonzero initial state adds a term (section 8).

> [!question]- Check (slide 22): In the derivation the inner integral first starts at $\mu=-\tau$ and in the next line at $\mu=0$. Why is this allowed? Then find $\hat g(s)$ for $g(t)=2e^{-3t}$, $t\ge0$, and the unit-step response.
> The substitution $\mu=t-\tau$ turns the lower limit $t=0$ into $\mu=-\tau\le0$. The system is causal, so $g(\mu)=0$ for $\mu<0$. The part of the integral from $-\tau$ to $0$ is zero, so the lower limit can be moved to $0$.
> $\hat g(s)=\int_0^\infty2e^{-3\mu}e^{-s\mu}\,d\mu=\dfrac{2}{s+3}$.
> Step: $\hat u=\dfrac1s$, so $\hat y=\dfrac{2}{s(s+3)}=\dfrac{2/3}{s}-\dfrac{2/3}{s+3}$.
> $y(t)=\dfrac23\left(1-e^{-3t}\right)$ for $t\ge0$.

> [!question]- Check (slide 23): A system with 2 inputs and 2 outputs has impulse responses $g_{11}=e^{-t}$, $g_{12}=0$, $g_{21}=2$, $g_{22}=e^{-3t}$ for $t\ge0$ (row = output, column = input). Find $\hat G(s)$. Then find $y_2(t)$ when $u_1$ is a unit step and $u_2=\delta(t)$.
> Transform each entry: $\hat G(s)=\begin{bmatrix}\dfrac{1}{s+1}&0\\ \dfrac{2}{s}&\dfrac{1}{s+3}\end{bmatrix}$.
> Inputs: $\hat u_1=\dfrac1s$, $\hat u_2=1$.
> Row 2: $\hat y_2=\hat g_{21}\hat u_1+\hat g_{22}\hat u_2=\dfrac2s\cdot\dfrac1s+\dfrac{1}{s+3}=\dfrac{2}{s^2}+\dfrac{1}{s+3}$.
> $y_2(t)=2t+e^{-3t}$ for $t\ge0$.
> Each output is a sum over the inputs: one term per column of its row.

## 6. Rational vs irrational, poles and zeros (slides 24-26)
![[ee502_eee501alllecturenotesabo_p024.jpg]]
![[ee502_eee501alllecturenotesabo_p025.jpg]]
![[ee502_eee501alllecturenotesabo_p026.jpg]]

**Notes.** $T$-delay $y(t)=u(t-T)$: $g(t)=\delta(t-T)$, so $\hat g(s)=e^{-sT}$, not a ratio of polynomials. A lumped LTI system always has a **rational** $\hat g(s)=N(s)/D(s)$.

| Name | Condition | $\hat g(\infty)$ |
|---|---|---|
| proper | $\deg N\le\deg D$ | finite |
| strictly proper | $\deg N<\deg D$ | $0$ |
| biproper | $\deg N=\deg D$ | nonzero constant |
| improper | $\deg N>\deg D$ | infinite |

$\lambda$ is a **pole** if $|\hat g(s)|\to\infty$ as $s\to\lambda$, a **zero** if $\hat g(\lambda)=0$. If $N$ and $D$ are coprime (no common root): poles are the roots of $D$, zeros are the roots of $N$. Strictly proper: $\deg D-\deg N$ zeros at infinity. Improper: $\deg N-\deg D$ poles at infinity.

Zero-pole-gain form: $\hat g(s)=k\dfrac{(s-z_1)\cdots(s-z_m)}{(s-p_1)\cdots(s-p_n)}$. Zeros and poles may be complex and repeated.

> [!example] Cancel first
> $\hat g=\dfrac{2s^2+6s+4}{s^2+4s+3}=\dfrac{2(s+1)(s+2)}{(s+1)(s+3)}=\dfrac{2(s+2)}{s+3}$. Pole $-3$, zero $-2$, biproper, $\hat g(\infty)=2$. The point $-1$ is neither a pole nor a zero.

> [!warning] Watch out
> Lumped implies rational, one direction only. A non-rational $\hat g$ proves "distributed".

> [!question]- Check (slide 24): A room adds one echo to a sound: $y(t)=u(t)+0.5\,u(t-2)$. Find $g(t)$ and $\hat g(s)$. Is the system lumped or distributed?
> Put $u=\delta$: $g(t)=\delta(t)+0.5\,\delta(t-2)$.
> Sifting property: $\int_0^\infty\delta(t-T)e^{-st}\,dt=e^{-sT}$, the integrand is evaluated at $t=T$.
> $\hat g(s)=1+0.5\,e^{-2s}$.
> $e^{-2s}$ is not a ratio of polynomials, so $\hat g$ is irrational. A lumped system always has a rational $\hat g$, so this system is **distributed**. To produce $u(t-2)$ the system must store the whole input over the last 2 seconds, which is infinitely many numbers.

> [!question]- Check (slide 25): Classify $\hat g(s)=\dfrac{3s^2+3}{s^2+2s+5}$: properness, $\hat g(\infty)$, poles and zeros.
> $\deg N=\deg D=2$: **biproper** (so also proper). $\hat g(\infty)=3/1=3$, the ratio of the leading coefficients.
> Poles: $s^2+2s+5=0$ gives $s=\dfrac{-2\pm\sqrt{4-20}}{2}=-1\pm2j$.
> Zeros: $3s^2+3=0$ gives $s=\pm j$.
> $N$ and $D$ have no common root, so they are coprime and nothing cancels. Complex poles and zeros come in conjugate pairs because the coefficients are real.

> [!question]- Check (slide 26): A transfer function has a double zero at $-1$, poles at $-2\pm j$ and $\hat g(0)=2$. Write it in zero-pole-gain form and find $k$. How many zeros at infinity does it have? What changes if one of the two zeros is removed?
> Form: $\hat g(s)=k\,\dfrac{(s+1)^2}{(s+2-j)(s+2+j)}=k\,\dfrac{(s+1)^2}{s^2+4s+5}$.
> At $s=0$: $\hat g(0)=k\cdot\dfrac{1}{5}=2$, so $k=10$.
> $\deg D-\deg N=2-2=0$: no zeros at infinity. $\hat g(\infty)=k=10$, biproper.
> With one zero removed, $\hat g=k\dfrac{s+1}{s^2+4s+5}$ is strictly proper with $2-1=1$ zero at infinity. Counting the zeros at infinity, the number of zeros again equals the number of poles (2).

## 7. Transfer matrix terminology, blocking zeros (slides 27-28)
![[ee502_eee501alllecturenotesabo_p027.jpg]]
![[ee502_eee501alllecturenotesabo_p028.jpg]]

**Notes.** $\hat G(s)$ is strictly proper if $\hat G(\infty)=0$, proper if $\hat G(\infty)=K$ (a constant matrix). Square $\hat G$ is biproper (it and its inverse are proper) exactly when $K$ is nonsingular.

- **Pole** of $\hat G$: a pole of at least one entry. Equivalent: a root of the least common multiple of the denominators of all entries (coprime form).
- **Blocking zero**: $\hat G(\lambda)=0$, a zero of every entry.

Meaning of a zero. Take $\hat g(s)=\dfrac{s-z_0}{s-p}$ and input $u=e^{zt}$. If $z\ne z_0$: $y(t)=Ae^{pt}+Be^{zt}$ with $A=\dfrac{p-z_0}{p-z}$, $B=\dfrac{z-z_0}{z-p}$. If $z=z_0$: the factor cancels, $\hat y=\dfrac{1}{s-p}$, $y=e^{pt}$. The zero blocks the input mode $e^{z_0t}$.

> [!example] Numbers
> $\hat g=\dfrac{s-2}{s+1}$. Step input: $y=3e^{-t}-2$. Input $e^{2t}$: $y=e^{-t}$, the growing input is blocked.

> [!question]- Check (slide 27): A $2\times2$ transfer matrix has entries $\hat g_{11}=\dfrac{s-1}{s+2}$, $\hat g_{12}=\dfrac{s-1}{(s+2)(s+3)}$, $\hat g_{21}=0$, $\hat g_{22}=\dfrac{2(s-1)}{s+3}$. Find its poles, decide if it is proper, strictly proper or biproper, and find its blocking zeros.
> Denominators: $s+2$, $(s+2)(s+3)$, $s+3$. Their least common multiple is $(s+2)(s+3)$. Poles: $-2$ and $-3$.
> Limit $s\to\infty$: $\hat g_{11}\to1$, $\hat g_{12}\to0$, $\hat g_{22}\to2$. So $K=\hat G(\infty)=\begin{bmatrix}1&0\\0&2\end{bmatrix}$.
> $K$ is a constant matrix: proper. $K\ne0$: not strictly proper. $\det K=2\ne0$, $K$ is nonsingular: **biproper**.
> Blocking zero: every entry must be zero at $\lambda$. All nonzero entries have the factor $s-1$, and $\hat g_{21}$ is zero everywhere. So $\hat G(1)=0$ and $\lambda=1$ is the only blocking zero.

> [!question]- Check (slide 28): Take $\hat g(s)=\dfrac{s+1}{s+4}$ and the input $u(t)=e^{-2t}$. Find the constants $A$ and $B$ in $y(t)=Ae^{pt}+Be^{zt}$. For which input exponent $z$ does the term $Be^{zt}$ disappear?
> Here $z_0=-1$, $p=-4$, $z=-2$.
> $A=\dfrac{p-z_0}{p-z}=\dfrac{-4+1}{-4+2}=\dfrac{-3}{-2}=\dfrac32$. $B=\dfrac{z-z_0}{z-p}=\dfrac{-2+1}{-2+4}=-\dfrac12$.
> $y(t)=\dfrac32e^{-4t}-\dfrac12e^{-2t}$. Check at $t=0$: $\dfrac32-\dfrac12=1=\hat g(\infty)\,u(0)$.
> $B=0$ needs $z=z_0=-1$. For $u=e^{-t}$: $\hat y=\dfrac{s+1}{s+4}\cdot\dfrac{1}{s+1}=\dfrac{1}{s+4}$, so $y=e^{-4t}$. The input mode $e^{-t}$ does not appear at the output: it is blocked by the zero.

## 8. State-space representation of LTI systems (slides 29-30)
![[ee502_eee501alllecturenotesabo_p029.jpg]]
![[ee502_eee501alllecturenotesabo_p030.jpg]]

**Notes.** Every lumped LTI system with $p$ inputs, $q$ outputs and $n$ states can be written

$$\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}\quad(4),\qquad \mathbf{y}=C\mathbf{x}+D\mathbf{u}\quad(5)$$

with $A\in\mathbb{R}^{n\times n}$, $B\in\mathbb{R}^{n\times p}$, $C\in\mathbb{R}^{q\times n}$, $D\in\mathbb{R}^{q\times p}$. Laplace transform with initial state $\mathbf{x}(0)$:

$$\hat{\mathbf{x}}(s)=(sI-A)^{-1}\mathbf{x}(0)+(sI-A)^{-1}B\,\hat{\mathbf{u}}(s)$$

$$\hat{\mathbf{y}}(s)=\underbrace{C(sI-A)^{-1}\mathbf{x}(0)}_{\text{zero-input}}+\underbrace{\bigl[C(sI-A)^{-1}B+D\bigr]\hat{\mathbf{u}}(s)}_{\text{zero-state}}$$

$$\hat G(s)=C(sI-A)^{-1}B+D$$

$\hat G$ is rational and proper, with $\hat G(\infty)=D$. Many different $(A,B,C,D)$ give the same $\hat G$.

> [!warning] Watch out
> Every pole of $\hat G$ is an eigenvalue of $A$. The converse fails: a factor of $\det(sI-A)$ can cancel. Example: $A=\operatorname{diag}(-1,-2)$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&1\end{bmatrix}$ gives $\hat g=\dfrac{1}{s+1}$.

> [!info] How to compute $(sI-A)^{-1}$ by hand (beyond the slides)
> The inverse of a matrix is its adjugate divided by its determinant: $(sI-A)^{-1}=\dfrac{\operatorname{adj}(sI-A)}{\det(sI-A)}$.
> For a $2\times2$ matrix the adjugate is easy: swap the two diagonal entries and change the sign of the other two.
>
> $$\begin{bmatrix}a&b\\c&d\end{bmatrix}^{-1}=\frac{1}{ad-bc}\begin{bmatrix}d&-b\\-c&a\end{bmatrix}$$
>
> Steps for $\hat G(s)$: (1) write $sI-A$, (2) compute $\det(sI-A)$, (3) write the adjugate, (4) multiply $C\cdot\operatorname{adj}\cdot B$, (5) divide by the determinant and add $D$.
> $\det(sI-A)$ is the characteristic polynomial of $A$. Its roots are the eigenvalues of $A$. The entries of the adjugate are polynomials, so $\det(sI-A)$ is the only denominator in $\hat G$. This is why the poles of $\hat G$ can only be eigenvalues of $A$.

> [!question]- Check (slide 29): A system is given by $\dot x_1=-x_1+2x_2+u_1$, $\dot x_2=-3x_2+u_1-u_2$, $y=x_1+4u_2$. Give $n$, $p$, $q$ and the matrices $A$, $B$, $C$, $D$ with their sizes. Why is the output equation called algebraic?
> $n=2$ states, $p=2$ inputs, $q=1$ output.
> $A=\begin{bmatrix}-1&2\\0&-3\end{bmatrix}$ ($2\times2$), $B=\begin{bmatrix}1&0\\1&-1\end{bmatrix}$ ($2\times2$, $n\times p$).
> $C=\begin{bmatrix}1&0\end{bmatrix}$ ($1\times2$, $q\times n$), $D=\begin{bmatrix}0&4\end{bmatrix}$ ($1\times2$, $q\times p$).
> Row $i$ of $A$ and $B$ holds the coefficients of the equation for $\dot x_i$.
> The output equation has no derivative. It gives $y(t)$ directly from $x(t)$ and $u(t)$ at the same time instant, so it is an algebraic equation, not a differential equation.

> [!question]- Check (slide 30): Compute $\hat G(s)$ step by step for $\dot x_1=x_1+2x_2$, $\dot x_2=3x_1-4x_2+u$, $y=x_1+x_2+2u$. What are the poles and what is $\hat G(\infty)$?
> $A=\begin{bmatrix}1&2\\3&-4\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$, $C=\begin{bmatrix}1&1\end{bmatrix}$, $D=2$.
> Step 1: $sI-A=\begin{bmatrix}s-1&-2\\-3&s+4\end{bmatrix}$.
> Step 2: $\det(sI-A)=(s-1)(s+4)-(-2)(-3)=s^2+3s-4-6=s^2+3s-10=(s-2)(s+5)$.
> Step 3: $\operatorname{adj}(sI-A)=\begin{bmatrix}s+4&2\\3&s-1\end{bmatrix}$.
> Step 4: $\operatorname{adj}\cdot B=\begin{bmatrix}2\\s-1\end{bmatrix}$ (the second column). $C\cdot\begin{bmatrix}2\\s-1\end{bmatrix}=2+s-1=s+1$.
> Step 5: $\hat G(s)=\dfrac{s+1}{(s-2)(s+5)}+2=\dfrac{2s^2+7s-19}{(s-2)(s+5)}$.
> Poles: $2$ and $-5$, the eigenvalues of $A$ (nothing cancels). $\hat G(\infty)=2=D$: the first part is strictly proper and vanishes at infinity.

## 9. Example: mass-spring-damper (slide 31)
![[ee502_eee501alllecturenotesabo_p031.jpg]]

**Notes.** $m\ddot y+b\dot y+ky=u$. States $x_1=y$, $x_2=\dot y$:

$$\begin{bmatrix}\dot x_1\\ \dot x_2\end{bmatrix}=\begin{bmatrix}0&1\\-\frac km&-\frac bm\end{bmatrix}\begin{bmatrix}x_1\\x_2\end{bmatrix}+\begin{bmatrix}0\\ \frac1m\end{bmatrix}u,\qquad y=\begin{bmatrix}1&0\end{bmatrix}\mathbf{x}$$

$$\hat g(s)=\begin{bmatrix}1&0\end{bmatrix}\begin{bmatrix}s&-1\\ \frac km&s+\frac bm\end{bmatrix}^{-1}\begin{bmatrix}0\\ \frac1m\end{bmatrix}=\frac{1}{ms^2+bs+k}$$

For $m=1$, $b=3$, $k=2$: $\hat g=\dfrac{1}{(s+1)(s+2)}=\dfrac{1}{s+1}-\dfrac{1}{s+2}$, so $g(t)=e^{-t}-e^{-2t}$ for $t\ge0$ and $0$ for $t<0$.

Recipe for an $n$-th order ODE: states are $y$ and its derivatives up to order $n-1$. The last row of $A$ and $B$ comes from the ODE solved for the highest derivative.

> [!example] Complete response (ours)
> Same system, $\mathbf{x}(0)=\begin{bmatrix}1&0\end{bmatrix}^{\mathsf T}$, unit-step force. $y_{zi}=2e^{-t}-e^{-2t}$, $y_{zs}=\frac12-e^{-t}+\frac12e^{-2t}$, total $y=\frac12+e^{-t}-\frac12e^{-2t}$.

> [!warning] Watch out
> The slide prints the second state as "$x_1:=\dot y$". It is $x_2:=\dot y$.

> [!question]- Check (slide 31): Use the same method on a series RLC circuit: $L\,\dfrac{di}{dt}+Ri+v_C=u$ and $C\,\dfrac{dv_C}{dt}=i$, with $R=5$, $L=1$, $C=0.25$. The input is the source voltage $u$, the output is $y=v_C$. Choose $x_1=v_C$, $x_2=i$. Find the state-space matrices, $\hat g(s)$ and $g(t)$.
> Solve each equation for the derivative: $\dot x_1=\dfrac{1}{C}x_2=4x_2$, $\dot x_2=-\dfrac1Lx_1-\dfrac RLx_2+\dfrac1Lu=-x_1-5x_2+u$.
> $A=\begin{bmatrix}0&4\\-1&-5\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$, $C_{out}=\begin{bmatrix}1&0\end{bmatrix}$, $D=0$. ($C_{out}$ is the output matrix, not the capacitance.)
> $sI-A=\begin{bmatrix}s&-4\\1&s+5\end{bmatrix}$, $\det=s(s+5)+4=s^2+5s+4=(s+1)(s+4)$.
> $\operatorname{adj}(sI-A)=\begin{bmatrix}s+5&4\\-1&s\end{bmatrix}$. $\operatorname{adj}\cdot B=\begin{bmatrix}4\\s\end{bmatrix}$, and $C_{out}$ picks the first entry: $4$.
> $\hat g(s)=\dfrac{4}{(s+1)(s+4)}=\dfrac{4/3}{s+1}-\dfrac{4/3}{s+4}$.
> $g(t)=\dfrac43\left(e^{-t}-e^{-4t}\right)$ for $t\ge0$, and $0$ for $t<0$.
> Check: $\hat g(0)=1$. At DC the capacitor voltage equals the source voltage.

## 10. Linearization (slides 32-34)
![[ee502_eee501alllecturenotesabo_p032.jpg]]
![[ee502_eee501alllecturenotesabo_p033.jpg]]
![[ee502_eee501alllecturenotesabo_p034.jpg]]

**Notes.** Nonlinear model: $\dot{\mathbf{x}}=\mathbf{f}(\mathbf{x},\mathbf{u},t)$ (6), $\mathbf{y}=\mathbf{h}(\mathbf{x},\mathbf{u},t)$ (7). An **operating trajectory** $(\mathbf{x}_o(t),\mathbf{u}_o(t))$ satisfies (6). Write $\mathbf{x}=\mathbf{x}_o+\tilde{\mathbf{x}}$, $\mathbf{u}=\mathbf{u}_o+\tilde{\mathbf{u}}$, Taylor-expand, drop higher-order terms:

$$\dot{\tilde{\mathbf{x}}}\cong A(t)\tilde{\mathbf{x}}+B(t)\tilde{\mathbf{u}},\qquad \tilde{\mathbf{y}}\cong C(t)\tilde{\mathbf{x}}+D(t)\tilde{\mathbf{u}}$$

$$A=\Bigl[\frac{\partial f_i}{\partial x_j}\Bigr],\quad B=\Bigl[\frac{\partial f_i}{\partial u_j}\Bigr],\quad C=\Bigl[\frac{\partial h_i}{\partial x_j}\Bigr],\quad D=\Bigl[\frac{\partial h_i}{\partial u_j}\Bigr],\quad\text{all evaluated at }(\mathbf{x}_o,\mathbf{u}_o)$$

Steps: (1) check the operating point satisfies (6), (2) compute the partial derivatives, (3) evaluate them at the operating point, (4) write the model for the deviations. About a constant equilibrium the result is LTI. About a moving trajectory it is linear time-varying.

**Slide example.** $\dot x=\sin x+u_1^2+u_2^2-t$, with $x_o=0$, $\mathbf{u}_o=\begin{bmatrix}0\\ \sqrt t\end{bmatrix}$. Check: $\sin0+0+t-t=0=\dot x_o$. Then $A=\cos x|_{0}=1$, $B=\begin{bmatrix}2u_1&2u_2\end{bmatrix}_o=\begin{bmatrix}0&2\sqrt t\end{bmatrix}$:

$$\dot{\tilde x}=\tilde x+2\sqrt t\,\tilde u_2$$

> [!example] Pendulum (ours)
> $ml^2\ddot\theta=-mgl\sin\theta+u$, states $(\theta,\dot\theta)$. $A=\begin{bmatrix}0&1\\-\frac gl\cos\theta_o&0\end{bmatrix}$, $B=\begin{bmatrix}0\\ \frac{1}{ml^2}\end{bmatrix}$. Hanging ($\theta_o=0$): eigenvalues $\pm j\sqrt{g/l}$, oscillation. Upright ($\theta_o=\pi$): eigenvalues $\pm\sqrt{g/l}$, unstable.

> [!warning] Watch out
> - Slide 33 gives the sizes of $C(t)$ and $D(t)$ as $n\times n$ and $n\times p$. They are $q\times n$ and $q\times p$.
> - The linear model is in the deviations $\tilde{\mathbf{x}}=\mathbf{x}-\mathbf{x}_o$, not in $\mathbf{x}$.
> - $\tilde u_1$ drops out in the slide example because $2u_1=0$ at $u_{1o}=0$.

> [!info] The step the slide skips, and what an equilibrium is (beyond the slides)
> Slide 32 writes $\dot{\mathbf{x}}_o+\dot{\tilde{\mathbf{x}}}=\mathbf{f}(\mathbf{x}_o,\mathbf{u}_o,t)+A\tilde{\mathbf{x}}+B\tilde{\mathbf{u}}+\cdots$. The operating trajectory satisfies $\dot{\mathbf{x}}_o=\mathbf{f}(\mathbf{x}_o,\mathbf{u}_o,t)$. Subtract this from both sides. Only the deviation terms stay: $\dot{\tilde{\mathbf{x}}}=A\tilde{\mathbf{x}}+B\tilde{\mathbf{u}}+\cdots$. The dots are terms with products of small quantities ($\tilde x^2$, $\tilde x\tilde u$, ...). They are much smaller than the linear terms when the deviations are small, so they are dropped.
> An **equilibrium** is an operating point that does not move, for a system where $\mathbf{f}$ does not depend on $t$ directly: $\mathbf{x}_o$ and $\mathbf{u}_o$ are constants with $\mathbf{f}(\mathbf{x}_o,\mathbf{u}_o)=\mathbf{0}$, so $\dot{\mathbf{x}}_o=\mathbf{0}$. To find it, set all derivatives to zero and solve.
> Row $i$ of a Jacobian belongs to the function $f_i$. Column $j$ belongs to the variable $x_j$ (or $u_j$).

> [!question]- Check (slide 32): A pendulum with friction obeys $ml^2\ddot\theta=-mgl\sin\theta-b\dot\theta+u$ with $m=0.5$, $l=2$, $g=9.81$, $b=0.4$. A constant torque $u_o$ holds it at $\theta_o=\pi/6$ (30 degrees). Find $u_o$, the Jacobians $A$ and $B$, and the eigenvalues of $A$. Is the equilibrium stable?
> States $x_1=\theta$, $x_2=\dot\theta$: $f_1=x_2$, $f_2=-\dfrac gl\sin x_1-\dfrac{b}{ml^2}x_2+\dfrac{1}{ml^2}u$. Here $ml^2=0.5\cdot4=2$ and $g/l=4.905$.
> Equilibrium: $x_2=0$ and $f_2=0$, so $u_o=mgl\sin\theta_o=0.5\cdot9.81\cdot2\cdot0.5=4.905$ N m.
> $A=\begin{bmatrix}\dfrac{\partial f_1}{\partial x_1}&\dfrac{\partial f_1}{\partial x_2}\\ \dfrac{\partial f_2}{\partial x_1}&\dfrac{\partial f_2}{\partial x_2}\end{bmatrix}=\begin{bmatrix}0&1\\-\dfrac gl\cos x_1&-\dfrac{b}{ml^2}\end{bmatrix}$. At $x_1=\pi/6$: $-4.905\cdot0.8660=-4.248$ and $-0.4/2=-0.2$.
> $A=\begin{bmatrix}0&1\\-4.248&-0.2\end{bmatrix}$, $B=\begin{bmatrix}0\\ \dfrac{1}{ml^2}\end{bmatrix}=\begin{bmatrix}0\\0.5\end{bmatrix}$.
> $\det(sI-A)=s^2+0.2s+4.248$. Roots: $s=-0.1\pm j\sqrt{4.248-0.01}=-0.1\pm2.059j$. Both real parts are negative, so the equilibrium is stable: a slowly decaying oscillation around 30 degrees.
> The model is $\dot{\tilde{\mathbf{x}}}=A\tilde{\mathbf{x}}+B\tilde u$ with $\tilde x_1=\theta-\pi/6$ and $\tilde u=u-4.905$.

> [!question]- Check (slide 33): A tank model is $\dot x=-2\sqrt{x}+u$ with the measured output $y=x^2$. The input is held at $u_o=4$. Find the equilibrium $x_o$, then $A$, $B$, $C$, $D$ and the transfer function of the linear model.
> Equilibrium: $0=-2\sqrt{x_o}+4$, so $\sqrt{x_o}=2$ and $x_o=4$. Output there: $y_o=16$.
> $A=\dfrac{\partial f}{\partial x}=-\dfrac{1}{\sqrt x}$, at $x_o=4$: $A=-0.5$. $B=\dfrac{\partial f}{\partial u}=1$.
> $C=\dfrac{\partial h}{\partial x}=2x$, at $x_o=4$: $C=8$. $D=\dfrac{\partial h}{\partial u}=0$.
> Linear model: $\dot{\tilde x}=-0.5\,\tilde x+\tilde u$, $\tilde y=8\,\tilde x$, with $\tilde x=x-4$, $\tilde u=u-4$, $\tilde y=y-16$.
> $\hat g(s)=C(s-A)^{-1}B+D=\dfrac{8}{s+0.5}$.
> Sizes: $n=1$, $p=1$, $q=1$. In general $C$ is $q\times n$ and $D$ is $q\times p$.

> [!question]- Check (slide 34): Take $\dot x=-x^2+u$ with the operating functions $x_o(t)=\dfrac{1}{t+1}$, $u_o(t)=0$. Check that this is a valid operating trajectory, then linearize. Is the result time-invariant?
> Check: $\dot x_o=-\dfrac{1}{(t+1)^2}$ and $f(x_o,u_o)=-x_o^2+0=-\dfrac{1}{(t+1)^2}$. Equal, so (6) holds.
> $A(t)=\dfrac{\partial f}{\partial x}\Big|_o=-2x_o=-\dfrac{2}{t+1}$. $B(t)=\dfrac{\partial f}{\partial u}=1$.
> Linear model: $\dot{\tilde x}=-\dfrac{2}{t+1}\,\tilde x+\tilde u$.
> $A(t)$ depends on $t$, so the model is linear **time-varying**. The reason is that the operating point moves. The slide example is the same case: there $B(t)=\begin{bmatrix}0&2\sqrt t\end{bmatrix}$ depends on $t$.

## 11. Modelling example: double pendulum (slide 35)
![[ee502_eee501alllecturenotesabo_p035.jpg]]

**Notes.** Masses $m_1,m_2$ on rods $l_1,l_2$, angles $\theta_1,\theta_2$ from the vertical, horizontal force $u$ on $m_2$. For small angles use $\sin\theta_i\cong\theta_i$, $\cos\theta_i\cong1$, $\sin(\theta_2-\theta_1)\cong\theta_2-\theta_1$, and drop products of small quantities:

$$\ddot\theta_1=-\frac{(m_1+m_2)g}{m_1l_1}\theta_1+\frac{m_2g}{m_1l_1}\theta_2,\qquad \ddot\theta_2=-\frac{g}{l_2}\theta_2+\frac{1}{m_2l_2}u$$

With $x_1=\theta_1$, $x_2=\dot\theta_1$, $x_3=\theta_2$, $x_4=\dot\theta_2$:

$$\dot{\mathbf{x}}=\begin{bmatrix}0&1&0&0\\-\frac{(m_1+m_2)g}{m_1l_1}&0&\frac{m_2g}{m_1l_1}&0\\0&0&0&1\\0&0&-\frac{g}{l_2}&0\end{bmatrix}\mathbf{x}+\begin{bmatrix}0\\0\\0\\ \frac{1}{m_2l_2}\end{bmatrix}u$$

The Jacobian method about $\mathbf{x}_o=\mathbf{0}$, $u_o=0$ gives the same matrices.

> [!warning] Watch out
> The slide states the assumption as "$\sin\theta_1\cong0$". The matrix shown needs $\sin\theta_i\cong\theta_i$ (first-order terms kept).

> [!question]- Check (slide 35): Put $m_1=2$, $m_2=1$, $l_1=1$, $l_2=0.5$ and $g=10$ into the slide's matrices. Write $A$ and $B$, find the eigenvalues of $A$, and the transfer function from $u$ to $\theta_1$. What does the zero in row 4, column 1 of $A$ mean?
> Entries: $-\dfrac{(m_1+m_2)g}{m_1l_1}=-\dfrac{3\cdot10}{2\cdot1}=-15$, $\dfrac{m_2g}{m_1l_1}=\dfrac{10}{2}=5$, $-\dfrac{g}{l_2}=-\dfrac{10}{0.5}=-20$, $\dfrac{1}{m_2l_2}=\dfrac{1}{0.5}=2$.
> $A=\begin{bmatrix}0&1&0&0\\-15&0&5&0\\0&0&0&1\\0&0&-20&0\end{bmatrix}$, $B=\begin{bmatrix}0\\0\\0\\2\end{bmatrix}$.
> The equations are $\ddot\theta_1=-15\theta_1+5\theta_2$ and $\ddot\theta_2=-20\theta_2+2u$. $A$ is block upper triangular, so $\det(sI-A)=(s^2+15)(s^2+20)$.
> Eigenvalues: $\pm j\sqrt{15}\approx\pm3.873j$ and $\pm j\sqrt{20}\approx\pm4.472j$. All on the imaginary axis: two oscillations that do not decay (the model has no friction).
> Transfer function: $\hat\theta_2=\dfrac{2}{s^2+20}\hat u$ and $\hat\theta_1=\dfrac{5}{s^2+15}\hat\theta_2$, so $\dfrac{\hat\theta_1}{\hat u}=\dfrac{10}{(s^2+15)(s^2+20)}$.
> The zero in row 4, column 1 means that $\theta_1$ does not appear in the equation for $\ddot\theta_2$. In this small-angle model the lower pendulum moves as if it were alone, and it drives the upper one through the entry $5$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Linear | superposition of (initial state, input) pairs |
| Impulse response | $y(t)=\int_{t_0}^{t}g(t,\tau)u(\tau)\,d\tau$ (relaxed, causal) |
| Convolution (LTI) | $y(t)=\int_0^t g(t-\tau)u(\tau)\,d\tau$ |
| Transfer function | $\hat y=\hat g\hat u$, $\hat g=\mathcal{L}\{g\}$ |
| Delay | $\hat g=e^{-sT}$, irrational, distributed |
| Properness | proper $\deg N\le\deg D$, strictly $<$, biproper $=$, improper $>$ |
| Poles / zeros | roots of $D$ / $N$ after cancelling common factors |
| Matrix poles | roots of the lcm of all entry denominators |
| Blocking zero | $\hat G(\lambda)=0$ |
| State space | $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$ |
| Transfer matrix | $\hat G(s)=C(sI-A)^{-1}B+D$ |
| Complete response | $\hat{\mathbf{y}}=C(sI-A)^{-1}\mathbf{x}(0)+\hat G\hat{\mathbf{u}}$ |
| Linearization | $A=\partial\mathbf{f}/\partial\mathbf{x}$, $B=\partial\mathbf{f}/\partial\mathbf{u}$, $C=\partial\mathbf{h}/\partial\mathbf{x}$, $D=\partial\mathbf{h}/\partial\mathbf{u}$ at $(\mathbf{x}_o,\mathbf{u}_o)$ |

## Check yourself
> [!question]- 1. $\dot x=-2x+u$, $y=x$, $x(0)=3$, $u=1$. Find $y_{zi}$, $y_{zs}$ and $y$.
> $y_{zi}=3e^{-2t}$. $y_{zs}=\int_0^te^{-2(t-\tau)}d\tau=\frac12-\frac12e^{-2t}$. $y=\frac12+\frac52e^{-2t}$.

> [!question]- 2. Is $y(t)=u(2t)$ time-invariant?
> Response to $u(t-T)$: $u(2t-T)$. Shifted output: $y(t-T)=u(2t-2T)$. Different for $T\neq0$, so **not time-invariant**.

> [!question]- 3. Poles, zeros and properness of $\hat g(s)=\dfrac{s+1}{s^2+5s+6}$
> $D=(s+2)(s+3)$, coprime with $N$. Poles $-2,-3$, zero $-1$, strictly proper, one zero at infinity.

> [!question]- 4. $\hat g(s)=\dfrac{s+3}{s+1}$, relaxed. Output for a unit step and for $u=e^{-3t}$?
> Step: $\hat y=\dfrac{s+3}{s(s+1)}=\dfrac3s-\dfrac{2}{s+1}$, $y=3-2e^{-t}$. For $e^{-3t}$: the zero cancels, $\hat y=\dfrac{1}{s+1}$, $y=e^{-t}$.

> [!question]- 5. Write $A,B,C,D$ and $\hat g(s)$ for $\ddot y+4\dot y+3y=2u$.
> $A=\begin{bmatrix}0&1\\-3&-4\end{bmatrix}$, $B=\begin{bmatrix}0\\2\end{bmatrix}$, $C=\begin{bmatrix}1&0\end{bmatrix}$, $D=0$. $\hat g=\dfrac{2}{(s+1)(s+3)}$.

> [!question]- 6. Linearize $\dot x_1=x_2$, $\dot x_2=-\sin x_1-x_2+u$ about $\mathbf{x}_o=(\pi,0)$, $u_o=0$. Eigenvalues?
> $A=\begin{bmatrix}0&1\\1&-1\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$. $\det(sI-A)=s^2+s-1$, roots $\dfrac{-1\pm\sqrt5}{2}\approx0.618,\ -1.618$. One positive eigenvalue: unstable.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L01 - Mathematical description of systems]]. Next: [[EE502 L03 - Vector spaces, norms and rank]]
- Used by Quiz 1 (state space and transfer functions of the two models) and Quiz 2 (slides 15-35: impulse response, transfer functions, state space, linearization).
- Full step-by-step notes (PDF): [EE502_Lecture_02_LTI_Models.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_02/EE502_Lecture_02_LTI_Models.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_02/EE502_Lecture_02_LTI_Models.pdf`
- Original slides (PDF, pp. 12-35): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L02 - LTI models and linearization - quiz]]

Slides not embedded: 12, 13, 14 (title, topic list repeated, chapter title).
