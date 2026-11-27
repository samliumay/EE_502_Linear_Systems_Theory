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

> [!question]- Check (slide 131, definition): Find the two mistakes: "If $(A,B)$ is controllable, a bounded input brings the state to $\mathbf{x}_f$ and the state then stays at $\mathbf{x}_f$."
> Mistake 1: the definition puts no limit on the input. It only says that some input on $[0,t_f]$ exists. The input can be very large, mainly when $t_f$ is small.
> Mistake 2: the definition only asks for $\mathbf{x}(t_f)=\mathbf{x}_f$ at the one instant $t_f$. It says nothing about staying there. To stay, we would need $A\mathbf{x}_f+B\mathbf{u}=\mathbf{0}$ for some $\mathbf{u}$, which in general is not possible for every $\mathbf{x}_f$.
> Also note what the definition does say: every $\mathbf{x}_0$, every $\mathbf{x}_f$, some finite $t_f>0$.

> [!question]- Check (slide 131, example): Take $A$ with rows $(0,1)$ and $(1,0)$, and $B=(1,1)^{\mathsf T}$. Which combination of the states can the input not change? Write the system in the coordinates $z_1=(x_1+x_2)/2$, $z_2=(x_1-x_2)/2$, and find the transfer function for $y=x_1$.
> The equations are $\dot x_1=x_2+u$ and $\dot x_2=x_1+u$.
> Subtract: $\tfrac{d}{dt}(x_1-x_2)=x_2-x_1=-(x_1-x_2)$. The input has dropped out. So $x_1-x_2=e^{-t}(x_{01}-x_{02})$, whatever $u$ is. The pair is uncontrollable. Here the combination is not constant (as in Example 1), but it still moves by itself.
> In the new coordinates: $\dot z_1=z_1+u$ and $\dot z_2=-z_2$, so
> $$\bar A=\begin{bmatrix}1&0\\0&-1\end{bmatrix},\qquad \bar B=\begin{bmatrix}1\\0\end{bmatrix},\qquad \bar C=\begin{bmatrix}1&1\end{bmatrix}.$$
> The zero in the lower-left of $\bar A$ and the zero in $\bar B$ show the split: $z_1$ is the controllable part (mode $\lambda=1$), $z_2$ is the uncontrollable part (mode $\lambda=-1$).
> Transfer function: $(sI-A)^{-1}B=\dfrac{1}{s^2-1}\begin{bmatrix}s+1\\s+1\end{bmatrix}=\dfrac{1}{s-1}\begin{bmatrix}1\\1\end{bmatrix}$, so $G(s)=\dfrac{1}{s-1}$.
> Only the controllable mode $\lambda=1$ appears. The mode $\lambda=-1$ has cancelled. (Beyond the slides: this split into a controllable and an uncontrollable part is the controllability decomposition. It is treated fully in L14.)

> [!question]- Check (slide 132): For the double integrator of Example 2, take $\mathbf{x}_0=(0,0)^{\mathsf T}$, $\mathbf{x}_f=(1,0)^{\mathsf T}$, $t_f=1$. Find a $U(\tau)$ of the form $a\tau+b\tau^2$ and the input $u$. Why must $U$ become negative somewhere?
> Conditions from the slide: $U(1)=x_{f1}-x_{01}=1$ and $\int_0^1U\,d\tau=x_{f2}-x_{02}-t_fx_{01}=0$.
> $U(1)=a+b=1$. $\int_0^1U\,d\tau=\tfrac a2+\tfrac b3=0$, so $b=-\tfrac{3a}{2}$. Then $a-\tfrac{3a}{2}=1$ gives $a=-2$, $b=3$.
> $U(\tau)=3\tau^2-2\tau$ and $u(\tau)=\dot U=6\tau-2$.
> Check: $x_1(1)=U(1)=3-2=1$. $x_2(1)=\int_0^1(3\tau^2-2\tau)\,d\tau=1-1=0$.
> $U$ ends at $+1$ but its net area must be $0$, so it needs a negative part (a continuous $U\ge0$ with area $0$ would be $0$ everywhere). Here $x_1=U$: $x_1$ first goes negative so that $x_2$ comes back to $0$. The figure on the slide shows the same idea: positive and negative areas that add up to the required net area.

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

> [!info] The step 4 $\Rightarrow$ 2 in small steps (beyond the slides)
> The slide proves "2 fails $\Rightarrow$ 4 fails" by contradiction.
> - If $W_c(t)$ is singular for all $t$, there is $\mathbf{v}\ne\mathbf{0}$ with $\mathbf{v}^{\mathsf T}e^{A\tau}B=\mathbf{0}^{\mathsf T}$ for all $\tau$. The Laplace transform of $e^{A\tau}$ is $(sI-A)^{-1}$, so $\mathbf{v}^{\mathsf T}(sI-A)^{-1}B=\mathbf{0}^{\mathsf T}$. In words: the transfer function from $\mathbf{u}$ to the combination $\mathbf{v}^{\mathsf T}\mathbf{x}$ is zero.
> - Suppose 4 holds. Then $[A-sI\ \ B]$ has rank $n$ for every complex $s$ (Remark 3).
> - The fact that is not proved: full rank for every $s$ gives polynomial matrices $X(s)$, $Y(s)$ with $(sI-A)X(s)+BY(s)=I$. This is a matrix form of the Bezout identity $ax+by=1$ for two coprime polynomials. "Polynomial matrix" means every entry is a polynomial in $s$.
> - Multiply from the left by $\mathbf{v}^{\mathsf T}(sI-A)^{-1}$. The term with $B$ is zero, so $\mathbf{v}^{\mathsf T}X(s)=\mathbf{v}^{\mathsf T}(sI-A)^{-1}$.
> - Left side: polynomial entries. Right side: strictly proper entries (degree of numerator $<$ degree of denominator, so they go to $0$ as $s\to\infty$). A polynomial that goes to $0$ as $s\to\infty$ is the zero polynomial. So $\mathbf{v}^{\mathsf T}(sI-A)^{-1}=\mathbf{0}^{\mathsf T}$, and then $\mathbf{v}=\mathbf{0}$ because $(sI-A)^{-1}$ is invertible. Contradiction.

> [!question]- Check (slide 133, rank test): Take $A$ with rows $(1,1,0)$, $(0,1,0)$, $(0,0,1)$ and $B=(0,1,1)^{\mathsf T}$. Find the controllability matrix and its rank. Is the pair controllable?
> $n=3$, so $\mathcal{C}=[B\ \ AB\ \ A^2B]$.
> $AB=(0+1+0,\ 1,\ 1)^{\mathsf T}=(1,1,1)^{\mathsf T}$. $A^2B=A(AB)=(1+1,\ 1,\ 1)^{\mathsf T}=(2,1,1)^{\mathsf T}$.
> $$\mathcal{C}=\begin{bmatrix}0&1&2\\1&1&1\\1&1&1\end{bmatrix}.$$
> Rows 2 and 3 are equal, so $\det\mathcal{C}=0$. Rows 1 and 2 are independent, so the rank is $2<3$. The pair is not controllable.
> Reason: $\dot x_2=x_2+u$ and $\dot x_3=x_3+u$ are the same equation, so $x_2-x_3$ cannot be steered by $u$.

> [!question]- Check (slide 133, two inputs): Same $A$ as in the question above. Now $B$ has two columns $\mathbf{b}_1=(0,1,1)^{\mathsf T}$ and $\mathbf{b}_2=(0,0,1)^{\mathsf T}$. What size is $\mathcal{C}$? Is the pair controllable with $\mathbf{b}_2$ alone, and with both inputs?
> With $p=2$ inputs, $\mathcal{C}=[B\ \ AB\ \ A^2B]$ is $n\times np=3\times 6$.
> $\mathbf{b}_2$ alone: $A\mathbf{b}_2=(0,0,1)^{\mathsf T}=\mathbf{b}_2$, so all columns are multiples of $\mathbf{b}_2$. Rank $1$: not controllable.
> $\mathbf{b}_1$ alone: rank $2$ (question above): not controllable.
> Both: take the columns $\mathbf{b}_1$, $\mathbf{b}_2$, $A\mathbf{b}_1=(1,1,1)^{\mathsf T}$.
> $$\det\begin{bmatrix}0&0&1\\1&0&1\\1&1&1\end{bmatrix}=1\cdot(1\cdot1-0\cdot1)=1\ne0.$$
> Rank $3$: controllable. Each input alone fails, both together work.
> (Beyond the slides: we needed $\mathbf{b}_1,A\mathbf{b}_1$ from input 1 and only $\mathbf{b}_2$ from input 2. Chen calls these counts the controllability indices, here $\mu_1=2$, $\mu_2=1$, with $\mu_1+\mu_2=n$.)

> [!question]- Check (slide 134): In the second line of the slide, the factor $W_c(t_f)^{-1}[e^{At_f}\mathbf{x}_0-\mathbf{x}_f]$ moves out of the integral, and in the third line the integral becomes $W_c(t_f)$. Why is each step allowed?
> Step 1: $W_c(t_f)^{-1}[e^{At_f}\mathbf{x}_0-\mathbf{x}_f]$ is a constant vector. It does not depend on the integration variable $\tau$. It stands on the right of the integrand, so it can leave the integral on the right side (the order of matrix products is kept).
> Step 2: substitute $\sigma=t_f-\tau$. Then $d\sigma=-d\tau$, and $\tau=0,\ t_f$ become $\sigma=t_f,\ 0$:
> $$\int_0^{t_f}e^{A(t_f-\tau)}BB^{\mathsf T}e^{A^{\mathsf T}(t_f-\tau)}d\tau=\int_0^{t_f}e^{A\sigma}BB^{\mathsf T}e^{A^{\mathsf T}\sigma}d\sigma=W_c(t_f).$$
> Then $W_cW_c^{-1}=I$, and $e^{At_f}\mathbf{x}_0$ cancels. Only $\mathbf{x}_f$ is left.

> [!question]- Check (slide 135): Take $A$ with rows $(-1,0)$ and $(1,-2)$, and $B=(1,1)^{\mathsf T}$. Find a left eigenvector $\mathbf{v}^{\mathsf T}$ of $A$ with $\mathbf{v}^{\mathsf T}B=0$. Which mode is uncontrollable? Check with $\mathcal{C}$.
> Eigenvalues (triangular $A$): $\lambda=-1$ and $\lambda=-2$. A left eigenvector satisfies $\mathbf{v}^{\mathsf T}A=\lambda\mathbf{v}^{\mathsf T}$.
> $\lambda=-1$: $\mathbf{v}^{\mathsf T}=(1,0)$, because $(1,0)A=(-1,0)$. Then $\mathbf{v}^{\mathsf T}B=1\ne0$.
> $\lambda=-2$: $\mathbf{v}^{\mathsf T}=(1,-1)$, because $(1,-1)A=(-1-1,\ 0+2)=(-2,2)=-2\,(1,-1)$. Then $\mathbf{v}^{\mathsf T}B=1-1=0$.
> So $\mathbf{v}^{\mathsf T}[A+2I\ \ B]=\mathbf{0}^{\mathsf T}$: condition 4 fails at $\lambda=-2$. The mode $\lambda=-2$ is uncontrollable.
> Check as on the slide: $AB=(-1,\ 1-2)^{\mathsf T}=(-1,-1)^{\mathsf T}=-B$, so $\mathcal{C}$ has rows $(1,-1)$ and $(1,-1)$, rank $1<2$. Also $\mathbf{v}^{\mathsf T}\mathcal{C}=(0,0)$.
> Meaning: $\tfrac{d}{dt}(x_1-x_2)=-2(x_1-x_2)$, with no $u$ in it.

> [!question]- Check (slide 136): Apply the PBH test to the 3-state pair of "Check (slide 133, rank test)": $A$ with rows $(1,1,0)$, $(0,1,0)$, $(0,0,1)$, $B=(0,1,1)^{\mathsf T}$. Then say why a single input can never control this $A$.
> $A$ is triangular with the only eigenvalue $\lambda=1$ (three times). One test is enough:
> $$[A-I\ \ B]=\begin{bmatrix}0&1&0&0\\0&0&0&1\\0&0&0&1\end{bmatrix}.$$
> Rows 2 and 3 are equal. Rank $2<3$: the test fails, the mode $\lambda=1$ is (partly) uncontrollable.
> The left vector is $\mathbf{v}^{\mathsf T}=(0,1,-1)$: $\mathbf{v}^{\mathsf T}(A-I)=\mathbf{0}^{\mathsf T}$ and $\mathbf{v}^{\mathsf T}B=1-1=0$.
> Any single input: $A-I$ has rank $1$ (only one nonzero entry). One extra column $\mathbf{b}$ raises the rank by at most $1$, so $\operatorname{rank}[A-I\ \ \mathbf{b}]\le2<3$ for every $\mathbf{b}$. This $A$ needs at least two inputs (see the two-input question of slide 133).

> [!question]- Check (slide 137, Cayley-Hamilton): Take $A$ with rows $(1,2)$ and $(3,4)$, and $B=(1,0)^{\mathsf T}$. Write $A^2B$ as a combination of $B$ and $AB$. What does this say about adding the column $A^2B$ to $\mathcal{C}$?
> Characteristic polynomial: $s^2-(1+4)s+(1\cdot4-2\cdot3)=s^2-5s-2$. Cayley-Hamilton: $A^2-5A-2I=0$, so $A^2=5A+2I$.
> Multiply by $B$: $A^2B=5AB+2B$.
> Numbers: $AB=(1,3)^{\mathsf T}$, so $5AB+2B=(5+2,\ 15+0)^{\mathsf T}=(7,15)^{\mathsf T}$. Direct: $A^2B=A(1,3)^{\mathsf T}=(1+6,\ 3+12)^{\mathsf T}=(7,15)^{\mathsf T}$. Same.
> So $A^2B$ (and then every $A^kB$, $k\ge2$) lies in the span of $B$ and $AB$. Extra columns never raise the rank. This is why $\mathcal{C}$ stops at $A^{n-1}B$, and why $\mathbf{v}^{\mathsf T}\mathcal{C}=\mathbf{0}^{\mathsf T}$ gives $\mathbf{v}^{\mathsf T}A^kB=\mathbf{0}^{\mathsf T}$ for all $k$.

> [!question]- Check (slide 137, change of coordinates): For the pair above ($A$ with rows $(1,2)$, $(3,4)$, $B=(1,0)^{\mathsf T}$) use $\bar{\mathbf{x}}=P\mathbf{x}$ with $P$ with rows $(1,1)$, $(0,1)$. Compute $\bar{\mathcal{C}}$ and compare it with $\mathcal{C}$. Does controllability change?
> $\bar A=PAP^{-1}$, $\bar B=PB$. $P^{-1}$ has rows $(1,-1)$, $(0,1)$.
> $PA$ has rows $(4,6)$, $(3,4)$. $\bar A=PAP^{-1}$ has rows $(4,\ -4+6)=(4,2)$ and $(3,\ -3+4)=(3,1)$. $\bar B=(1,0)^{\mathsf T}$.
> $\bar A\bar B=(4,3)^{\mathsf T}$, so
> $$\bar{\mathcal{C}}=\begin{bmatrix}1&4\\0&3\end{bmatrix},\qquad \mathcal{C}=\begin{bmatrix}1&1\\0&3\end{bmatrix},\qquad P\,\mathcal{C}=\begin{bmatrix}1&1+3\\0&3\end{bmatrix}=\bar{\mathcal{C}}.$$
> In general $\bar A^k\bar B=PA^kP^{-1}PB=PA^kB$, so $\bar{\mathcal{C}}=P\mathcal{C}$. $P$ is nonsingular, so the rank is the same (here $\det=3$ for both). Controllability does not depend on the choice of state coordinates. (Beyond the slides: this invariance is not stated on slide 137. It is Chen's Theorem 6.2.)

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

> [!question]- Check (slide 138, Gramian): Take $A$ with rows $(-1,0)$ and $(1,-2)$, and $B=(1,1)^{\mathsf T}$ (the pair of slide 135's question). Compute $W_c(t)$. Is it nonsingular for some $t$? Which direction $\mathbf{v}$ does it miss?
> $AB=-B$, so $B$ is an eigenvector of $A$ for $\lambda=-1$ and $e^{A\tau}B=e^{-\tau}B=e^{-\tau}(1,1)^{\mathsf T}$.
> $$W_c(t)=\int_0^te^{-2\tau}\begin{bmatrix}1&1\\1&1\end{bmatrix}d\tau=\frac{1-e^{-2t}}{2}\begin{bmatrix}1&1\\1&1\end{bmatrix}.$$
> $\det W_c(t)=0$ for every $t$: singular for all $t$, so the pair is not controllable (condition 2 fails).
> With $\mathbf{v}=(1,-1)^{\mathsf T}$: $W_c(t)\mathbf{v}=\mathbf{0}$ and $\mathbf{v}^{\mathsf T}e^{A\tau}B=e^{-\tau}(1-1)=0$. This is the same $\mathbf{v}$ as the left eigenvector of the PBH test. The input only pushes along $(1,1)^{\mathsf T}$.

> [!question]- Check (slide 138, input): For the double integrator of Example 3, find the input that brings $\mathbf{x}_0=(1,0)^{\mathsf T}$ to $\mathbf{x}_f=(0,0)^{\mathsf T}$ in time $t=2$. Find its energy $\int_0^2u^2d\tau$.
> $W_c(2)=\begin{bmatrix}2&2\\2&8/3\end{bmatrix}$, $\det=\tfrac{16}{3}-4=\tfrac43$, so $W_c(2)^{-1}=\tfrac34\begin{bmatrix}8/3&-2\\-2&2\end{bmatrix}=\begin{bmatrix}2&-3/2\\-3/2&3/2\end{bmatrix}$.
> $\boldsymbol{\xi}=e^{2A}\mathbf{x}_0-\mathbf{x}_f=\begin{bmatrix}1&0\\2&1\end{bmatrix}\begin{bmatrix}1\\0\end{bmatrix}=\begin{bmatrix}1\\2\end{bmatrix}$.
> $W_c(2)^{-1}\boldsymbol{\xi}=(2-3,\ -\tfrac32+3)^{\mathsf T}=(-1,\ \tfrac32)^{\mathsf T}$.
> $B^{\mathsf T}e^{A^{\mathsf T}(2-\tau)}=\begin{bmatrix}1&2-\tau\end{bmatrix}$, so
> $$u(\tau)=-\Bigl[-1+\tfrac32(2-\tau)\Bigr]=\tfrac32\tau-2.$$
> Check: $x_1(2)=1+\int_0^2(\tfrac32\tau-2)d\tau=1+3-4=0$. $x_1(s)=1-2s+\tfrac34s^2$, so $x_2(2)=\int_0^2x_1\,ds=2-4+2=0$.
> Energy: $\int_0^2(\tfrac32\tau-2)^2d\tau=\int_0^2(\tfrac94\tau^2-6\tau+4)d\tau=6-12+8=2$. Same as $\boldsymbol{\xi}^{\mathsf T}W_c^{-1}\boldsymbol{\xi}=(1)(-1)+(2)(\tfrac32)=2$. No other input that does this transfer in time $2$ has less energy.

> [!question]- Check (slide 139): Keep the $A$ of the double pendulum but let the input enter the second equation only: $B=(0,1,0,0)^{\mathsf T}$. Predict whether the pair is controllable before computing. Then compute $\mathcal{C}$.
> Prediction: rows 3 and 4 of $A$ have zeros in columns 1 and 2. So $\dot x_3=x_4$, $\dot x_4=-cx_3$ do not depend on $x_1$, $x_2$ or $u$. In this linear model the lower pendulum would swing by itself. Not controllable.
> Computation: $AB$ is column 2 of $A$: $(1,0,0,0)^{\mathsf T}$. $A^2B=A(1,0,0,0)^{\mathsf T}=(0,-a,0,0)^{\mathsf T}$. $A^3B=A(0,-a,0,0)^{\mathsf T}=(-a,0,0,0)^{\mathsf T}$.
> $$\mathcal{C}=\begin{bmatrix}0&1&0&-a\\1&0&-a&0\\0&0&0&0\\0&0&0&0\end{bmatrix},\qquad\operatorname{rank}\mathcal{C}=2<4.$$
> On the slide the input enters at $x_4$ and reaches $x_1,x_2$ through the coupling $b$ (entry $(2,3)$ of $A$). There is no coupling in the other direction, so the place where the input enters matters.

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

> [!question]- Check (slide 154): Scalar system $\dot x=b(t)u$ with $b(t)=1$ for $t<1$ and $b(t)=0$ for $t\ge1$. Is it controllable at $t_0=0$? At $t_0=2$? What does this show about the LTV definition?
> At $t_0=0$: on $[0,1)$ we have $\dot x=u$. Take $t_f=\tfrac12$ and the constant input $u=2(x_f-x_0)$. Then $x(\tfrac12)=x_0+\tfrac12\cdot2(x_f-x_0)=x_f$. Controllable at $t_0=0$.
> At $t_0=2$: for all $t\ge2$, $\dot x=0$, so $x(t)=x_0$ for every input. No $x_f\ne x_0$ is reached. Uncontrollable at $t_0=2$.
> The answer depends on the initial time. This is why the slide says "controllable at $t_0$". For an LTI pair the answer is the same for every start time, so $t_0$ is not named.

> [!question]- Check (slide 155): Take $A(t)=0$ and $B(t)=(\cos t,\ \sin t)^{\mathsf T}$. Compute $W_c(0,t)$ and its determinant. Is the pair controllable at $t_0=0$? Compare with the constant $B=(1,0)^{\mathsf T}$.
> $A=0$ gives $\Phi(t,\tau)=I$, so the integrand is $B(\tau)B(\tau)^{\mathsf T}$:
> $$W_c(0,t)=\int_0^t\begin{bmatrix}\cos^2\tau&\cos\tau\sin\tau\\\cos\tau\sin\tau&\sin^2\tau\end{bmatrix}d\tau=\begin{bmatrix}\tfrac t2+\tfrac{\sin2t}{4}&\tfrac{\sin^2t}{2}\\\tfrac{\sin^2t}{2}&\tfrac t2-\tfrac{\sin2t}{4}\end{bmatrix}.$$
> $\det W_c=\tfrac{t^2}{4}-\tfrac{\sin^22t}{16}-\tfrac{\sin^4t}{4}$. With $\sin2t=2\sin t\cos t$: $\tfrac{\sin^22t}{16}=\tfrac{\sin^2t\cos^2t}{4}$, so
> $$\det W_c(0,t)=\frac{t^2-\sin^2t\,(\cos^2t+\sin^2t)}{4}=\frac{t^2-\sin^2t}{4}>0\quad\text{for }t>0,$$
> because $\lvert\sin t\rvert<t$. Nonsingular: controllable at $t_0=0$ (Theorem 4).
> Constant $B=(1,0)^{\mathsf T}$: $W_c$ has rows $(t,0)$, $(0,0)$, singular, uncontrollable ($\dot x_2=0$). At each instant both systems push in one direction only. With $B(t)$ the direction turns in time, and over an interval it covers the whole plane.

> [!question]- Check (slide 156): Find the mistake: "$W_c(t_0,t)$ is singular at $t=t_0+1$, so the pair is uncontrollable at $t_0$." Use $\dot x=b(t)u$ with $b=0$ on $[0,1]$ and $b=1$ for $t>1$, $t_0=0$.
> The proof on the slide needs $W_c(t_0,t)$ singular for all $t>t_0$. Singular at one $t$ is not enough, because Theorem 4 asks for nonsingular at some $t$.
> Example: $\Phi=1$, so $W_c(0,t)=\int_0^tb(\tau)^2d\tau$. $W_c(0,1)=0$ (singular). But $W_c(0,2)=\int_1^2 1\,d\tau=1\ne0$. So the system is controllable at $t_0=0$: wait until $t>1$ and then steer.
> A longer interval can only help: $W_c(t_0,t)$ singular at some $t$ says nothing about larger $t$.

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

> [!warning] Slide slip (p. 159)
> Example 2 ends with "controllable at any $t_0>0$". The condition $t_0>0$ is not needed: $t^2+1\ne0$ for all real $t$, so the pair is controllable at every $t_0$.

> [!question]- Check (slide 157): Take $A(t)$ with rows $(0,1)$ and $(0,t)$, and $B(t)=(0,t)^{\mathsf T}$. Compute $M_0$, $M_1$ and $\det[M_0\ M_1]$. At which $t_0$ does Theorem 5 give controllability?
> $n=2$, so we need $M_0$ and $M_1$.
> $M_0=B=(0,t)^{\mathsf T}$.
> $A M_0=(1\cdot t,\ t\cdot t)^{\mathsf T}=(t,t^2)^{\mathsf T}$ and $\dot M_0=(0,1)^{\mathsf T}$.
> $M_1=-AM_0+\dot M_0=(-t,\ 1-t^2)^{\mathsf T}$.
> $$\det\begin{bmatrix}0&-t\\t&1-t^2\end{bmatrix}=0\cdot(1-t^2)-(-t)(t)=t^2.$$
> The rank is $2$ at every $t_1\ne0$. The theorem needs only one $t_1>t_0$, and such a $t_1\ne0$ always exists. So the pair is controllable at every $t_0$, also at $t_0<0$.
> Without the term $\dot M_0$ we would get $M_1=(-t,-t^2)^{\mathsf T}$ and $\det=0\cdot(-t^2)-(-t)(t)=t^2$ again here, but in general the result is wrong (see Example 2 of slide 159, where $\dot M_1\ne0$ changes $M_2$).

> [!question]- Check (slide 158): Apply the rank test of Theorem 5 to Example 1 ($A=\operatorname{diag}(1,2)$, $B(t)=(e^t,e^{2t})^{\mathsf T}$). What does the test say? Then use $z_1=e^{-t}x_1$, $z_2=e^{-2t}x_2$ to see directly why the pair is uncontrollable.
> $M_0=(e^t,e^{2t})^{\mathsf T}$. $AM_0=(e^t,2e^{2t})^{\mathsf T}$ and $\dot M_0=(e^t,2e^{2t})^{\mathsf T}$, so $M_1=-AM_0+\dot M_0=(0,0)^{\mathsf T}$.
> $\operatorname{rank}[M_0\ M_1]=1<2$ at every $t_1$. The test fails. Theorem 5 is sufficient only, so this alone proves nothing. The Gramian (Theorem 4) decides: singular for all $t$, uncontrollable.
> Direct view: $\dot z_1=-e^{-t}x_1+e^{-t}(x_1+e^tu)=u$ and $\dot z_2=-2e^{-2t}x_2+e^{-2t}(2x_2+e^{2t}u)=u$.
> Both $z_1$ and $z_2$ obey $\dot z=u$, so $z_1-z_2=e^{-t}x_1-e^{-2t}x_2$ is constant for every input. This is Example 1 of slide 131 again, hidden by a time-varying change of variables.

> [!question]- Check (slide 159): In Example 2 replace $B$ by $(1,0,0)^{\mathsf T}$. Compute $M_0$, $M_1$, $M_2$ and the rank. What does Theorem 5 say, and is the pair controllable?
> $M_0=(1,0,0)^{\mathsf T}$. $AM_0$ is column 1 of $A$: $(t,0,0)^{\mathsf T}$. $\dot M_0=\mathbf{0}$. So $M_1=(-t,0,0)^{\mathsf T}$.
> $AM_1=(-t^2,0,0)^{\mathsf T}$ and $\dot M_1=(-1,0,0)^{\mathsf T}$. So $M_2=-AM_1+\dot M_1=(t^2-1,\ 0,\ 0)^{\mathsf T}$.
> All three columns are multiples of $(1,0,0)^{\mathsf T}$: rank $1<3$ for every $t_1$.
> Theorem 5 gives no conclusion (sufficient only). We need another argument: $A(t)$ is upper triangular, so $\dot x_2=-tx_2+tx_3$ and $\dot x_3=tx_3$ contain no $x_1$ and no $u$. The input never reaches $x_2$, $x_3$. The pair is uncontrollable at every $t_0$.

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
> [!question]- 1. Is $A$ with rows $(0,1)$, $(0,0)$ and $B=(0,1)^{\mathsf T}$ controllable?
> $AB=(1,0)^{\mathsf T}$, $\mathcal{C}=\begin{bmatrix}0&1\\1&0\end{bmatrix}$, $\det=-1$: controllable. PBH at $\lambda=0$: $\begin{bmatrix}0&1&0\\0&0&1\end{bmatrix}$ has rank 2.

> [!question]- 2. $A=\operatorname{diag}(1,2)$, $B=(1,0)^{\mathsf T}$. Name the uncontrollable mode.
> $\mathcal{C}=\begin{bmatrix}1&1\\0&0\end{bmatrix}$, rank 1. PBH at $\lambda=2$: $\begin{bmatrix}-1&0&1\\0&0&0\end{bmatrix}$, rank 1. Mode $\lambda=2$ is uncontrollable: $\dot x_2=2x_2$, whatever $u$ is.

> [!question]- 3. Is $A$ with rows $(0,1)$, $(-2,-3)$ and $\mathbf{b}=(0,1)^{\mathsf T}$ controllable?
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
- Quiz: [[EE502 L13 - Controllability - quiz]]

Slides not embedded: 130, 153 (section titles).
