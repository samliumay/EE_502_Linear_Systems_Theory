---
course: EE 502 Linear System Theory
lecture: 9
title: LTI state equation solution
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 89-93)
full_notes: lecture_notes/lecture_09/EE502_Lecture_09_LTI_Solution.pdf
---
# EE 502 · Lecture 9 · Solution of the LTI state equation

> [!summary] In short
> - The state equation $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$ is solved with the integrating factor $e^{-At}$.
> - Solution: $\mathbf{x}(t)=e^{At}\mathbf{x}(0)+\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$. First term: zero-input part. Second term: zero-state part (a convolution).
> - In the Laplace domain the same formula is $\hat{\mathbf{x}}=(sI-A)^{-1}\mathbf{x}(0)+(sI-A)^{-1}B\hat{\mathbf{u}}$. Usually easier by hand.
> - The time functions in $e^{At}\mathbf{x}(0)$ (the modes) are $t^{j}e^{\lambda_i t}$ with $j<m_i$, where $m_i$ is the exponent of $\lambda_i$ in the **minimal** polynomial.
> - Extra (Chen 4.2.1, not on the slides): exact sampling under a zero-order hold, $A_d=e^{AT}$, $B_d=\int_0^T e^{A\sigma}d\sigma\,B$.

Slide numbers below are pages of the 220-page ABO file. Midterm material.

## 1. State trajectory and response (slide 90)
![[ee502_eee501alllecturenotesabo_p090.jpg]]

**Notes.** The LTI state representation is
$$\dot{\mathbf{x}}(t)=A\mathbf{x}(t)+B\mathbf{u}(t),\qquad \mathbf{y}(t)=C\mathbf{x}(t)+D\mathbf{u}(t),$$
with $A\in\mathbb{R}^{n\times n}$, $B\in\mathbb{R}^{n\times p}$, $C\in\mathbb{R}^{q\times n}$, $D\in\mathbb{R}^{q\times p}$. The trajectory is $\mathbf{x}(t)$, the response is $\mathbf{y}(t)$.

Derivation (four lines):
1. Multiply on the **left** by $e^{-At}$: $e^{-At}\dot{\mathbf{x}}-e^{-At}A\mathbf{x}=e^{-At}B\mathbf{u}$.
2. The left side is $\tfrac{d}{dt}\bigl[e^{-At}\mathbf{x}(t)\bigr]$ (product rule, $\tfrac{d}{dt}e^{-At}=-e^{-At}A$).
3. Integrate from $0$ to $t$: $e^{-At}\mathbf{x}(t)-\mathbf{x}(0)=\int_0^t e^{-A\tau}B\mathbf{u}(\tau)\,d\tau$.
4. Multiply on the left by $e^{At}$, using $e^{At}e^{-A\tau}=e^{A(t-\tau)}$:

$$\mathbf{x}(t)=e^{At}\mathbf{x}(0)+\int_{0}^{t}e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau \tag{1}$$
$$\mathbf{y}(t)=Ce^{At}\mathbf{x}(0)+\int_{0}^{t}Ce^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau+D\mathbf{u}(t) \tag{2}$$

> [!example] Scalar warm-up: $\dot x=-2x+u$, $x(0)=1$, unit step
> Zero-input part: $e^{-2t}$. Zero-state part: $e^{-2t}\int_0^t e^{2\tau}d\tau=\tfrac12(1-e^{-2t})$.
> Sum: $x(t)=\tfrac12+\tfrac12e^{-2t}$. Check: $x(0)=1$, and $\dot x=-e^{-2t}=-2x+1$.

> [!info] Checking formula (1) by differentiation (beyond the slides)
> The slide derives (1) but does not check it. The check uses the Leibniz rule for an integral whose upper limit and integrand both depend on $t$:
> $$\frac{d}{dt}\int_0^t F(t,\tau)\,d\tau=F(t,t)+\int_0^t\frac{\partial F}{\partial t}(t,\tau)\,d\tau .$$
> Here $F(t,\tau)=e^{A(t-\tau)}B\mathbf{u}(\tau)$. So $F(t,t)=e^{A\cdot 0}B\mathbf{u}(t)=B\mathbf{u}(t)$ and $\tfrac{\partial F}{\partial t}=Ae^{A(t-\tau)}B\mathbf{u}(\tau)$.
> The matrix $A$ is constant, so it can be moved in front of the integral. It must stay on the left of $e^{A(t-\tau)}$.

> [!question]- Check (slide 90, derivation): Differentiate formula (1) and show that it satisfies $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$ and the initial condition. Where does the term $B\mathbf{u}(t)$ come from?
> First term: $\tfrac{d}{dt}e^{At}\mathbf{x}(0)=Ae^{At}\mathbf{x}(0)$.
> Second term (Leibniz rule): $\tfrac{d}{dt}\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau=e^{A\cdot 0}B\mathbf{u}(t)+A\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$.
> Sum: $\dot{\mathbf{x}}=A\Bigl[e^{At}\mathbf{x}(0)+\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau\Bigr]+B\mathbf{u}(t)=A\mathbf{x}+B\mathbf{u}$.
> The term $B\mathbf{u}(t)$ comes from the upper limit of the integral: the integrand at $\tau=t$ is $e^{0}B\mathbf{u}(t)$.
> Initial condition: at $t=0$ the integral is over an interval of length zero, so $\mathbf{x}(0)=e^{0}\mathbf{x}(0)=\mathbf{x}(0)$.

> [!question]- Check (slide 90, computation): $A$ has rows $(0,\ 1)$ and $(-2,\ -3)$, $B=(0,\ 1)^{\mathsf T}$, $\mathbf{x}(0)=(1,\ 0)^{\mathsf T}$, unit step input. Given $e^{At}$ with rows $(2e^{-t}-e^{-2t},\ e^{-t}-e^{-2t})$ and $(-2e^{-t}+2e^{-2t},\ -e^{-t}+2e^{-2t})$, find $\mathbf{x}(t)$ with formula (1) and check it.
> Zero-input part: $e^{At}\mathbf{x}(0)$ is the first column of $e^{At}$: $\bigl(2e^{-t}-e^{-2t},\ -2e^{-t}+2e^{-2t}\bigr)^{\mathsf T}$.
> Zero-state part: with $u=1$ and the substitution $\sigma=t-\tau$, $\int_0^t e^{A(t-\tau)}B\,d\tau=\int_0^t e^{A\sigma}B\,d\sigma$. $e^{A\sigma}B$ is the second column:
> $$\int_0^t\begin{bmatrix}e^{-\sigma}-e^{-2\sigma}\\-e^{-\sigma}+2e^{-2\sigma}\end{bmatrix}d\sigma=\begin{bmatrix}(1-e^{-t})-\tfrac12(1-e^{-2t})\\-(1-e^{-t})+(1-e^{-2t})\end{bmatrix}=\begin{bmatrix}\tfrac12-e^{-t}+\tfrac12e^{-2t}\\e^{-t}-e^{-2t}\end{bmatrix}.$$
> Sum: $x_1(t)=\tfrac12+e^{-t}-\tfrac12e^{-2t}$, $x_2(t)=-e^{-t}+e^{-2t}$.
> Check: $x_1(0)=\tfrac12+1-\tfrac12=1$, $x_2(0)=0$. Row 1: $\dot x_1=-e^{-t}+e^{-2t}=x_2$. Row 2: $\dot x_2=e^{-t}-2e^{-2t}$, and $-2x_1-3x_2+1=(-1-2e^{-t}+e^{-2t})+(3e^{-t}-3e^{-2t})+1=e^{-t}-2e^{-2t}$. Both rows agree.

## 2. Zero-input and zero-state parts, Laplace form (slide 91)
![[ee502_eee501alllecturenotesabo_p091.jpg]]

**Notes.**

| | Zero-input part | Zero-state part |
|---|---|---|
| Switched off | the input, $\mathbf{u}\equiv 0$ | the initial state, $\mathbf{x}(0)=\mathbf{0}$ |
| Trajectory | $e^{At}\mathbf{x}(0)$ | $\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$ |
| Response | $Ce^{At}\mathbf{x}(0)$ | $\int_0^t Ce^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau+D\mathbf{u}(t)$ |

The full answer is the sum of the two parts (superposition).

With the unit impulse $\delta$, the zero-state response is the convolution of $\mathbf{u}$ with the impulse response matrix $H(t)=Ce^{At}B+D\delta(t)$.

Laplace form (use $\mathcal{L}\{\dot f\}=s\hat f(s)-f(0)$ on the state equation):
$$\begin{aligned}\hat{\mathbf{x}}(s)&=(sI-A)^{-1}\mathbf{x}(0)+(sI-A)^{-1}B\hat{\mathbf{u}}(s),\\ \hat{\mathbf{y}}(s)&=C(sI-A)^{-1}\mathbf{x}(0)+\bigl[C(sI-A)^{-1}B+D\bigr]\hat{\mathbf{u}}(s).\end{aligned}$$
So $\mathcal{L}\{e^{At}\}=(sI-A)^{-1}$, and the transfer matrix $G(s)=C(sI-A)^{-1}B+D$ is the Laplace transform of $H(t)$. $G(s)$ describes only the zero-state part.

> [!warning] Watch out
> Do not forget $D\mathbf{u}(t)$ in the output. The slide numbers both remarks "1)"; the second one is remark 2.

> [!info] Why $D\delta(t-\tau)$ gives back $D\mathbf{u}(t)$ (beyond the slides)
> The unit impulse has the sifting property: $\int_0^t\delta(t-\tau)\mathbf{u}(\tau)\,d\tau=\mathbf{u}(t)$. It picks the value of $\mathbf{u}$ at $\tau=t$. So $\int_0^t D\delta(t-\tau)\mathbf{u}(\tau)\,d\tau=D\mathbf{u}(t)$, and remark 1 is only another way to write (2).

> [!question]- Check (slide 91, superposition): A system gives $y(t)=3e^{-t}$ for the initial state $\mathbf{x}_a$ with $u\equiv 0$, and $y(t)=2-2e^{-t}$ for $\mathbf{x}(0)=\mathbf{0}$ with a unit step. Find $y(t)$ for $\mathbf{x}(0)=2\mathbf{x}_a$ and a step of height $5$. Does doubling only $\mathbf{x}(0)$ double the whole output?
> The zero-input response is linear in $\mathbf{x}(0)$: $2\cdot 3e^{-t}=6e^{-t}$.
> The zero-state response is linear in $u$: $5(2-2e^{-t})=10-10e^{-t}$.
> Sum: $y(t)=6e^{-t}+10-10e^{-t}=10-4e^{-t}$.
> Doubling only $\mathbf{x}(0)$ doubles only the zero-input part. With a unit step it gives $6e^{-t}+2-2e^{-t}=2+4e^{-t}$, which is not $2(2+e^{-t})$. The whole output doubles only if $\mathbf{x}(0)$ and $u$ are both doubled.

> [!question]- Check (slide 91, transfer function): $A$ has rows $(0,\ 1)$ and $(-2,\ -3)$, $B=(0,\ 1)^{\mathsf T}$, $C=(1,\ 0)$, $D=1$. Find $G(s)$ and $H(t)$. What are the values of the zero-state unit step response at $t=0^+$ and for $t\to\infty$?
> $\det(sI-A)=s^2+3s+2=(s+1)(s+2)$ and $(sI-A)^{-1}$ has rows $(s+3,\ 1)$ and $(-2,\ s)$, divided by $(s+1)(s+2)$.
> $C(sI-A)^{-1}B$ is the entry $(1,2)$: $\tfrac{1}{(s+1)(s+2)}$. So
> $$G(s)=\frac{1}{(s+1)(s+2)}+1=\frac{s^2+3s+3}{(s+1)(s+2)}.$$
> Partial fractions: $\tfrac{1}{(s+1)(s+2)}=\tfrac{1}{s+1}-\tfrac{1}{s+2}$, so $H(t)=e^{-t}-e^{-2t}+\delta(t)$. This agrees with $Ce^{At}B+D\delta(t)$.
> Step response: $y(t)=\int_0^t(e^{-\sigma}-e^{-2\sigma})\,d\sigma+1=\tfrac32-e^{-t}+\tfrac12e^{-2t}$.
> At $t=0^+$: $y=\tfrac32-1+\tfrac12=1$. This jump is the term $Du$. For $t\to\infty$: $y\to\tfrac32=G(0)$.

## 3. Solution via the Laplace transform (slide 92)
![[ee502_eee501alllecturenotesabo_p092.jpg]]

**Notes.** $A=\begin{bmatrix}1&1\\-1&1\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&0\end{bmatrix}$, $D=0$, unit step input, $\mathbf{x}(0)=(x_{01},x_{02})^{\mathsf T}$.

1. $\det(sI-A)=(s-1)^2+1$, eigenvalues $1\pm j$.
$$(sI-A)^{-1}=\frac{1}{(s-1)^2+1}\begin{bmatrix}s-1&1\\-1&s-1\end{bmatrix}$$
2. Shift rule: $\tfrac{s-1}{(s-1)^2+1}\to e^{t}\cos t$, $\tfrac{1}{(s-1)^2+1}\to e^{t}\sin t$. So
$$e^{At}=e^{t}\begin{bmatrix}\cos t&\sin t\\-\sin t&\cos t\end{bmatrix}.$$
3. Forced term: $(sI-A)^{-1}B\,\tfrac1s=\dfrac{1}{s[(s-1)^2+1]}\begin{bmatrix}s-1\\-1\end{bmatrix}$. Partial fractions:
$$\frac{s-1}{s[(s-1)^2+1]}=-\frac{1}{2s}+\frac12\frac{s-1}{(s-1)^2+1}+\frac12\frac{1}{(s-1)^2+1}.$$
   The second entry is the same with the last sign negative.
4. Result:
$$\mathbf{x}(t)=e^{t}\begin{bmatrix}\cos t&\sin t\\-\sin t&\cos t\end{bmatrix}\begin{bmatrix}x_{01}\\x_{02}\end{bmatrix}+\frac12\begin{bmatrix}e^{t}(\cos t+\sin t)-1\\e^{t}(\cos t-\sin t)-1\end{bmatrix}$$
$$y(t)=e^{t}(\cos t\,x_{01}+\sin t\,x_{02})+\tfrac12\bigl[e^{t}(\cos t+\sin t)-1\bigr]$$

Check at $t=0$: the forced term is $\mathbf{0}$ and the first term is $\mathbf{x}(0)$.

> [!question]- Check (slide 92, verify): The slide claims the forced (zero-state) term $\mathbf{x}_f(t)=\tfrac12\bigl(e^{t}(\cos t+\sin t)-1,\ e^{t}(\cos t-\sin t)-1\bigr)^{\mathsf T}$. Verify it by substitution into $\dot{\mathbf{x}}=A\mathbf{x}+B$.
> The equations are $\dot x_1=x_1+x_2+1$ and $\dot x_2=-x_1+x_2$ (unit step, $B=(1,0)^{\mathsf T}$).
> Derivatives (product rule): $\dot x_{f1}=\tfrac12e^{t}\bigl[(\cos t+\sin t)+(-\sin t+\cos t)\bigr]=e^{t}\cos t$ and $\dot x_{f2}=\tfrac12e^{t}\bigl[(\cos t-\sin t)+(-\sin t-\cos t)\bigr]=-e^{t}\sin t$.
> Row 1: $x_{f1}+x_{f2}+1=\tfrac12(2e^{t}\cos t-2)+1=e^{t}\cos t$. Equal.
> Row 2: $-x_{f1}+x_{f2}=\tfrac12(-2e^{t}\sin t)=-e^{t}\sin t$. Equal.
> Initial value: $\mathbf{x}_f(0)=\tfrac12(1-1,\ 1-1)^{\mathsf T}=\mathbf{0}$, as a zero-state term must have.

> [!question]- Check (slide 92, new system): $A$ has rows $(0,\ 1)$ and $(-4,\ 0)$, $B=(0,\ 1)^{\mathsf T}$, $\mathbf{x}(0)=\mathbf{0}$, unit step. Find $e^{At}$ and $\mathbf{x}(t)$ with the Laplace method.
> $\det(sI-A)=s^2+4$, eigenvalues $\pm 2j$.
> $$(sI-A)^{-1}=\frac{1}{s^2+4}\begin{bmatrix}s&1\\-4&s\end{bmatrix}\quad\Rightarrow\quad e^{At}=\begin{bmatrix}\cos 2t&\tfrac12\sin 2t\\-2\sin 2t&\cos 2t\end{bmatrix}$$
> using $\tfrac{s}{s^2+4}\to\cos 2t$ and $\tfrac{2}{s^2+4}\to\sin 2t$.
> Forced term: $(sI-A)^{-1}B\,\tfrac1s=\dfrac{1}{s(s^2+4)}\begin{bmatrix}1\\s\end{bmatrix}$.
> Entry 1: $\tfrac{1}{s(s^2+4)}=\tfrac{1}{4s}-\tfrac14\tfrac{s}{s^2+4}$, so $x_1(t)=\tfrac14(1-\cos 2t)$. Entry 2: $\tfrac{1}{s^2+4}$, so $x_2(t)=\tfrac12\sin 2t$.
> Check: $\dot x_1=\tfrac12\sin 2t=x_2$. $\dot x_2=\cos 2t$ and $-4x_1+1=-(1-\cos 2t)+1=\cos 2t$. $\mathbf{x}(0)=\mathbf{0}$.
> The eigenvalues are on the imaginary axis, so the step makes the state oscillate forever around $(\tfrac14,\ 0)$.

## 4. Modes of the zero-input response (slide 93)
![[ee502_eee501alllecturenotesabo_p093.jpg]]

**Notes.** Let the minimal polynomial of $A$ be $\Psi(\lambda)=\prod_{i=1}^{k}(\lambda-\lambda_i)^{m_i}$ with distinct $\lambda_i$. Then each entry of $e^{At}\mathbf{x}(0)$ and of $Ce^{At}\mathbf{x}(0)$ is a linear combination of
$$\bigl\{e^{\lambda_i t},\ te^{\lambda_i t},\ \dots,\ t^{m_i-1}e^{\lambda_i t}\bigr\}_{i=1,\dots,k}.$$
Reason: $e^{At}=Qe^{J_At}Q^{-1}$ with the Jordan form $J_A$, and a Jordan block of size $m$ gives powers of $t$ up to $t^{m-1}$. $m_i$ is the size of the largest block of $\lambda_i$.

> [!example] Same characteristic polynomial, different modes
> $A=\begin{bmatrix}0&1\\-1&-2\end{bmatrix}$: $\Delta=(\lambda+1)^2$ and $A+I\ne 0$, so $\Psi=(\lambda+1)^2$. Modes $e^{-t}$, $te^{-t}$:
> $$e^{At}=e^{-t}\begin{bmatrix}1+t&t\\-t&1-t\end{bmatrix}.$$
> $A'=-I$: same $\Delta$, but $\Psi=\lambda+1$, so $e^{A't}=e^{-t}I$ and there is no $te^{-t}$.

> [!warning] Watch out
> The power of $t$ comes from the exponent in $\Psi$, not from the multiplicity in $\Delta$. The rule says which functions *may* appear: a particular $\mathbf{x}(0)$ or $C$ can give some of them coefficient $0$. Poles of $G(s)$ are among the eigenvalues of $A$, but a cancellation can hide an eigenvalue.

> [!info] Exciting a single mode (beyond the slides)
> Let $\mathbf{v}$ be an eigenvector of $A$: $A\mathbf{v}=\lambda\mathbf{v}$. Then $A^k\mathbf{v}=\lambda^k\mathbf{v}$, and the power series of $e^{At}$ gives $e^{At}\mathbf{v}=e^{\lambda t}\mathbf{v}$.
> So the initial state $\mathbf{x}(0)=\mathbf{v}$ excites only the mode $e^{\lambda t}$: the state stays on the line through $\mathbf{v}$ and only its length changes.
> If $A$ has $n$ independent eigenvectors, write $\mathbf{x}(0)=\sum_i c_i\mathbf{v}_i$. Then $e^{At}\mathbf{x}(0)=\sum_i c_ie^{\lambda_it}\mathbf{v}_i$. The mode $e^{\lambda_it}$ is missing exactly when $c_i=0$.

> [!question]- Check (slide 93, single mode): $A$ has rows $(-1,\ 2)$ and $(0,\ -3)$. Which modes can appear in $e^{At}\mathbf{x}(0)$? Find one initial state that excites only $e^{-3t}$ and one that excites only $e^{-t}$. What does $\mathbf{x}(0)=(1,\ 1)^{\mathsf T}$ give?
> $A$ is triangular, so the eigenvalues are $-1$ and $-3$. They are distinct, so $\Psi(\lambda)=(\lambda+1)(\lambda+3)$ and the modes are $e^{-t}$ and $e^{-3t}$ (no powers of $t$).
> Eigenvector of $-3$: $(A+3I)\mathbf{v}=\mathbf{0}$ gives $2v_1+2v_2=0$, so $\mathbf{v}=(1,\ -1)^{\mathsf T}$. Then $\mathbf{x}(t)=e^{-3t}(1,\ -1)^{\mathsf T}$.
> Eigenvector of $-1$: $(A+I)\mathbf{v}=\mathbf{0}$ gives $v_2=0$, so $\mathbf{v}=(1,\ 0)^{\mathsf T}$. Then $\mathbf{x}(t)=e^{-t}(1,\ 0)^{\mathsf T}$.
> $(1,\ 1)^{\mathsf T}=2(1,\ 0)^{\mathsf T}-(1,\ -1)^{\mathsf T}$, so $\mathbf{x}(t)=2e^{-t}(1,\ 0)^{\mathsf T}-e^{-3t}(1,\ -1)^{\mathsf T}=\bigl(2e^{-t}-e^{-3t},\ e^{-3t}\bigr)^{\mathsf T}$. Both modes appear.
> Check of the last result: $\dot x_1=-2e^{-t}+3e^{-3t}=-x_1+2x_2$ and $\dot x_2=-3e^{-3t}=-3x_2$.

> [!question]- Check (slide 93, hidden mode): Same $A$ with rows $(-1,\ 2)$ and $(0,\ -3)$, now $B=(0,\ 1)^{\mathsf T}$, $C=(0,\ 1)$, $D=0$. Which modes appear in the zero-input response $y$? Find $G(s)$ and compare its poles with the eigenvalues of $A$.
> $y=x_2$ and the second state equation is $\dot x_2=-3x_2+u$. It does not contain $x_1$.
> Zero-input response: $y(t)=e^{-3t}x_2(0)$. Only the mode $e^{-3t}$ appears, for every $\mathbf{x}(0)$. The mode $e^{-t}$ lives in $x_1$, which the output does not see.
> $G(s)=C(sI-A)^{-1}B$ is the entry $(2,2)$ of $(sI-A)^{-1}$: $G(s)=\tfrac{1}{s+3}$.
> $G(s)$ has one pole, $-3$. The eigenvalue $-1$ is not a pole. The Fact only says which functions may appear. $C$ gave the mode $e^{-t}$ the coefficient $0$.

## 5. Discretization (not on the slides, Chen 4.2.1)
No slide pages. This section of our notes is written from the `.tex` alone.

**Notes.** A zero-order hold (ZOH) keeps the input constant between samples: $u(t)=u[k]$ for $kT\le t<(k+1)T$, with sampling period $T$. Write $\mathbf{x}[k]=\mathbf{x}(kT)$. Then the samples satisfy exactly
$$\mathbf{x}[k+1]=A_d\mathbf{x}[k]+B_d\mathbf{u}[k],\qquad A_d=e^{AT},\qquad B_d=\Bigl(\int_0^T e^{A\sigma}\,d\sigma\Bigr)B .$$
If $A$ is nonsingular, $B_d=A^{-1}(A_d-I)B$. $C$ and $D$ do not change. Eigenvalues map as $\lambda\mapsto e^{\lambda T}$: the left half-plane goes inside the unit circle.

> [!example] Motor model, $T=0.1$
> $A=\begin{bmatrix}0&1\\0&-2\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$. $e^{At}=\begin{bmatrix}1&\tfrac12(1-e^{-2t})\\0&e^{-2t}\end{bmatrix}$.
> $A_d=\begin{bmatrix}1&0.090635\\0&0.818731\end{bmatrix}$. $A$ is singular, so integrate: $B_d=\begin{bmatrix}\tfrac T2-\tfrac14(1-e^{-2T})\\ \tfrac12(1-e^{-2T})\end{bmatrix}=\begin{bmatrix}0.004683\\0.090635\end{bmatrix}$.

> [!warning] Watch out
> $A_d=e^{AT}$, not $I+AT$ (that is forward Euler, with $B_d\approx BT$). When $A$ has an eigenvalue $0$, the shortcut $A^{-1}(A_d-I)B$ does not exist.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Solution | $\mathbf{x}(t)=e^{At}\mathbf{x}(0)+\int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$ |
| Zero-input part | the terms with $\mathbf{x}(0)$: $e^{At}\mathbf{x}(0)$, $Ce^{At}\mathbf{x}(0)$ |
| Zero-state part | the terms with $\mathbf{u}$ (convolution, plus $D\mathbf{u}$) |
| Laplace | $\hat{\mathbf{x}}=(sI-A)^{-1}\mathbf{x}(0)+(sI-A)^{-1}B\hat{\mathbf{u}}$ |
| Transfer matrix | $G(s)=C(sI-A)^{-1}B+D$ |
| Impulse response | $H(t)=Ce^{At}B+D\delta(t)$, $\mathcal{L}\{H\}=G$ |
| Modes | $t^{j}e^{\lambda_i t}$, $j<m_i$ (exponents of the minimal polynomial $\Psi$) |
| ZOH sampling | $A_d=e^{AT}$, $B_d=\int_0^T e^{A\sigma}d\sigma\,B$ |

## Check yourself
> [!question]- 1. Solve $\dot x=-x+2u$, $x(0)=3$, unit step. Split into the two parts.
> Zero-input: $3e^{-t}$. Zero-state: $2e^{-t}\int_0^t e^{\tau}d\tau=2(1-e^{-t})$. Total: $x(t)=2+e^{-t}$.

> [!question]- 2. $A=\operatorname{diag}(-1,-2)$, $B=(1,1)^{\mathsf T}$, $\mathbf{x}(0)=\mathbf{0}$, unit step. Find $\mathbf{x}(t)$.
> $e^{A(t-\tau)}B=(e^{-(t-\tau)},e^{-2(t-\tau)})^{\mathsf T}$. Integrate each entry: $\mathbf{x}(t)=\bigl(1-e^{-t},\ \tfrac12(1-e^{-2t})\bigr)^{\mathsf T}$.

> [!question]- 3. Which modes appear in $e^{At}$ for $A$ with rows $(-2,\ 1)$ and $(0,\ -2)$, and for $A=\operatorname{diag}(-2,-2)$?
> First: $A+2I\ne 0$, so $\Psi=(\lambda+2)^2$: modes $e^{-2t}$ and $te^{-2t}$. Second: $A+2I=0$, $\Psi=\lambda+2$: only $e^{-2t}$.

> [!question]- 4. A $3\times 3$ matrix has $\Psi(\lambda)=\lambda^2(\lambda+3)$. Modes? Is the unforced motion bounded?
> Modes $1$, $t$, $e^{-3t}$. Not bounded for every $\mathbf{x}(0)$: the $2\times 2$ Jordan block of $0$ gives a term that grows like $t$.

> [!question]- 5. Discretize $\dot x=-x+u$ with a ZOH, $T=0.1$. Compare with Euler.
> $A_d=e^{-0.1}=0.904837$, $B_d=1-e^{-0.1}=0.095163$. Euler: $0.9$ and $0.1$.

> [!question]- 6. Double integrator $\ddot p=u$, $T=0.5$: find $A_d$, $B_d$.
> $A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$, $A^2=0$, so $A_d=I+AT=\begin{bmatrix}1&0.5\\0&1\end{bmatrix}$. $B_d=\int_0^T(\sigma,1)^{\mathsf T}d\sigma=(0.125,0.5)^{\mathsf T}$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L08 - Positive definiteness and SVD]]. Next: [[EE502 L10 - LTV state equation solution]]
- Used later in: [[EE502 L11 - Equivalence and realization]], [[EE502 L12 - Stability]], [[EE502 L13 - Controllability]], [[EE502 L14 - Observability]]
- Full step-by-step notes (PDF): [EE502_Lecture_09_LTI_Solution.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_09/EE502_Lecture_09_LTI_Solution.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_09/EE502_Lecture_09_LTI_Solution.pdf`
- Original slides (PDF, pp. 89-93): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L09 - LTI state equation solution - quiz]]

Slides not embedded: 89 (section title).
