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

## 4. Example: feedback loop with a unit delay (slide 21)
![[ee502_eee501alllecturenotesabo_p021.jpg]]

**Notes.** Negative feedback, gain $a$ and a unit delay in the forward path. Loop equation: $y(t)=a\,r(t-1)-a\,y(t-1)$. With $r=\delta$ and a relaxed system, unrolling gives one echo per trip around the loop:

$$g_f(t)=\sum_{i=1}^{\infty}(-1)^{i-1}a^i\,\delta(t-i),\qquad y(t)=\sum_{i=1}^{\infty}(-1)^{i-1}a^i\,r(t-i)$$

In the $s$-domain: $\hat g_f(s)=\dfrac{ae^{-s}}{1+ae^{-s}}$. For a unit step and $a=0.5$ the output goes $0.5,\ 0.25,\ 0.375,\ 0.3125,\dots\to\frac{a}{1+a}=\frac13$. The echoes die out exactly when $|a|<1$. The system is LTI and causal but distributed.

> [!warning] Watch out
> Slide typos: the third term is printed $a^3(t-3)$, it is $a^3\delta(t-3)$. The integrand is printed $g_f(t)r(\tau)$, it is $g_f(t-\tau)r(\tau)$.

## 5. Transfer function and transfer matrix (slides 22-23)
![[ee502_eee501alllecturenotesabo_p022.jpg]]
![[ee502_eee501alllecturenotesabo_p023.jpg]]

**Notes.** Take the Laplace transform of the convolution, swap the order of integration, substitute $\mu=t-\tau$, and use $g(\mu)=0$ for $\mu<0$:

$$\hat y(s)=\hat g(s)\,\hat u(s),\qquad \hat g(s)=\int_0^\infty g(\mu)e^{-s\mu}\,d\mu$$

$\hat g(s)$ is the **transfer function**: the Laplace transform of the impulse response. For $p$ inputs and $q$ outputs, $\hat G(s)=\int_0^\infty G(t)e^{-st}\,dt=[\hat g_{ij}(s)]_{q\times p}$ is the **transfer matrix**, and $\hat g_{ij}$ is the transfer function from input $j$ to output $i$.

> [!warning] Watch out
> $\hat y=\hat g\hat u$ is only the zero-state response. A nonzero initial state adds a term (section 8).

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

## 7. Transfer matrix terminology, blocking zeros (slides 27-28)
![[ee502_eee501alllecturenotesabo_p027.jpg]]
![[ee502_eee501alllecturenotesabo_p028.jpg]]

**Notes.** $\hat G(s)$ is strictly proper if $\hat G(\infty)=0$, proper if $\hat G(\infty)=K$ (a constant matrix). Square $\hat G$ is biproper (it and its inverse are proper) exactly when $K$ is nonsingular.

- **Pole** of $\hat G$: a pole of at least one entry. Equivalent: a root of the least common multiple of the denominators of all entries (coprime form).
- **Blocking zero**: $\hat G(\lambda)=0$, a zero of every entry.

Meaning of a zero. Take $\hat g(s)=\dfrac{s-z_0}{s-p}$ and input $u=e^{zt}$. If $z\ne z_0$: $y(t)=Ae^{pt}+Be^{zt}$ with $A=\dfrac{p-z_0}{p-z}$, $B=\dfrac{z-z_0}{z-p}$. If $z=z_0$: the factor cancels, $\hat y=\dfrac{1}{s-p}$, $y=e^{pt}$. The zero blocks the input mode $e^{z_0t}$.

> [!example] Numbers
> $\hat g=\dfrac{s-2}{s+1}$. Step input: $y=3e^{-t}-2$. Input $e^{2t}$: $y=e^{-t}$, the growing input is blocked.

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

## 11. Modelling example: double pendulum (slide 35)
![[ee502_eee501alllecturenotesabo_p035.jpg]]

**Notes.** Masses $m_1,m_2$ on rods $l_1,l_2$, angles $\theta_1,\theta_2$ from the vertical, horizontal force $u$ on $m_2$. For small angles use $\sin\theta_i\cong\theta_i$, $\cos\theta_i\cong1$, $\sin(\theta_2-\theta_1)\cong\theta_2-\theta_1$, and drop products of small quantities:

$$\ddot\theta_1=-\frac{(m_1+m_2)g}{m_1l_1}\theta_1+\frac{m_2g}{m_1l_1}\theta_2,\qquad \ddot\theta_2=-\frac{g}{l_2}\theta_2+\frac{1}{m_2l_2}u$$

With $x_1=\theta_1$, $x_2=\dot\theta_1$, $x_3=\theta_2$, $x_4=\dot\theta_2$:

$$\dot{\mathbf{x}}=\begin{bmatrix}0&1&0&0\\-\frac{(m_1+m_2)g}{m_1l_1}&0&\frac{m_2g}{m_1l_1}&0\\0&0&0&1\\0&0&-\frac{g}{l_2}&0\end{bmatrix}\mathbf{x}+\begin{bmatrix}0\\0\\0\\ \frac{1}{m_2l_2}\end{bmatrix}u$$

The Jacobian method about $\mathbf{x}_o=\mathbf{0}$, $u_o=0$ gives the same matrices.

> [!warning] Watch out
> The slide states the assumption as "$\sin\theta_1\cong0$". The matrix shown needs $\sin\theta_i\cong\theta_i$ (first-order terms kept).

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

Slides not embedded: 12, 13, 14 (title, topic list repeated, chapter title).
