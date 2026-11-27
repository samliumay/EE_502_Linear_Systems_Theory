---
course: EE 502 Linear System Theory
lecture: 14
title: Observability
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 140-152, 160-162)
full_notes: lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf
---
# EE 502 · Lecture 14 · Observability, duality, Kalman decomposition

> [!summary] In short
> - $(C,A)$ is observable if the input and output on some $[0,t_1]$ fix the initial state $\mathbf{x}_0$ uniquely.
> - Tests: Gramian $W_o(t)$ nonsingular, $\operatorname{rank}[C;CA;\dots;CA^{n-1}]=n$, PBH with a right eigenvector.
> - Duality: $(A,B)$ controllable iff $(B^{\mathsf T},A^{\mathsf T})$ observable. Every controllability test transposes into an observability test.
> - A change of state keeps both properties. A good choice of $P$ displays the controllable and observable parts (Kalman decomposition). Only the controllable and observable part reaches the transfer matrix.
> - Minimal realization $\iff$ controllable and observable.

Slide numbers below are pages of the 220-page ABO file.

## 1. Definition and two examples (slides 141-142)
![[ee502_eee501alllecturenotesabo_p141.jpg]]
![[ee502_eee501alllecturenotesabo_p142.jpg]]

**Notes.** $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$, or the pair $(C,A)$, is **observable** if for any unknown $\mathbf{x}_0=\mathbf{x}(0)$, knowing $\mathbf{u}(t)$ and $\mathbf{y}(t)$ on $[0,t_1]$ for some $t_1>0$ determines $\mathbf{x}_0$ uniquely.

> [!example] Example 1 (unobservable)
> $A=\begin{bmatrix}0&0\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&0\end{bmatrix}$, $D=1$: $y=x_1+u$. $x_2$ never influences $y$, so $x_2(0)$ cannot be found.

> [!example] Example 2 (observable)
> Same $A,B,D$ with $C=\begin{bmatrix}1&1\end{bmatrix}$. With $U(t)=\int_0^tu$, the readings at $0$ and $t_1$ give
> $$\begin{bmatrix}y(0)-u(0)\\ y(t_1)-U(t_1)-\int_0^{t_1}U-u(t_1)\end{bmatrix}=\begin{bmatrix}1&1\\t_1+1&1\end{bmatrix}\begin{bmatrix}x_{01}\\x_{02}\end{bmatrix}.$$
> The matrix has determinant $-t_1\ne 0$, so $\mathbf{x}_0$ is unique.

> [!warning] Watch out
> The slide writes $y(0)=x_{01}+x_{02}$. With $D=1$ it is $y(0)=x_{01}+x_{02}+u(0)$, so subtract $u(0)$ as above. Also: "not measured" does not mean "unobservable". Only the tests decide.

> [!question]- Check (slide 141): The definition asks only for the initial state $\mathbf{x}_0$. Why is that enough to know $\mathbf{x}(t)$ on the whole interval? And why must the input be known, not only the output?
> The state at any time is $\mathbf{x}(t)=e^{At}\mathbf{x}_0+\int_0^te^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$. Once $\mathbf{x}_0$ is known and $\mathbf{u}$ is known, every term on the right is known, so $\mathbf{x}(t)$ is known for all $t$.
> The input must be known because the output mixes two effects: the response to $\mathbf{x}_0$ and the response to $\mathbf{u}$. Only after the input part is subtracted does the rest, $Ce^{At}\mathbf{x}_0$, carry information about $\mathbf{x}_0$ alone.
> The definition does not say that each state variable is measured, and it does not say that one reading of $\mathbf{y}$ at one time is enough. It needs the output over an interval $[0,t_1]$.

> [!question]- Check (slide 142): Take the same $A$ with rows $(0,0)$ and $(1,0)$, but $C=(2,1)$ and $u=0$. The measurements are $y(0)=3$ and $y(1)=5$. Find $\mathbf{x}_0$.
> With $u=0$: $x_1(t)=x_{01}$ and $x_2(t)=t\,x_{01}+x_{02}$.
> $$y(t)=2x_1(t)+x_2(t)=(t+2)x_{01}+x_{02}.$$
> At $t=0$: $2x_{01}+x_{02}=3$. At $t=1$: $3x_{01}+x_{02}=5$.
> Subtract the first from the second: $x_{01}=2$. Then $x_{02}=3-2\cdot 2=-1$.
> So $\mathbf{x}_0=(2,-1)^{\mathsf T}$. The coefficient matrix with rows $(2,1)$ and $(3,1)$ has determinant $2-3=-1\ne 0$, so the solution is unique.

## 2. The observability Gramian (slides 143-144)
![[ee502_eee501alllecturenotesabo_p143.jpg]]
![[ee502_eee501alllecturenotesabo_p144.jpg]]

**Notes.** Move the known input terms to the left:
$$\hat{\mathbf{y}}(t):=\mathbf{y}(t)-\int_0^tCe^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau-D\mathbf{u}(t)=Ce^{At}\mathbf{x}_0 .$$
Only the zero-input response matters for observability.

**Theorem 2.** $(C,A)$ is observable iff $W_o(t_1)=\int_0^{t_1}e^{A^{\mathsf T}\tau}C^{\mathsf T}Ce^{A\tau}\,d\tau$ is nonsingular for some $t_1>0$.

- If: multiply $\hat{\mathbf{y}}(\tau)=Ce^{A\tau}\mathbf{x}_0$ on the left by $e^{A^{\mathsf T}\tau}C^{\mathsf T}$ and integrate. Then
$$\mathbf{x}_0=W_o(t_1)^{-1}\int_0^{t_1}e^{A^{\mathsf T}\tau}C^{\mathsf T}\hat{\mathbf{y}}(\tau)\,d\tau .$$
- Only if: if $W_o\mathbf{v}=\mathbf{0}$ with $\mathbf{v}\ne\mathbf{0}$, then $\int_0^{t_1}\lVert Ce^{A\tau}\mathbf{v}\rVert^2d\tau=0$, so $Ce^{A\tau}\mathbf{v}=\mathbf{0}$ for all $\tau$. The initial states $\mathbf{v}$ and $\mathbf{0}$ give the same output.

> [!question]- Check (slide 143): $A$ has rows $(0,1)$ and $(0,0)$, $C=(1,0)$, $t_1=1$. The input-free output is $\hat y(t)=2+3t$. Compute $W_o(1)$ and reconstruct $\mathbf{x}_0$ with the Gramian formula.
> $A^2=0$, so $e^{A\tau}=I+A\tau$ has rows $(1,\tau)$ and $(0,1)$. Then $Ce^{A\tau}=\begin{bmatrix}1&\tau\end{bmatrix}$.
> $$W_o(1)=\int_0^1\begin{bmatrix}1\\\tau\end{bmatrix}\begin{bmatrix}1&\tau\end{bmatrix}d\tau=\int_0^1\begin{bmatrix}1&\tau\\\tau&\tau^2\end{bmatrix}d\tau=\begin{bmatrix}1&\tfrac12\\\tfrac12&\tfrac13\end{bmatrix}.$$
> $\det W_o(1)=\tfrac13-\tfrac14=\tfrac1{12}\ne 0$, so
> $$W_o(1)^{-1}=12\begin{bmatrix}\tfrac13&-\tfrac12\\-\tfrac12&1\end{bmatrix}=\begin{bmatrix}4&-6\\-6&12\end{bmatrix}.$$
> $$\mathbf{z}=\int_0^1\begin{bmatrix}1\\\tau\end{bmatrix}(2+3\tau)\,d\tau=\begin{bmatrix}2+\tfrac32\\1+1\end{bmatrix}=\begin{bmatrix}\tfrac72\\2\end{bmatrix}.$$
> $$\mathbf{x}_0=W_o(1)^{-1}\mathbf{z}=\begin{bmatrix}4\cdot\tfrac72-6\cdot 2\\-6\cdot\tfrac72+12\cdot 2\end{bmatrix}=\begin{bmatrix}2\\3\end{bmatrix}.$$
> Test: $Ce^{At}\mathbf{x}_0=2+3t$. Correct.

> [!question]- Check (slide 144): $A$ has rows $(1,1)$ and $(0,1)$, $C=(0,1)$. Compute $W_o(t_1)$, find a vector $\mathbf{v}\ne\mathbf{0}$ with $W_o(t_1)\mathbf{v}=\mathbf{0}$, and say which initial states cannot be told apart.
> $e^{A\tau}=e^{\tau}\begin{bmatrix}1&\tau\\0&1\end{bmatrix}$, so $Ce^{A\tau}=\begin{bmatrix}0&e^{\tau}\end{bmatrix}$.
> $$W_o(t_1)=\int_0^{t_1}\begin{bmatrix}0\\e^{\tau}\end{bmatrix}\begin{bmatrix}0&e^{\tau}\end{bmatrix}d\tau=\begin{bmatrix}0&0\\0&\tfrac12(e^{2t_1}-1)\end{bmatrix}.$$
> It is singular for every $t_1$. The vector $\mathbf{v}=(1,0)^{\mathsf T}$ gives $W_o(t_1)\mathbf{v}=\mathbf{0}$, and indeed $Ce^{A\tau}\mathbf{v}=0$ for all $\tau$.
> So $\mathbf{x}_0=(1,0)^{\mathsf T}$ and $\mathbf{x}_0=\mathbf{0}$ give the same output (zero, with zero input). More generally $\mathbf{x}_0$ and $\mathbf{x}_0+\alpha\mathbf{v}$ give the same output for every $\alpha$: the output shows $x_{02}$ but never $x_{01}$.

## 3. Duality and the main theorem (slides 145-146)
![[ee502_eee501alllecturenotesabo_p145.jpg]]
![[ee502_eee501alllecturenotesabo_p146.jpg]]

**Notes.** The **dual** of $(A,B,C,D)$ is $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T},D^{\mathsf T})$. Its controllability Gramian is the original $W_o$, and its observability Gramian is the original $W_c$. So $(A,B)$ is controllable iff $(B^{\mathsf T},A^{\mathsf T})$ is observable, and $(C,A)$ is observable iff $(A^{\mathsf T},C^{\mathsf T})$ is controllable.

**Corollary.** Equivalent:
1. $(C,A)$ is observable.
2. $W_o(t)$ is nonsingular for some $t>0$.
3. The observability matrix has rank $n$:
$$\mathcal{O}=\begin{bmatrix}C\\CA\\ \vdots\\CA^{n-1}\end{bmatrix}.$$
4. $\operatorname{rank}\begin{bmatrix}A-\lambda I\\C\end{bmatrix}=n$ for every eigenvalue $\lambda$ of $A$ (PBH).

> [!warning] Watch out
> $\mathcal{C}$ is a block row, $\mathcal{O}$ is a block column. For controllability the bad vector is a left eigenvector ($\mathbf{v}^{\mathsf T}B=\mathbf{0}^{\mathsf T}$). For observability it is a right eigenvector: $A\mathbf{w}=\lambda\mathbf{w}$ and $C\mathbf{w}=\mathbf{0}$.

> [!info] Why the rank test works, and the unobservable subspace (beyond the slides)
> The slide gets the rank test from duality and gives no direct reason. Here is the direct one.
> An initial state $\mathbf{v}$ is invisible when $Ce^{At}\mathbf{v}=\mathbf{0}$ for all $t$. Differentiate $k$ times and set $t=0$: $CA^k\mathbf{v}=\mathbf{0}$ for $k=0,1,2,\dots$ By the Cayley-Hamilton theorem every $A^k$ with $k\ge n$ is a combination of $I,A,\dots,A^{n-1}$, so only $k=0,\dots,n-1$ matter. These $n$ conditions together are $\mathcal{O}\mathbf{v}=\mathbf{0}$. The converse also holds: if $CA^k\mathbf{v}=\mathbf{0}$ for all $k$, then the series $e^{At}=\sum_k A^kt^k/k!$ gives $Ce^{At}\mathbf{v}=\mathbf{0}$ for all $t$.
> So the set of invisible initial states is the null space of $\mathcal{O}$. It is called the **unobservable subspace**. Its dimension is $n-\operatorname{rank}\mathcal{O}$. The pair is observable exactly when this null space contains only $\mathbf{0}$, which means $\operatorname{rank}\mathcal{O}=n$.
> The slide writes $\mathcal{O}$ and the PBH matrix with transposes. Written out, they are the block columns $[C;CA;\dots;CA^{n-1}]$ and $[A-\lambda I;\ C]$ used in this note.

> [!question]- Check (slide 145): $A$ has rows $(1,2)$ and $(0,3)$, $B=(1,1)^{\mathsf T}$. Check controllability of $(A,B)$. Then use duality to state a result about observability, and verify it directly.
> $AB=(1\cdot1+2\cdot1,\ 3\cdot 1)^{\mathsf T}=(3,3)^{\mathsf T}$. The controllability matrix $[B\ \ AB]$ has rows $(1,3)$ and $(1,3)$. Its rank is 1, so $(A,B)$ is not controllable.
> Duality: $(A,B)$ is controllable iff $(B^{\mathsf T},A^{\mathsf T})$ is observable. So the pair with output matrix $B^{\mathsf T}=(1,1)$ and system matrix $A^{\mathsf T}$, rows $(1,0)$ and $(2,3)$, is not observable.
> Direct check: $B^{\mathsf T}A^{\mathsf T}=(1+2,\ 0+3)=(3,3)$. The observability matrix has rows $(1,1)$ and $(3,3)$, rank 1. It is the transpose of $[B\ \ AB]$, as duality says.

> [!question]- Check (slide 146, rank test): $A$ has rows $(0,1,0)$, $(0,0,1)$, $(-6,-11,-6)$ and $C=(8,6,1)$. Find $\operatorname{rank}\mathcal{O}$, the unobservable subspace, and an initial state that cannot be distinguished from zero.
> $CA=(1\cdot(-6),\ 8-11,\ 6-6)=(-6,-3,0)$.
> $CA^2=(CA)A=(0,\ -6,\ -3)$.
> Stack $C$, $CA$, $CA^2$ as rows. This is the block column form; the slide writes the same matrix as $[C^{\mathsf T}\ \ A^{\mathsf T}C^{\mathsf T}\ \ (A^{\mathsf T})^2C^{\mathsf T}]^{\mathsf T}$.
> $$\mathcal{O}=\begin{bmatrix}8&6&1\\-6&-3&0\\0&-6&-3\end{bmatrix}.$$
> Row 1 $=-\tfrac43\,$row 2 $-\tfrac13\,$row 3, and rows 2 and 3 are independent. So $\operatorname{rank}\mathcal{O}=2<3$: not observable.
> Null space: row 2 gives $v_2=-2v_1$, row 3 gives $v_3=-2v_2=4v_1$. With $v_1=1$: $\mathbf{v}=(1,-2,4)^{\mathsf T}$. Row 1: $8-12+4=0$. Correct.
> The unobservable subspace is the line spanned by $(1,-2,4)^{\mathsf T}$. With zero input, $\mathbf{x}_0=(1,-2,4)^{\mathsf T}$ gives $y(t)=0$ for all $t$, the same as $\mathbf{x}_0=\mathbf{0}$.

> [!question]- Check (slide 146, PBH test): For the same pair, the eigenvalues of $A$ are $-1,-2,-3$. Use the PBH test to find which mode is unobservable.
> $A$ is a companion matrix, so the right eigenvector for $\lambda$ is $\mathbf{w}=(1,\lambda,\lambda^2)^{\mathsf T}$. Then $C\mathbf{w}=8+6\lambda+\lambda^2=(\lambda+2)(\lambda+4)$.
> $\lambda=-1$: $C\mathbf{w}=3\ne 0$. $\lambda=-3$: $C\mathbf{w}=-1\ne 0$. $\lambda=-2$: $C\mathbf{w}=8-12+4=0$.
> At $\lambda=-2$ the vector $\mathbf{w}=(1,-2,4)^{\mathsf T}$ satisfies $(A+2I)\mathbf{w}=\mathbf{0}$ and $C\mathbf{w}=0$. So $[A+2I;\ C]\mathbf{w}=\mathbf{0}$ and the rank is $2<3$. (Here $[A-\lambda I;\ C]$ is $A-\lambda I$ with the row $C$ below it. The slide writes the same matrix as $[A^{\mathsf T}-\lambda I\ \ C^{\mathsf T}]^{\mathsf T}$.) At $\lambda=-1$ and $\lambda=-3$ the rank is 3.
> The mode $-2$ ($e^{-2t}$) is unobservable. Its eigenvector is the same vector that spans the null space of $\mathcal{O}$.

## 4. Invariance, controllable and uncontrollable parts (slides 147-150)
![[ee502_eee501alllecturenotesabo_p147.jpg]]
![[ee502_eee501alllecturenotesabo_p148.jpg]]
![[ee502_eee501alllecturenotesabo_p149.jpg]]
![[ee502_eee501alllecturenotesabo_p150.jpg]]

**Notes.** Under $\hat{\mathbf{x}}=P\mathbf{x}$: $\hat{\mathcal{C}}=P\mathcal{C}$ and $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$. Ranks do not change, so controllability and observability are invariant under equivalence.

**Theorem 1.** Let $\operatorname{rank}\mathcal{C}=n_1<n$. Take $n_1$ independent columns $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$ of $\mathcal{C}$, complete them to a basis, and set $P^{-1}=[\mathbf{q}_1\ \cdots\ \mathbf{q}_n]$. Then
$$\hat A=\begin{bmatrix}\hat A_c&\hat A_{12}\\0&\hat A_{\bar c}\end{bmatrix},\quad\hat B=\begin{bmatrix}\hat B_c\\0\end{bmatrix},\quad\hat C=\begin{bmatrix}\hat C_c&\hat C_{\bar c}\end{bmatrix},$$
with $(\hat A_c,\hat B_c)$ controllable and $C(sI-A)^{-1}B+D=\hat C_c(sI-\hat A_c)^{-1}\hat B_c+D$. The eigenvalues of $\hat A_{\bar c}$ are the uncontrollable modes. They cancel out of the transfer matrix.

Recipe: column $j$ of $\hat A$ holds the coordinates of $A\mathbf{q}_j$ in the basis; $\hat B$ holds the coordinates of the columns of $B$; $\hat C=CP^{-1}$.

> [!example] Slide example (p. 150)
> $A=\begin{bmatrix}1&1&0\\0&1&0\\0&1&1\end{bmatrix}$, $B=\begin{bmatrix}0&1\\1&0\\0&1\end{bmatrix}$, $C=\begin{bmatrix}1&1&1\end{bmatrix}$. $\operatorname{rank}\mathcal{C}=2$. Take $\mathbf{q}_1,\mathbf{q}_2$ = columns of $B$, $\mathbf{q}_3=(1,0,0)^{\mathsf T}$:
> $$\hat A_c=\begin{bmatrix}1&0\\1&1\end{bmatrix},\ \hat B_c=I_2,\ \hat C_c=\begin{bmatrix}1&2\end{bmatrix},\ \hat A_{\bar c}=1,\ \hat C_{\bar c}=1 .$$
> $$\hat C_c(sI-\hat A_c)^{-1}\hat B_c=\begin{bmatrix}\dfrac{1}{s-1}+\dfrac{2}{(s-1)^2}&\dfrac{2}{s-1}\end{bmatrix}=C(sI-A)^{-1}B .$$

> [!warning] Slide slip (p. 149)
> The proof states that $\hat{\mathcal{C}}$ has rank $n$. Since $\hat{\mathcal{C}}=P\mathcal{C}$, the rank is $n_1$.

> [!question]- Check (slide 147): Show that $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$. Why does this not change the rank? Does it change the unobservable subspace?
> Block $k$ of $\hat{\mathcal{O}}$ is $\hat C\hat A^k=CP^{-1}(PAP^{-1})^k=CP^{-1}PA^kP^{-1}=CA^kP^{-1}$. Every block is the old block times $P^{-1}$ on the right, so $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$.
> $P^{-1}$ is nonsingular, and multiplying by a nonsingular matrix keeps the rank. So $\operatorname{rank}\hat{\mathcal{O}}=\operatorname{rank}\mathcal{O}$.
> The subspace itself moves with the coordinates: $\hat{\mathcal{O}}\hat{\mathbf{v}}=\mathbf{0}$ iff $\mathcal{O}P^{-1}\hat{\mathbf{v}}=\mathbf{0}$, so $\hat{\mathbf{v}}=P\mathbf{v}$. It is the same set of states written in the new coordinates, and its dimension is the same.

> [!question]- Check (slide 148): $A$ has rows $(0,1)$ and $(-2,-3)$, $B=(1,-1)^{\mathsf T}$, $C=(1,0)$. Apply Theorem 1 with $\mathbf{q}_2=(0,1)^{\mathsf T}$. Find $\hat A$, $\hat B$, $\hat C$, the uncontrollable mode and the transfer function.
> $AB=(-1,\ -2+3)^{\mathsf T}=(-1,1)^{\mathsf T}=-B$. So $[B\ \ AB]$ has rank $n_1=1$. Take $\mathbf{q}_1=B$.
> Column 1 of $\hat A$: $A\mathbf{q}_1=-\mathbf{q}_1$, coordinates $(-1,0)$.
> Column 2 of $\hat A$: $A\mathbf{q}_2=(1,-3)^{\mathsf T}=1\cdot\mathbf{q}_1-2\cdot\mathbf{q}_2$, coordinates $(1,-2)$.
> $$\hat A=\begin{bmatrix}-1&1\\0&-2\end{bmatrix},\quad\hat B=\begin{bmatrix}1\\0\end{bmatrix},\quad\hat C=CP^{-1}=\begin{bmatrix}C\mathbf{q}_1&C\mathbf{q}_2\end{bmatrix}=\begin{bmatrix}1&0\end{bmatrix}.$$
> So $\hat A_c=-1$, $\hat B_c=1$, $\hat C_c=1$, $\hat A_{\bar c}=-2$. The uncontrollable mode is $-2$.
> Transfer function: $\hat C_c(s-\hat A_c)^{-1}\hat B_c=\dfrac{1}{s+1}$. The full system has two states but the transfer function has degree 1.

> [!question]- Check (slide 149): In the proof, why is the lower left block $\hat A_{21}$ zero? Say which property of the columns $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$ is used.
> Column $j$ of $\hat A$ holds the coordinates of $A\mathbf{q}_j$ in the basis $\mathbf{q}_1,\dots,\mathbf{q}_n$.
> For $j\le n_1$, $\mathbf{q}_j$ is in the column span of $\mathcal{C}$. This span is invariant under $A$: $A\mathcal{C}=[AB\ \cdots\ A^nB]$, and $A^nB$ is a combination of $B,\dots,A^{n-1}B$ by Cayley-Hamilton. So $A\mathbf{q}_j$ is again in the span of $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$.
> Its coordinates along $\mathbf{q}_{n_1+1},\dots,\mathbf{q}_n$ are then zero. These coordinates are exactly the entries of $\hat A_{21}$.
> The same argument with the columns of $B$ (they are columns of $\mathcal{C}$) gives the zero block in $\hat B$.

> [!question]- Check (slide 150): In the slide example, replace $\mathbf{q}_3=(1,0,0)^{\mathsf T}$ by $\mathbf{q}_3=(1,1,0)^{\mathsf T}$. Which of $\hat A_c$, $\hat B_c$, $\hat C_c$, $\hat A_{12}$, $\hat A_{\bar c}$, $\hat C_{\bar c}$ change? Does the transfer matrix change?
> $\hat A_c$, $\hat B_c$, $\hat C_c$ use only $\mathbf{q}_1,\mathbf{q}_2$, so they do not change.
> Third column of $\hat A$: $A\mathbf{q}_3=(1+1,\ 1,\ 1)^{\mathsf T}=(2,1,1)^{\mathsf T}$. Solve $a\mathbf{q}_1+b\mathbf{q}_2+c\mathbf{q}_3=(2,1,1)^{\mathsf T}$ with $\mathbf{q}_1=(0,1,0)^{\mathsf T}$, $\mathbf{q}_2=(1,0,1)^{\mathsf T}$: row 3 gives $b=1$, row 1 gives $b+c=2$ so $c=1$, row 2 gives $a+c=1$ so $a=0$.
> So $\hat A_{12}=(0,1)^{\mathsf T}$ (before it was $(0,0)^{\mathsf T}$) and $\hat A_{\bar c}=1$ (unchanged; it must stay an eigenvalue of $A$).
> $\hat C_{\bar c}=C\mathbf{q}_3=1+1+0=2$ (before it was 1).
> The transfer matrix does not change. It uses only $(\hat A_c,\hat B_c,\hat C_c)$, and it is the same for every equivalent representation.

## 5. Observable parts and the Kalman decomposition (slides 151-152)
![[ee502_eee501alllecturenotesabo_p151.jpg]]
![[ee502_eee501alllecturenotesabo_p152.jpg]]

**Notes.** **Theorem 2.** Let $\operatorname{rank}\mathcal{O}=n_2<n$. Build $P$ from $n_2$ independent **rows** of $\mathcal{O}$, completed to a nonsingular matrix. Then
$$\hat A=\begin{bmatrix}\hat A_o&0\\\hat A_{21}&\hat A_{\bar o}\end{bmatrix},\quad\hat B=\begin{bmatrix}\hat B_o\\\hat B_{\bar o}\end{bmatrix},\quad\hat C=\begin{bmatrix}\hat C_o&0\end{bmatrix},$$
with $(\hat C_o,\hat A_o)$ observable and the same transfer matrix from $(\hat A_o,\hat B_o,\hat C_o,D)$.

**Theorem 3 (Kalman canonical decomposition).** Some $P$ gives
$$\hat A=\begin{bmatrix}\hat A_{co}&0&\hat A_{13}&0\\\hat A_{21}&\hat A_{c\bar o}&\hat A_{23}&\hat A_{24}\\0&0&\hat A_{\bar co}&0\\0&0&\hat A_{43}&\hat A_{\bar c\bar o}\end{bmatrix},\quad\hat B=\begin{bmatrix}\hat B_{co}\\\hat B_{c\bar o}\\0\\0\end{bmatrix},\quad\hat C=\begin{bmatrix}\hat C_{co}&0&\hat C_{\bar co}&0\end{bmatrix},$$
with $(\hat A_{co},\hat B_{co})$ controllable, $(\hat C_{co},\hat A_{co})$ observable, and
$$C(sI-A)^{-1}B+D=\hat C_{co}(sI-\hat A_{co})^{-1}\hat B_{co}+D .$$
Subscripts: $c$ controllable, $\bar c$ uncontrollable, $o$ observable, $\bar o$ unobservable.

**Minimal realization (our notes).** A realization has the smallest possible state dimension exactly when it is controllable and observable. Otherwise $(\hat A_{co},\hat B_{co},\hat C_{co},D)$ is a smaller one.

> [!warning] Slide slips (p. 151)
> The completing rows are printed as $\mathbf{p}_{n_1+1},\dots,\mathbf{p}_n$ and the output matrix as $[\hat C_c\ \ 0]$. Intended: $\mathbf{p}_{n_2+1},\dots,\mathbf{p}_n$ and $[\hat C_o\ \ 0]$.

> [!info] Reading the four Kalman blocks (beyond the slides)
> The new state is split as $\hat{\mathbf{x}}=(\hat{\mathbf{x}}_{co},\hat{\mathbf{x}}_{c\bar o},\hat{\mathbf{x}}_{\bar co},\hat{\mathbf{x}}_{\bar c\bar o})$.
> - $\hat{\mathbf{x}}_{co}$: the input moves it and the output shows it. This is the only path from $\mathbf{u}$ to $\mathbf{y}$.
> - $\hat{\mathbf{x}}_{c\bar o}$: the input moves it, but $\hat C$ has a zero block there and no observable part reads it.
> - $\hat{\mathbf{x}}_{\bar co}$: the output shows it, but $\hat B$ has a zero block there and no controllable part drives it. It only shows the effect of its own initial state.
> - $\hat{\mathbf{x}}_{\bar c\bar o}$: neither driven nor seen.
>
> The zero blocks in rows 3 and 4 of $\hat A$ say that the controllable states do not feed the uncontrollable ones. The zero blocks in columns 2 and 4 of rows 1 and 3 say that the unobservable states do not feed the observable ones.
> **Minimal realization.** A realization of a transfer matrix $\hat G(s)$ is minimal if no realization of $\hat G(s)$ has fewer states. Its number of states is the degree of $\hat G(s)$. For a scalar $\hat g(s)=N(s)/D(s)$ with no common factor, this is $\deg D$. If a realization has more states than that, at least one mode is uncontrollable or unobservable, and it shows up as a pole-zero cancellation in $C(sI-A)^{-1}B$.

> [!question]- Check (slide 151): $A$ has rows $(0,1)$ and $(-2,-3)$, $B=(0,1)^{\mathsf T}$, $C=(1,1)$. Apply Theorem 2 with $\mathbf{p}_2=(0,1)$. Find $\hat A$, $\hat B$, $\hat C$, the unobservable mode and the transfer function.
> $CA=(-2,\ 1-3)=(-2,-2)=-2C$. So $\mathcal{O}$ has rank $n_2=1$. Take $\mathbf{p}_1=C=(1,1)$.
> $P$ has rows $(1,1)$ and $(0,1)$. $P^{-1}$ has rows $(1,-1)$ and $(0,1)$.
> $PA$ has rows $(-2,-2)$ and $(-2,-3)$. Then
> $$\hat A=PAP^{-1}=\begin{bmatrix}-2&0\\-2&-1\end{bmatrix},\quad\hat B=PB=\begin{bmatrix}1\\1\end{bmatrix},\quad\hat C=CP^{-1}=\begin{bmatrix}1&0\end{bmatrix}.$$
> So $\hat A_o=-2$, $\hat B_o=1$, $\hat C_o=1$, $\hat A_{\bar o}=-1$. The unobservable mode is $-1$. PBH agrees: $\mathbf{w}=(1,-1)^{\mathsf T}$ has $A\mathbf{w}=-\mathbf{w}$ and $C\mathbf{w}=0$.
> Transfer function: $\hat C_o(s-\hat A_o)^{-1}\hat B_o=\dfrac{1}{s+2}$. Direct: $C(sI-A)^{-1}B=\dfrac{s+1}{(s+1)(s+2)}$. The factor $s+1$ cancels. This is the pole-zero cancellation of the unobservable mode.

> [!question]- Check (slide 151, rows): Theorem 1 builds $P^{-1}$ from columns of $\mathcal{C}$. Theorem 2 builds $P$ from rows of $\mathcal{O}$. Why rows, and why $P$ instead of $P^{-1}$?
> Theorem 2 is Theorem 1 applied to the dual system $(A^{\mathsf T},C^{\mathsf T})$. The controllability matrix of the dual is $\mathcal{O}^{\mathsf T}$, so its columns are the transposed rows of $\mathcal{O}$.
> Theorem 1 for the dual gives a matrix $Q^{-1}$ whose columns are those vectors. Transposing back turns $\hat A_{\text{dual}}=QA^{\mathsf T}Q^{-1}$ into $(Q^{-1})^{\mathsf T}A\,Q^{\mathsf T}$. So for the original system $P=(Q^{-1})^{\mathsf T}$, a matrix whose rows are rows of $\mathcal{O}$.
> The transpose also flips the block shape: upper triangular $\hat A$ with $\hat B=[\hat B_c;0]$ becomes lower triangular $\hat A$ with $\hat C=[\hat C_o\ \ 0]$.

> [!question]- Check (slide 152): $A=\operatorname{diag}(-1,-2,-3,-4)$, $B=(1,1,0,0)^{\mathsf T}$, $C=(1,0,1,0)$. Put each mode into one of the four Kalman parts. Give the transfer function and the dimension of a minimal realization.
> $A$ is diagonal with distinct eigenvalues. Mode $i$ is controllable iff $b_i\ne 0$ and observable iff $c_i\ne 0$.
> - $-1$: $b_1=1$, $c_1=1$. Controllable and observable ($co$).
> - $-2$: $b_2=1$, $c_2=0$. Controllable, not observable ($c\bar o$).
> - $-3$: $b_3=0$, $c_3=1$. Not controllable, observable ($\bar co$).
> - $-4$: $b_4=0$, $c_4=0$. Neither ($\bar c\bar o$).
>
> The state order already matches Theorem 3, so $P=I$. Here $\operatorname{rank}\mathcal{C}=2$ and $\operatorname{rank}\mathcal{O}=2$.
> $$C(sI-A)^{-1}B=\sum_{i=1}^{4}\frac{c_ib_i}{s-\lambda_i}=\frac{1}{s+1}.$$
> Only the $co$ part $(\hat A_{co},\hat B_{co},\hat C_{co})=(-1,1,1)$ is left. A minimal realization has 1 state, although the system has 4.

> [!question]- Check (slide 152, minimality, beyond the slides): For a realization with 3 states, $C(sI-A)^{-1}B$ computed without cancelling is $\dfrac{s+3}{(s+1)(s+2)(s+3)}$, so the eigenvalues of $A$ are $-1,-2,-3$. What can you conclude without computing $\mathcal{C}$ or $\mathcal{O}$? What can you not conclude?
> The factor $s+3$ cancels: $\hat g(s)=\dfrac{1}{(s+1)(s+2)}$. Its degree is 2.
> A minimal realization has 2 states. This one has 3, so it is not minimal. By Theorem 3 it is not controllable or not observable (or both). The $co$ part has dimension 2.
> The lost mode is $-3$: it is an eigenvalue of $A$ but not a pole of $\hat g$.
> You cannot conclude which property fails. The transfer function does not tell whether the mode $-3$ is uncontrollable, unobservable, or both. For that, compute $\mathcal{C}$ and $\mathcal{O}$ or use the PBH tests at $\lambda=-3$.

## 6. Observability of LTV systems (slides 161-162)
![[ee502_eee501alllecturenotesabo_p161.jpg]]
![[ee502_eee501alllecturenotesabo_p162.jpg]]

**Notes.** $(C(t),A(t))$ is **observable at $t_0$** if $\mathbf{u}$ and $\mathbf{y}$ on $[t_0,t_1]$, for some $t_1>t_0$, determine $\mathbf{x}(t_0)$ uniquely. The dual system is
$$\frac{d}{dt}\hat{\mathbf{x}}=-A^{\mathsf T}(t)\hat{\mathbf{x}}+C^{\mathsf T}(t)\mathbf{u},\qquad\mathbf{y}=B^{\mathsf T}(t)\hat{\mathbf{x}}+D^{\mathsf T}(t)\mathbf{u},$$
with state transition matrix $\hat\Phi(t,t_0)=\Phi(t_0,t)^{\mathsf T}$ (slide exercise; see the adjoint system in [[EE502 L10 - LTV state equation solution]]).

**Theorem 6.**
1. Observable at $t_0$ iff $W_o(t_0,t)=\int_{t_0}^{t}\Phi(\tau,t)^{\mathsf T}C(\tau)^{\mathsf T}C(\tau)\Phi(\tau,t)\,d\tau$ is nonsingular for some $t>t_0$.
2. Sufficient rank test: $N_0(t)=C(t)$, $N_{k+1}(t)=N_k(t)A(t)+\tfrac{d}{dt}N_k(t)$. If $\operatorname{rank}[N_0(t_1);N_1(t_1);\dots;N_{n-1}(t_1)]=n$ for some $t_1>t_0$, the pair is observable at $t_0$.

Slide exercise: Chen's Gramian uses $\Phi(\tau,t_0)$ instead of $\Phi(\tau,t)$. Since $\Phi(\tau,t)=\Phi(\tau,t_0)\Phi(t_0,t)$, the two differ by the nonsingular factor $\Phi(t_0,t)$ on both sides, so one is nonsingular exactly when the other is.

> [!warning] Watch out
> The LTV dual uses $-A^{\mathsf T}(t)$, not $A^{\mathsf T}(t)$. The rank test is sufficient only, and the recursion includes the derivative $\dot N_k$. The slide lists "$k=0,\dots,n-2$" for the recursion index; the test uses $N_0,\dots,N_{n-1}$.

> [!question]- Check (slide 161): For constant $A$ and $C$, the dual on this slide has $-A^{\mathsf T}$, but the LTI dual of Section 3 has $A^{\mathsf T}$. Do the two give different observability tests? Also check the exercise formula for the scalar case $A(t)=2t$.
> No. The controllability matrix of $(-A^{\mathsf T},C^{\mathsf T})$ is $[C^{\mathsf T}\ \ -A^{\mathsf T}C^{\mathsf T}\ \ (A^{\mathsf T})^2C^{\mathsf T}\ \cdots]$. Compared with the one of $(A^{\mathsf T},C^{\mathsf T})$, only the signs of some blocks change. The rank is the same, so both duals give the same test, $\operatorname{rank}\mathcal{O}=n$.
> The minus sign is needed in the time-varying case to make the transition matrices match: $\hat\Phi(t,t_0)=\Phi(t_0,t)^{\mathsf T}$.
> Scalar check: $\dot x=2t\,x$ gives $\Phi(t,t_0)=e^{t^2-t_0^2}$. The dual $\dot{\hat x}=-2t\,\hat x$ gives $\hat\Phi(t,t_0)=e^{-(t^2-t_0^2)}=e^{t_0^2-t^2}=\Phi(t_0,t)$. For a scalar the transpose does nothing, so the formula holds.

> [!question]- Check (slide 162): $A(t)$ has rows $(0,t)$ and $(0,0)$, $C=(1,0)$. Apply the rank test. At $t_1=0$ the rank is 1: does that show the pair is unobservable?
> $N_0=C=(1,0)$.
> $N_1=N_0A(t)+\dot N_0=(1\cdot 0+0\cdot 0,\ 1\cdot t+0\cdot 0)+(0,0)=(0,t)$.
> The matrix $[N_0;N_1]$ has rows $(1,0)$ and $(0,t)$. Its determinant is $t$.
> For any $t_0$ pick $t_1>t_0$ with $t_1\ne 0$. The rank is 2, so the pair is observable at every $t_0$.
> The rank 1 at $t_1=0$ shows nothing. The test needs full rank at only one $t_1>t_0$. It is also only sufficient: even if the rank were below $n$ at every $t_1$, the test would give no answer, and the Gramian $W_o(t_0,t)$ would have to decide.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Observable | $\mathbf{u}$, $\mathbf{y}$ on $[0,t_1]$ fix $\mathbf{x}_0$ uniquely |
| Gramian | $W_o(t)=\int_0^te^{A^{\mathsf T}\tau}C^{\mathsf T}Ce^{A\tau}d\tau$ |
| Reconstruction | $\mathbf{x}_0=W_o(t_1)^{-1}\int_0^{t_1}e^{A^{\mathsf T}\tau}C^{\mathsf T}\hat{\mathbf{y}}(\tau)\,d\tau$ |
| Observability matrix | $\mathcal{O}=[C;CA;\dots;CA^{n-1}]$, $nq\times n$, rank $n$ |
| PBH | $\operatorname{rank}[A-\lambda I;\ C]=n$ at every eigenvalue |
| Dual | $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T},D^{\mathsf T})$; swaps $W_c$ and $W_o$ |
| Equivalence | $\hat{\mathcal{C}}=P\mathcal{C}$, $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$ |
| Kalman decomposition | only $(\hat A_{co},\hat B_{co},\hat C_{co})$ is in the transfer matrix |
| Minimal | minimal $\iff$ controllable and observable |
| LTV | $W_o(t_0,t)$ with $\Phi(\tau,t)$; $N_0=C$, $N_{k+1}=N_kA+\dot N_k$ (sufficient) |

## Check yourself
> [!question]- 1. $A$ has rows $(0,1)$ and $(0,0)$. Observable with $C=(1,0)$? With $C=(0,1)$?
> First: $CA=\begin{bmatrix}0&1\end{bmatrix}$, $\mathcal{O}=I$: observable. Second: $CA=\begin{bmatrix}0&0\end{bmatrix}$, rank 1: not observable, $x_1$ is invisible.

> [!question]- 2. $A=\operatorname{diag}(-1,-2)$, $C=(1,0)$. Which mode is unobservable?
> $\mathcal{O}=\begin{bmatrix}1&0\\-1&0\end{bmatrix}$, rank 1. Eigenvector $\mathbf{e}_2$ of $\lambda=-2$ has $C\mathbf{e}_2=0$: mode $-2$ is unobservable.

> [!question]- 3. Dual of the system where $A$ has rows $(0,1)$ and $(-2,-3)$, $B=(0,1)^{\mathsf T}$, $C=(1,0)$.
> $\hat A=\begin{bmatrix}0&-2\\1&-3\end{bmatrix}$, $\hat B=\begin{bmatrix}1\\0\end{bmatrix}$, $\hat C=\begin{bmatrix}0&1\end{bmatrix}$. $[\hat B\ \ \hat A\hat B]=I=\mathcal{O}^{\mathsf T}$.

> [!question]- 4. $A$ has rows $(-4,-3)$ and $(1,0)$, $B=(1,0)^{\mathsf T}$, $C=(1,3)$. Observable? Hidden mode?
> $CA=\begin{bmatrix}-1&-3\end{bmatrix}$, $\mathcal{O}$ has rank 1: not observable. At $\lambda=-3$, $\mathbf{w}=(-3,1)^{\mathsf T}$ and $C\mathbf{w}=0$: mode $-3$ is hidden. $\hat g=\tfrac{s+3}{(s+1)(s+3)}=\tfrac{1}{s+1}$, minimal order 1.

> [!question]- 5. True or false: if $\hat g=N/D$ is coprime with $\deg D=n$, every $n$-state realization is controllable and observable.
> True. Nothing cancels, so the minimal order is $n$, and minimal means controllable and observable.

> [!question]- 6. $A(t)=0$, $C(t)=(1,t^2)$. Observable at $t_0$?
> $N_0=(1,t^2)$, $N_1=(0,2t)$, $\det=2t\ne 0$ for $t\ne 0$. Pick $t_1>t_0$ with $t_1\ne 0$: observable at every $t_0$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L13 - Controllability]]. Next: [[EE502 L15 - State feedback (extra)]] (observers need observability)
- Needs: [[EE502 L11 - Equivalence and realization]] (change of state, canonical forms)
- Full step-by-step notes (PDF): [EE502_Lecture_14_Observability.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf`
- Original slides (PDF, pp. 140-152 and 160-162): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L14 - Observability - quiz]]

Slides not embedded: 140, 160 (section titles).
