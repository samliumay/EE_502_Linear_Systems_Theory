---
course: EE 502 Linear System Theory
lecture: 13
title: Controllability
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 130-139, 153-159)
full_notes: lecture_notes/lecture_13/EE502_Lecture_13_Controllability.pdf
---
# EE 502 · Lecture 13 · Controllability

> [!summary] In short
> - $(A,B)$ is controllable if an input can drive any state to any other state in finite time.
> - Four equivalent LTI tests: definition, Gramian $W_c(t)$ nonsingular, $\operatorname{rank}[B\ AB\ \cdots\ A^{n-1}B]=n$, and the PBH test $\operatorname{rank}[A-\lambda I\ \ B]=n$ at every eigenvalue.
> - The Gramian gives the steering input explicitly, and it is the minimum-energy one. Short drive times need large inputs.
> - LTV: controllability is "at $t_0$". The Gramian $W_c(t_0,t)$ test is necessary and sufficient. The rank test with $M_{k+1}=-AM_k+\dot M_k$ is sufficient only.

Slide numbers below are pages of the 220-page ABO file.

## 1. Definition and two examples (slides 131-132)
![[ee502_eee501alllecturenotesabo_p131.jpg]]
![[ee502_eee501alllecturenotesabo_p132.jpg]]

**Notes.** $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, or the pair $(A,B)$, is **controllable** if for every $\mathbf{x}_0$ and every $\mathbf{x}_f$ there are a time $t_f>0$ and an input on $[0,t_f]$ with $\mathbf{x}(t_f)=\mathbf{x}_f$. Nothing limits the size of the input. It is a property of $(A,B)$ only: separate from stability ($A$) and observability ($A,C$).

> [!example] Example 1 (uncontrollable)
> $A=\begin{bmatrix}1&1\\1&1\end{bmatrix}$, $B=\begin{bmatrix}2\\2\end{bmatrix}$. Both states obey the same equation, so $x_1-x_2$ never changes. Starting with $x_{01}=x_{02}$, a target with $x_{f1}\ne x_{f2}$ is never reached.

> [!example] Example 2 (controllable, double integrator)
> $A=\begin{bmatrix}0&0\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$: $\dot x_1=u$, $\dot x_2=x_1$. With $U(t)=\int_0^tu$: $x_1=U+x_{01}$, $x_2=tx_{01}+\int_0^tU+x_{02}$. Choose any $U$ with $U(t_f)=x_{f1}-x_{01}$ and $\int_0^{t_f}U=x_{f2}-x_{02}-t_fx_{01}$. Then $u=\dot U$.

## 2. Main theorem of LTI controllability (slides 133-137)
![[ee502_eee501alllecturenotesabo_p133.jpg]]
![[ee502_eee501alllecturenotesabo_p134.jpg]]
![[ee502_eee501alllecturenotesabo_p135.jpg]]
![[ee502_eee501alllecturenotesabo_p136.jpg]]
![[ee502_eee501alllecturenotesabo_p137.jpg]]

**Notes.** **Theorem 1.** Equivalent:
1. $(A,B)$ is controllable.
2. The controllability Gramian $W_c(t)=\int_0^te^{A\tau}BB^{\mathsf T}e^{A^{\mathsf T}\tau}\,d\tau$ is nonsingular for some $t>0$.
3. The controllability matrix $\mathcal{C}=\begin{bmatrix}B&AB&\cdots&A^{n-1}B\end{bmatrix}$ has rank $n$.
4. $\operatorname{rank}\begin{bmatrix}A-\lambda I&B\end{bmatrix}=n$ for every eigenvalue $\lambda$ of $A$ (PBH test).

**Steering input** (proof of 2 $\Rightarrow$ 1):
$$\mathbf{u}(\tau)=-B^{\mathsf T}e^{A^{\mathsf T}(t_f-\tau)}\,W_c(t_f)^{-1}\bigl[e^{At_f}\mathbf{x}_0-\mathbf{x}_f\bigr],\qquad\tau\in[0,t_f]. \tag{1}$$
Substituting into the solution formula gives $\mathbf{x}(t_f)=e^{At_f}\mathbf{x}_0-W_cW_c^{-1}[e^{At_f}\mathbf{x}_0-\mathbf{x}_f]=\mathbf{x}_f$.

The other steps all use one idea: if a test fails, there is a $\mathbf{v}\ne\mathbf{0}$ with $\mathbf{v}^{\mathsf T}e^{A\tau}B=\mathbf{0}^{\mathsf T}$ for all $\tau$, a direction the input never touches.
- 1 $\Rightarrow$ 2: $\mathbf{v}^{\mathsf T}W_c\mathbf{v}=\int_0^t\lVert\mathbf{v}^{\mathsf T}e^{A\tau}B\rVert^2d\tau=0$. Driving $\mathbf{0}$ to $\mathbf{v}$ would give $\mathbf{v}^{\mathsf T}\mathbf{v}=0$.
- 2 $\Rightarrow$ 3: $\mathbf{v}^{\mathsf T}\mathcal{C}=\mathbf{0}^{\mathsf T}$ gives $\mathbf{v}^{\mathsf T}A^kB=\mathbf{0}^{\mathsf T}$ for all $k$ (Cayley-Hamilton), so $\mathbf{v}^{\mathsf T}e^{At}B=\mathbf{0}^{\mathsf T}$.
- 3 $\Rightarrow$ 4: $\mathbf{v}^{\mathsf T}A=\lambda\mathbf{v}^{\mathsf T}$ and $\mathbf{v}^{\mathsf T}B=\mathbf{0}^{\mathsf T}$ give $\mathbf{v}^{\mathsf T}A^kB=\lambda^k\mathbf{v}^{\mathsf T}B=\mathbf{0}^{\mathsf T}$.
- 4 $\Rightarrow$ 2 uses a polynomial-matrix fact that the slides do not prove.

Remarks (slide 137): $W_c(t)$ is symmetric positive semi-definite, so nonsingular means positive definite. Ranks do not change under transposition (used for duality). PBH holds automatically at any $\lambda$ that is not an eigenvalue.

How to use them: $\mathcal{C}$ for a quick yes or no, PBH to name the bad mode, the Gramian to build the input.

> [!warning] Watch out
> PBH must hold at **every** eigenvalue. In Example 1, $\lambda=2$ passes and $\lambda=0$ fails. A rank drop at $\lambda$ gives a left vector $\mathbf{v}^{\mathsf T}$, and $\mathbf{v}^{\mathsf T}\mathbf{x}$ is the combination the input cannot change.

## 3. Gramian example and the double pendulum (slides 138-139)
![[ee502_eee501alllecturenotesabo_p138.jpg]]
![[ee502_eee501alllecturenotesabo_p139.jpg]]

**Notes.**

> [!example] Example 3: double integrator
> $e^{At}=\begin{bmatrix}1&0\\t&1\end{bmatrix}$, $e^{A\tau}B=(1,\tau)^{\mathsf T}$, so
> $$W_c(t)=\int_0^t\begin{bmatrix}1&\tau\\\tau&\tau^2\end{bmatrix}d\tau=\begin{bmatrix}t&t^2/2\\t^2/2&t^3/3\end{bmatrix},\qquad\det W_c=\frac{t^4}{12}.$$
> Input from (1), final time $t$:
> $$u(\tau)=-\begin{bmatrix}\dfrac4t-\dfrac{6}{t^2}(t-\tau)&\dfrac{12}{t^3}(t-\tau)-\dfrac{6}{t^2}\end{bmatrix}\left(\begin{bmatrix}1&0\\t&1\end{bmatrix}\mathbf{x}_0-\mathbf{x}_f\right).$$
> It grows without bound as $t\to 0$: a fast drive is costly.

**Minimum energy (our notes).** With $\boldsymbol{\xi}=e^{At_f}\mathbf{x}_0-\mathbf{x}_f$, the input (1) is the unique one of least energy, and
$$E_{\min}=\int_0^{t_f}\lVert\mathbf{u}(\tau)\rVert^2d\tau=\boldsymbol{\xi}^{\mathsf T}W_c(t_f)^{-1}\boldsymbol{\xi}.$$
Double integrator, $\mathbf{0}$ to $(1,1)$: $E_{\min}=4(t^2-3t+3)/t^3$, about $12/t^3$ for small $t$.

**Double pendulum (slide 139).** States $x_1=\theta_1$, $x_2=\dot\theta_1$, $x_3=\theta_2$, $x_4=\dot\theta_2$, with $a=\tfrac{(m_1+m_2)g}{m_1l_1}$, $b=\tfrac{m_2g}{m_1l_1}$, $c=\tfrac{g}{l_2}$, $d=\tfrac{1}{m_2l_2}$:
$$A=\begin{bmatrix}0&1&0&0\\-a&0&b&0\\0&0&0&1\\0&0&-c&0\end{bmatrix},\ B=\begin{bmatrix}0\\0\\0\\d\end{bmatrix},\qquad\mathcal{C}=\begin{bmatrix}0&0&0&bd\\0&0&bd&0\\0&d&0&-cd\\d&0&-cd&0\end{bmatrix}.$$
$\det\mathcal{C}=b^2d^4\ne 0$: controllable. One force on the lower mass steers all four states.

> [!warning] Slide misprint (p. 139)
> The $(3,4)$ entry of $A^3$ is printed as $1$. It is $-c$ (row 3 of $A^3$ is row 4 of $A^2$). The matrix $\mathcal{C}$ on the slide is correct.

## 4. LTV controllability and the Gramian test (slides 154-156)
![[ee502_eee501alllecturenotesabo_p154.jpg]]
![[ee502_eee501alllecturenotesabo_p155.jpg]]
![[ee502_eee501alllecturenotesabo_p156.jpg]]

**Notes.** $(A(t),B(t))$ is **controllable at $t_0$** if every $\mathbf{x}(t_0)=\mathbf{x}_0$ can be driven to every $\mathbf{x}_f$ at some later time $t_f$. Unlike LTI, the definition depends on the initial time.

**Theorem 4.** Controllable at $t_0$ iff
$$W_c(t_0,t)=\int_{t_0}^{t}\Phi(t,\tau)B(\tau)B(\tau)^{\mathsf T}\Phi(t,\tau)^{\mathsf T}\,d\tau$$
is nonsingular for some $t>t_0$. Steering input:
$$\mathbf{u}(\tau)=-B(\tau)^{\mathsf T}\Phi(t_f,\tau)^{\mathsf T}W_c(t_0,t_f)^{-1}\bigl[\Phi(t_f,t_0)\mathbf{x}_0-\mathbf{x}_f\bigr],\qquad\tau\in[t_0,t_f].$$
The proof copies the LTI one with $\Phi(t,\tau)$ in place of $e^{A(t-\tau)}$ (see [[EE502 L10 - LTV state equation solution]]).

> [!warning] Slide slips (p. 155)
> The input formula is printed with $B(t)^{\mathsf T}$ and without the brackets around $\Phi(t_f,t_0)\mathbf{x}_0-\mathbf{x}_f$. Read it as above, with $B(\tau)^{\mathsf T}$. "For some $t_f>0$" should be $t_f>t_0$.

## 5. A sufficient rank condition for LTV (slides 157-159)
![[ee502_eee501alllecturenotesabo_p157.jpg]]
![[ee502_eee501alllecturenotesabo_p158.jpg]]
![[ee502_eee501alllecturenotesabo_p159.jpg]]

**Notes.** **Theorem 5.** Let $A(t)$, $B(t)$ be $n-1$ times differentiable and define
$$M_0(t)=B(t),\qquad M_{k+1}(t)=-A(t)M_k(t)+\frac{d}{dt}M_k(t).$$
If $\operatorname{rank}\begin{bmatrix}M_0(t_1)&M_1(t_1)&\cdots&M_{n-1}(t_1)\end{bmatrix}=n$ for some $t_1>t_0$, then $(A(t),B(t))$ is controllable at $t_0$. Reason: $\tfrac{\partial^k}{\partial\tau^k}\bigl[\Phi(t,\tau)B(\tau)\bigr]=\Phi(t,\tau)M_k(\tau)$.

> [!example] Example 1 (p. 158): uncontrollable
> $A=\operatorname{diag}(1,2)$, $B(t)=(e^t,e^{2t})^{\mathsf T}$. $\Phi(t,\tau)B(\tau)=(e^{t},e^{2t})^{\mathsf T}$ does not depend on $\tau$, so
> $W_c(t_0,t)=(t-t_0)\begin{bmatrix}e^{2t}&e^{3t}\\e^{3t}&e^{4t}\end{bmatrix}$, rank 1 for all $t$. Uncontrollable at any $t_0$.

> [!example] Example 2 (p. 159): controllable
> $A(t)=\begin{bmatrix}t&-1&0\\0&-t&t\\0&0&t\end{bmatrix}$, $B=\begin{bmatrix}0\\1\\1\end{bmatrix}$. $M_0=(0,1,1)^{\mathsf T}$, $M_1=(1,0,-t)^{\mathsf T}$, $M_2=(-t,t^2,t^2-1)^{\mathsf T}$.
> $\det\begin{bmatrix}M_0&M_1&M_2\end{bmatrix}=t^2+1\ne 0$: controllable at any $t_0$.

> [!warning] Watch out
> - Sufficient only: rank $<n$ proves nothing. Then use the Gramian.
> - Do not forget the derivative term $\dot M_k$.
> - The slide says "$M_k$ for $k=0,1,\dots,n-2$" for the recursion index; the test uses $M_0,\dots,M_{n-1}$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Controllable | any $\mathbf{x}_0$ to any $\mathbf{x}_f$ in finite time |
| Gramian | $W_c(t)=\int_0^te^{A\tau}BB^{\mathsf T}e^{A^{\mathsf T}\tau}d\tau$, positive semi-definite |
| Controllability matrix | $\mathcal{C}=[B\ AB\ \cdots\ A^{n-1}B]$, $n\times np$, rank $n$ |
| PBH test | $\operatorname{rank}[A-\lambda I\ \ B]=n$ at every eigenvalue |
| Steering input | $\mathbf{u}(\tau)=-B^{\mathsf T}e^{A^{\mathsf T}(t_f-\tau)}W_c(t_f)^{-1}[e^{At_f}\mathbf{x}_0-\mathbf{x}_f]$ |
| Minimum energy | $\boldsymbol{\xi}^{\mathsf T}W_c(t_f)^{-1}\boldsymbol{\xi}$, $\boldsymbol{\xi}=e^{At_f}\mathbf{x}_0-\mathbf{x}_f$ |
| LTV Gramian | $W_c(t_0,t)=\int_{t_0}^{t}\Phi(t,\tau)BB^{\mathsf T}\Phi(t,\tau)^{\mathsf T}d\tau$ |
| LTV rank test | $M_0=B$, $M_{k+1}=-AM_k+\dot M_k$; rank $n$ is sufficient |

## Check yourself
> [!question]- 1. Is $A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$ controllable?
> $AB=(1,0)^{\mathsf T}$, $\mathcal{C}=\begin{bmatrix}0&1\\1&0\end{bmatrix}$, $\det=-1$: controllable. PBH at $\lambda=0$: $\begin{bmatrix}0&1&0\\0&0&1\end{bmatrix}$ has rank 2.

> [!question]- 2. $A=\operatorname{diag}(1,2)$, $B=(1,0)^{\mathsf T}$. Name the uncontrollable mode.
> $\mathcal{C}=\begin{bmatrix}1&1\\0&0\end{bmatrix}$, rank 1. PBH at $\lambda=2$: $\begin{bmatrix}-1&0&1\\0&0&0\end{bmatrix}$, rank 1. Mode $\lambda=2$ is uncontrollable: $\dot x_2=2x_2$, whatever $u$ is.

> [!question]- 3. Is $A=\begin{bmatrix}0&1\\-2&-3\end{bmatrix}$, $\mathbf{b}=\begin{bmatrix}0\\1\end{bmatrix}$ controllable?
> $A\mathbf{b}=(1,-3)^{\mathsf T}$, $\det\mathcal{C}=-1\ne 0$: controllable. PBH at $-1$ and $-2$ both give rank 2.

> [!question]- 4. For $\dot x=-x+u$: $W_c(t)$, the input and the minimum energy from $0$ to $1$ in time $t$.
> $W_c(t)=\tfrac{1-e^{-2t}}{2}$. $u(\tau)=\tfrac{2e^{-(t-\tau)}}{1-e^{-2t}}$. $E_{\min}=\tfrac{2}{1-e^{-2t}}$: tends to $2$ as $t\to\infty$ and to $\infty$ as $t\to 0$.

> [!question]- 5. $A(t)=0$, $B(t)=(1,t)^{\mathsf T}$. Controllable at $t_0$? Find $W_c(0,t)$.
> $M_0=(1,t)^{\mathsf T}$, $M_1=\dot M_0=(0,1)^{\mathsf T}$, $\det[M_0\ M_1]=1$: controllable at every $t_0$. $\Phi=I$, so $W_c(0,t)=\begin{bmatrix}t&t^2/2\\t^2/2&t^3/3\end{bmatrix}$, the double-integrator Gramian.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L12 - Stability]]. Next: [[EE502 L14 - Observability]] (the dual results, Kalman decomposition)
- Used later in: [[EE502 L15 - State feedback (extra)]] (eigenvalue assignment needs controllability)
- Full step-by-step notes (PDF): [EE502_Lecture_13_Controllability.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_13/EE502_Lecture_13_Controllability.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_13/EE502_Lecture_13_Controllability.pdf`
- Original slides (PDF, pp. 130-139 and 153-159): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: 130, 153 (section titles).
