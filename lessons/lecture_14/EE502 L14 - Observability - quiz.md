---
course: EE 502 Linear System Theory
lesson: EE502 L14 - Observability
type: quiz
questions: 17
---

# EE502 L14 - Observability - quiz

Lesson note: [[EE502 L14 - Observability]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. The model is $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$ with $n$ states. The observability matrix is $\mathcal{O}=[C;\ CA;\ \dots;\ CA^{n-1}]$ (blocks stacked as rows), the Gramian is $W_o(t)=\int_0^te^{A^{\mathsf T}\tau}C^{\mathsf T}Ce^{A\tau}\,d\tau$, and the PBH test asks $\operatorname{rank}[A-\lambda I;\ C]=n$ ($A-\lambda I$ with $C$ below it) at every eigenvalue $\lambda$ of $A$.

## 1. Definition and two examples (slides 141-142)

### Q1 (slide 141)

The definition of observability asks only for the initial state $\mathbf{x}_0$, and it uses the input $\mathbf{u}$ as well as the output $\mathbf{y}$ on $[0,t_1]$. Which pair of reasons is right: why $\mathbf{x}_0$ is enough to know $\mathbf{x}(t)$ on the whole interval, and why $\mathbf{u}$ must be known?

- A) $\mathbf{x}(t)$ follows from $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$ at each $t$. $\mathbf{u}$ is needed only to remove $D\mathbf{u}$ when $D\ne 0$.
- B) $\mathbf{x}(t)$ follows from the solution formula with $\mathbf{x}_0$ and $\mathbf{u}$. $\mathbf{u}$ is needed only to remove $D\mathbf{u}$ when $D\ne 0$.
- C) $\mathbf{x}(t)$ follows from $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$ at each $t$. $\mathbf{u}$ is needed to remove its whole effect from $\mathbf{y}$.
- D) $\mathbf{x}(t)$ follows from the solution formula with $\mathbf{x}_0$ and $\mathbf{u}$. $\mathbf{u}$ is needed to remove its whole effect from $\mathbf{y}$.

> [!success]- Answer
> **D.** $\mathbf{x}(t)=e^{At}\mathbf{x}_0+\int_0^te^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau$. With $\mathbf{x}_0$ and $\mathbf{u}$ known, every term is known.
> The output mixes the response to $\mathbf{x}_0$ and the response to $\mathbf{u}$ (the integral term and $D\mathbf{u}$). Only after the whole input part is subtracted does $Ce^{At}\mathbf{x}_0$ remain.
> - A: Two slips. $C$ is in general not invertible, so $\mathbf{y}$ at one instant does not give $\mathbf{x}(t)$. And the input also acts through the integral term, not only through $D\mathbf{u}$.
> - B: The first reason is right. But even with $D=0$ the integral term $\int_0^tCe^{A(t-\tau)}B\mathbf{u}\,d\tau$ is in $\mathbf{y}$ and must be removed.
> - C: The second reason is right. But $C$ is in general not invertible (for example $C$ is $1\times n$), so $\mathbf{x}(t)$ cannot be read from $\mathbf{y}(t)$ at one instant.

### Q2 (slide 142)

$A$ has the rows $(0,0)$ and $(1,0)$, $C=(2,1)$ and $u=0$. The measurements are $y(0)=3$ and $y(1)=5$. What is $\mathbf{x}_0$?

- A) $\mathbf{x}_0=(1,\ 1)^{\mathsf T}$
- B) $\mathbf{x}_0=(2,\ 1)^{\mathsf T}$
- C) $\mathbf{x}_0=(-2,\ 7)^{\mathsf T}$
- D) $\mathbf{x}_0=(2,\ -1)^{\mathsf T}$

> [!success]- Answer
> **D.** With $u=0$: $x_1(t)=x_{01}$ and $x_2(t)=t\,x_{01}+x_{02}$. So $y(t)=2x_1+x_2=(t+2)x_{01}+x_{02}$.
> $t=0$: $2x_{01}+x_{02}=3$. $t=1$: $3x_{01}+x_{02}=5$. Subtract: $x_{01}=2$, then $x_{02}=3-4=-1$.
> - A: $A^{\mathsf T}$ is used in place of $A$: $x_1=x_{01}+t\,x_{02}$, $x_2=x_{02}$. Then $2x_{01}+x_{02}=3$, $2x_{01}+3x_{02}=5$ give $(1,1)$.
> - B: $x_{02}=3-x_{01}$: the factor 2 in $2x_{01}$ is lost.
> - C: Sign slip $x_2(t)=-t\,x_{01}+x_{02}$. Then $2x_{01}+x_{02}=3$, $x_{01}+x_{02}=5$ give $(-2,7)$.

## 2. The observability Gramian (slides 143-144)

### Q3 (slide 143)

$A$ has the rows $(0,1)$ and $(0,0)$, $C=(1,0)$, $t_1=1$. The input-free output is $\hat y(t)=Ce^{At}\mathbf{x}_0=2+3t$. Use $\mathbf{x}_0=W_o(1)^{-1}\int_0^1e^{A^{\mathsf T}\tau}C^{\mathsf T}\hat y(\tau)\,d\tau$. What is $\mathbf{x}_0$?

- A) $\mathbf{x}_0=(\tfrac72,\ 2)^{\mathsf T}$
- B) $\mathbf{x}_0=(2,\ 3)^{\mathsf T}$
- C) $\mathbf{x}_0=(26,\ 45)^{\mathsf T}$
- D) $\mathbf{x}_0=(\tfrac16,\ \tfrac14)^{\mathsf T}$

> [!success]- Answer
> **B.** $A^2=0$, so $Ce^{A\tau}=(1,\ \tau)$ and $W_o(1)=\int_0^1\begin{bmatrix}1&\tau\\\tau&\tau^2\end{bmatrix}d\tau=\begin{bmatrix}1&\tfrac12\\\tfrac12&\tfrac13\end{bmatrix}$, $\det=\tfrac1{12}$.
> $W_o(1)^{-1}=\begin{bmatrix}4&-6\\-6&12\end{bmatrix}$ and $\mathbf{z}=\int_0^1(1,\tau)^{\mathsf T}(2+3\tau)\,d\tau=(\tfrac72,\ 2)^{\mathsf T}$.
> $\mathbf{x}_0=(14-12,\ -21+24)^{\mathsf T}=(2,3)^{\mathsf T}$. Test: $Ce^{At}\mathbf{x}_0=2+3t$.
> - A: This is $\mathbf{z}$. The multiplication by $W_o(1)^{-1}$ is forgotten.
> - C: The inverse is taken with $+6$ off the diagonal: $\begin{bmatrix}4&6\\6&12\end{bmatrix}\mathbf{z}=(26,45)^{\mathsf T}$.
> - D: Only the adjugate is used, without the factor $1/\det=12$: $\begin{bmatrix}\tfrac13&-\tfrac12\\-\tfrac12&1\end{bmatrix}\mathbf{z}=(\tfrac16,\tfrac14)^{\mathsf T}$.

### Q4 (slide 144)

$A$ has the rows $(1,1)$ and $(0,1)$, $C=(0,1)$. Compute $W_o(t_1)$. Which initial states give the same output as $\mathbf{x}_0=\mathbf{0}$ (with zero input)?

- A) Every $\alpha(0,1)^{\mathsf T}$: the direction where $W_o(t_1)$ is nonzero.
- B) Only $\mathbf{x}_0=\mathbf{0}$: $W_o(t_1)$ is nonsingular for every $t_1>0$.
- C) Every $\mathbf{x}_0\in\mathbb{R}^2$: $W_o(t_1)$ is singular for every $t_1$.
- D) Every $\alpha(1,0)^{\mathsf T}$: the null space of $W_o(t_1)$ for every $t_1$.

> [!success]- Answer
> **D.** $e^{A\tau}=e^{\tau}\begin{bmatrix}1&\tau\\0&1\end{bmatrix}$, so $Ce^{A\tau}=(0,\ e^{\tau})$ and $W_o(t_1)=\begin{bmatrix}0&0\\0&\tfrac12(e^{2t_1}-1)\end{bmatrix}$.
> It is singular for every $t_1$. $W_o(t_1)\mathbf{v}=\mathbf{0}$ for $\mathbf{v}=(1,0)^{\mathsf T}$, and $Ce^{A\tau}\alpha\mathbf{v}=0$ for all $\tau$. The output never shows $x_{01}$.
> - A: $(0,1)^{\mathsf T}$ is the direction the output does show: $Ce^{A\tau}(0,1)^{\mathsf T}=e^{\tau}\ne 0$.
> - B: The transpose is on the wrong side: $\int_0^{t_1}e^{A\tau}C^{\mathsf T}Ce^{A^{\mathsf T}\tau}d\tau$ has a positive determinant for $t_1>0$. That is a different matrix.
> - C: "Singular" is read as "zero". The null space has dimension $2-1=1$, not 2.

## 3. Duality and the main theorem (slides 145-146)

### Q5 (slide 145)

$A$ has the rows $(1,2)$ and $(0,3)$, $B=(1,1)^{\mathsf T}$. Check the controllability of $(A,B)$ and use duality. Which statement is right?

- A) $(A,B)$ is not controllable, so the pair with output matrix $(1,1)$ and system matrix $A$ is not observable.
- B) $(A,B)$ is controllable, so the pair with output matrix $(1,1)$ and system matrix $A^{\mathsf T}$ is observable.
- C) $(A,B)$ is not controllable, so the pair with output matrix $(1,1)$ and system matrix $A^{\mathsf T}$ is not observable.
- D) $(A,B)$ is controllable, so the pair with output matrix $(1,1)$ and system matrix $A$ is observable.

> [!success]- Answer
> **C.** $AB=(3,3)^{\mathsf T}$, so $[B\ \ AB]$ has the rows $(1,3)$, $(1,3)$: rank 1, not controllable.
> Duality: $(A,B)$ controllable iff $(B^{\mathsf T},A^{\mathsf T})$ observable. Direct: $B^{\mathsf T}A^{\mathsf T}=(3,3)$, so $\mathcal{O}$ has the rows $(1,1)$, $(3,3)$: rank 1, not observable.
> - A: Duality is used without transposing $A$. For $(B^{\mathsf T},A)$: $B^{\mathsf T}A=(1,5)$, rows $(1,1)$, $(1,5)$, rank 2. That pair is observable.
> - B: The controllability matrix is built with $A^{\mathsf T}$: $[B\ \ A^{\mathsf T}B]$ has the columns $(1,1)^{\mathsf T}$, $(1,5)^{\mathsf T}$, rank 2. With $A$ the rank is 1.
> - D: Two slips: the controllability matrix with $A^{\mathsf T}$ (as in B) and duality without transposing $A$ (as in A).

### Q6 (slide 146, rank test)

$A$ has the rows $(0,1,0)$, $(0,0,1)$, $(-6,-11,-6)$ and $C=(8,6,1)$. Find $\operatorname{rank}\mathcal{O}$ and the unobservable subspace (the null space of $\mathcal{O}$).

- A) $\operatorname{rank}\mathcal{O}=3$; the unobservable subspace is $\{\mathbf{0}\}$.
- B) $\operatorname{rank}\mathcal{O}=2$; the line spanned by $(1,\ 2,\ 4)^{\mathsf T}$.
- C) $\operatorname{rank}\mathcal{O}=2$; the line spanned by $(3,\ 4,\ 1)^{\mathsf T}$.
- D) $\operatorname{rank}\mathcal{O}=2$; the line spanned by $(1,\ -2,\ 4)^{\mathsf T}$.

> [!success]- Answer
> **D.** $CA=(-6,-3,0)$, $CA^2=(0,-6,-3)$. $\mathcal{O}$ has the rows $(8,6,1)$, $(-6,-3,0)$, $(0,-6,-3)$.
> Row 1 $=-\tfrac43$ row 2 $-\tfrac13$ row 3, rows 2 and 3 are independent: rank 2.
> Row 2: $v_2=-2v_1$. Row 3: $v_3=-2v_2=4v_1$. So $\mathbf{v}=(1,-2,4)^{\mathsf T}$. Row 1: $8-12+4=0$.
> - A: $\mathcal{O}$ is built with $A^{\mathsf T}$: rows $C$, $CA^{\mathsf T}=(6,1,-120)$, $C(A^{\mathsf T})^2=(1,-120,673)$ have rank 3. (Checking $\operatorname{rank}A=3$ gives the same wrong answer.)
> - B: The minus signs are dropped when solving rows 2 and 3. Row 2 gives $-6-6\ne 0$.
> - C: The left null space is found: $\mathbf{w}^{\mathsf T}\mathcal{O}=\mathbf{0}$ for $\mathbf{w}=(3,4,1)^{\mathsf T}$. The unobservable subspace needs $\mathcal{O}\mathbf{v}=\mathbf{0}$, and row 1 gives $24+24+1=49\ne 0$.

### Q7 (slide 146, PBH test)

For the same pair, $A$ has the rows $(0,1,0)$, $(0,0,1)$, $(-6,-11,-6)$, $C=(8,6,1)$, and the eigenvalues of $A$ are $-1,-2,-3$. Use the PBH test. Which modes are unobservable?

- A) None: all three modes are observable.
- B) Only $\lambda=-2$.
- C) $\lambda=-1$ and $\lambda=-3$.
- D) All three: $-1$, $-2$ and $-3$.

> [!success]- Answer
> **B.** $A$ is a companion matrix, so the right eigenvector is $\mathbf{w}=(1,\lambda,\lambda^2)^{\mathsf T}$ and $C\mathbf{w}=8+6\lambda+\lambda^2=(\lambda+2)(\lambda+4)$.
> $\lambda=-1$: $3$. $\lambda=-3$: $-1$. $\lambda=-2$: $0$. So $[A+2I;\ C]\mathbf{w}=\mathbf{0}$ and the rank is $2<3$. At $-1$ and $-3$ the rank is 3.
> - A: Left eigenvectors are used, as for controllability. $\mathbf{v}^{\mathsf T}=(6,5,1),(3,4,1),(2,3,1)$ give $C\mathbf{v}=79,49,35$. Observability needs the right eigenvector.
> - C: The test is read backwards. Rank 3 means the mode passes; rank $<3$ means it is unobservable.
> - D: Only $\operatorname{rank}(A-\lambda I)$ is checked. It is 2 at every eigenvalue; the row $C$ below it decides.

## 4. Invariance, controllable and uncontrollable parts (slides 147-150)

### Q8 (slide 147)

Change the state by $\hat{\mathbf{x}}=P\mathbf{x}$, so $\hat A=PAP^{-1}$ and $\hat C=CP^{-1}$. Which formula for $\hat{\mathcal{O}}$ and which description of the unobservable subspace are right? ($\mathbf{v}$ is an unobservable state in the old coordinates.)

- A) $\hat{\mathcal{O}}=\mathcal{O}P$; in the new coordinates it is $\hat{\mathbf{v}}=P^{-1}\mathbf{v}$.
- B) $\hat{\mathcal{O}}=\mathcal{O}P$; in the new coordinates it is $\hat{\mathbf{v}}=P\mathbf{v}$.
- C) $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$; in the new coordinates it is $\hat{\mathbf{v}}=P\mathbf{v}$.
- D) $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$; in the new coordinates it is $\hat{\mathbf{v}}=P^{-1}\mathbf{v}$.

> [!success]- Answer
> **C.** Block $k$: $\hat C\hat A^k=CP^{-1}(PAP^{-1})^k=CA^kP^{-1}$, so $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$. $P^{-1}$ is nonsingular, so the rank does not change.
> $\hat{\mathcal{O}}\hat{\mathbf{v}}=\mathbf{0}$ iff $\mathcal{O}(P^{-1}\hat{\mathbf{v}})=\mathbf{0}$, so $\hat{\mathbf{v}}=P\mathbf{v}$: the same states in new coordinates, same dimension.
> - A: The change is read as $\mathbf{x}=P\hat{\mathbf{x}}$ ($\hat A=P^{-1}AP$). Then $\hat{\mathcal{O}}=\mathcal{O}P$ and $\hat{\mathbf{v}}=P^{-1}\mathbf{v}$ follow, but for the wrong convention.
> - B: Two slips: $\hat{\mathcal{O}}=\mathcal{O}P$ (wrong convention, as in A), and then $\mathbf{v}$ mapped by $P$, which does not match that formula.
> - D: The formula is right, but the null vector is mapped with the wrong matrix: $\mathcal{O}P^{-1}(P^{-1}\mathbf{v})\ne\mathbf{0}$ in general.

### Q9 (slide 148)

$A$ has the rows $(0,1)$ and $(-2,-3)$, $B=(1,-1)^{\mathsf T}$, $C=(1,0)$. Apply Theorem 1 with $\mathbf{q}_1=B$, $\mathbf{q}_2=(0,1)^{\mathsf T}$, $P^{-1}=[\mathbf{q}_1\ \ \mathbf{q}_2]$. Which eigenvalue is the uncontrollable mode, and what is the transfer function $G(s)=C(sI-A)^{-1}B$?

- A) Uncontrollable mode $-2$; $G(s)=\dfrac{1}{s+1}$
- B) Uncontrollable mode $-1$; $G(s)=\dfrac{1}{s+2}$
- C) Uncontrollable mode $-1$; $G(s)=\dfrac{1}{s+1}$
- D) Uncontrollable mode $-2$; $G(s)=\dfrac{1}{s+2}$

> [!success]- Answer
> **A.** $AB=(-1,1)^{\mathsf T}=-B$, so $\operatorname{rank}[B\ \ AB]=1$.
> $A\mathbf{q}_1=-\mathbf{q}_1$ and $A\mathbf{q}_2=(1,-3)^{\mathsf T}=\mathbf{q}_1-2\mathbf{q}_2$. So $\hat A=\begin{bmatrix}-1&1\\0&-2\end{bmatrix}$, $\hat B=(1,0)^{\mathsf T}$, $\hat C=(1,0)$.
> $\hat A_c=-1$, $\hat A_{\bar c}=-2$: the mode $-2$ is uncontrollable. $G(s)=\hat C_c(s-\hat A_c)^{-1}\hat B_c=\dfrac{1}{s+1}$.
> - B: The two blocks are swapped: the mode and the transfer function are both taken from the wrong block.
> - C: The mode is taken from the wrong block: $-1$ is $\hat A_c$, the controllable one.
> - D: The uncontrollable mode is kept in $G(s)$. In fact it is the one that cancels.

### Q10 (slide 149)

In the proof of Theorem 1, $P^{-1}=[\mathbf{q}_1\ \cdots\ \mathbf{q}_n]$, where $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$ are independent columns of $\mathcal{C}=[B\ \ AB\ \cdots\ A^{n-1}B]$. Why is the lower left block $\hat A_{21}$ of $\hat A=PAP^{-1}$ zero?

- A) $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$ are eigenvectors of $A$, so each $A\mathbf{q}_j$ is a multiple of $\mathbf{q}_j$.
- B) The added vectors $\mathbf{q}_{n_1+1},\dots,\mathbf{q}_n$ are orthogonal to $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$.
- C) The column span of $\mathcal{C}$ is $A$-invariant, so $A\mathbf{q}_j$ stays in the span of $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$.
- D) The columns of $B$ are among the $\mathbf{q}_j$, so the zero block of $\hat B$ forces $\hat A_{21}=0$.

> [!success]- Answer
> **C.** Column $j$ of $\hat A$ holds the coordinates of $A\mathbf{q}_j$. $A\mathcal{C}=[AB\ \cdots\ A^nB]$, and $A^nB$ is a combination of $B,\dots,A^{n-1}B$ (Cayley-Hamilton). So for $j\le n_1$, $A\mathbf{q}_j$ is in the span of $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$, and its coordinates along $\mathbf{q}_{n_1+1},\dots,\mathbf{q}_n$ (the entries of $\hat A_{21}$) are zero.
> - A: Not needed and in general false. In the slide example $\mathbf{q}_1=(0,1,0)^{\mathsf T}$ and $A\mathbf{q}_1=(1,1,1)^{\mathsf T}$.
> - B: Coordinates in a basis do not need orthogonality. The added vectors are any completion to a basis.
> - D: The zero block of $\hat B$ is a second result of the same argument. It does not imply $\hat A_{21}=0$.

### Q11 (slide 150)

$A$ has the rows $(1,1,0)$, $(0,1,0)$, $(0,1,1)$, $B$ has the columns $(0,1,0)^{\mathsf T}$ and $(1,0,1)^{\mathsf T}$, $C=(1,1,1)$, and $\operatorname{rank}\mathcal{C}=2$. Take $\mathbf{q}_1,\mathbf{q}_2$ = the columns of $B$, $\mathbf{q}_3=(1,1,0)^{\mathsf T}$, $Q=[\mathbf{q}_1\ \ \mathbf{q}_2\ \ \mathbf{q}_3]$, so $\hat A=Q^{-1}AQ$ and $\hat C=CQ$. What are $\hat A_{12}$ (the top two entries of column 3) and $\hat C_{\bar c}$ (entry 3 of $\hat C$)?

- A) $\hat A_{12}=(1,\ 2)^{\mathsf T}$, $\hat C_{\bar c}=1$
- B) $\hat A_{12}=(0,\ 1)^{\mathsf T}$, $\hat C_{\bar c}=2$
- C) $\hat A_{12}=(0,\ 1)^{\mathsf T}$, $\hat C_{\bar c}=1$
- D) $\hat A_{12}=(1,\ 2)^{\mathsf T}$, $\hat C_{\bar c}=2$

> [!success]- Answer
> **B.** $A\mathbf{q}_3=(2,1,1)^{\mathsf T}$. Solve $a\mathbf{q}_1+b\mathbf{q}_2+c\mathbf{q}_3=(2,1,1)^{\mathsf T}$: row 3 gives $b=1$, row 1 $b+c=2$ so $c=1$, row 2 $a+c=1$ so $a=0$.
> So $\hat A_{12}=(0,1)^{\mathsf T}$ (and $\hat A_{\bar c}=1$). $\hat C_{\bar c}=C\mathbf{q}_3=1+1+0=2$.
> The transfer matrix uses only $(\hat A_c,\hat B_c,\hat C_c)$, and these do not depend on $\mathbf{q}_3$.
> - A: $Q$ and $Q^{-1}$ are swapped in both formulas: $QAQ^{-1}$ has column 3 equal to $(1,2,1)^{\mathsf T}$, and $CQ^{-1}=(0,1,1)$.
> - C: $\hat A$ is right, but $\hat C=CQ^{-1}=(0,1,1)$ is used in place of $CQ$.
> - D: $\hat C$ is right, but $\hat A=QAQ^{-1}$ is used in place of $Q^{-1}AQ$.

## 5. Observable parts and the Kalman decomposition (slides 151-152)

### Q12 (slide 151)

$A$ has the rows $(0,1)$ and $(-2,-3)$, $B=(0,1)^{\mathsf T}$, $C=(1,1)$. Apply Theorem 2 with $P$ having the rows $\mathbf{p}_1=C$ and $\mathbf{p}_2=(0,1)$, so $\hat A=PAP^{-1}$. Which eigenvalue is the unobservable mode, and what is the transfer function $G(s)=C(sI-A)^{-1}B$?

- A) Unobservable mode $-1$; $G(s)=\dfrac{1}{s+2}$
- B) Unobservable mode $-2$; $G(s)=\dfrac{1}{s+1}$
- C) Unobservable mode $-2$; $G(s)=\dfrac{1}{s+2}$
- D) Unobservable mode $-1$; $G(s)=\dfrac{1}{s+1}$

> [!success]- Answer
> **A.** $CA=(-2,-2)=-2C$, so $\operatorname{rank}\mathcal{O}=1$. $P^{-1}$ has the rows $(1,-1)$, $(0,1)$.
> $\hat A=\begin{bmatrix}-2&0\\-2&-1\end{bmatrix}$, $\hat B=(1,1)^{\mathsf T}$, $\hat C=(1,0)$. So $\hat A_o=-2$ and $\hat A_{\bar o}=-1$.
> $G(s)=\hat C_o(s-\hat A_o)^{-1}\hat B_o=\dfrac{1}{s+2}$. Direct: $\dfrac{s+1}{(s+1)(s+2)}$. PBH: $\mathbf{w}=(1,-1)^{\mathsf T}$, $A\mathbf{w}=-\mathbf{w}$, $C\mathbf{w}=0$.
> - B: The two blocks are swapped: the mode and the transfer function are both taken from the wrong block.
> - C: The mode is taken from the wrong block: $-2$ is $\hat A_o$, the observable one.
> - D: The unobservable mode is kept in $G(s)$. In fact it is the one that cancels.

### Q13 (slide 151, rows)

Theorem 1 builds $P^{-1}$ from columns of $\mathcal{C}$. Theorem 2 builds $P$ from rows of $\mathcal{O}$. Why rows, and why $P$ instead of $P^{-1}$?

- A) Theorem 2 is Theorem 1 for $(A,C^{\mathsf T})$. Its controllability matrix has the rows of $\mathcal{O}$ as columns.
- B) The rows of $\mathcal{O}$ are left eigenvectors of $A$, so they must be the rows of $P$, not of $P^{-1}$.
- C) Theorem 2 is Theorem 1 for $(A^{\mathsf T},C^{\mathsf T})$. Its controllability matrix is $\mathcal{O}^{\mathsf T}$; transposing back gives $P$.
- D) Rows or columns work alike. Putting rows of $\mathcal{O}$ in $P$ is only the slide's convention.

> [!success]- Answer
> **C.** The dual pair $(A^{\mathsf T},C^{\mathsf T})$ has controllability matrix $[C^{\mathsf T}\ \ A^{\mathsf T}C^{\mathsf T}\ \cdots]=\mathcal{O}^{\mathsf T}$. Its columns are the transposed rows of $\mathcal{O}$.
> Theorem 1 for the dual gives $Q^{-1}$ with these columns. Transposing $QA^{\mathsf T}Q^{-1}$ back gives $(Q^{-1})^{\mathsf T}AQ^{\mathsf T}$, so $P=(Q^{-1})^{\mathsf T}$, whose rows are rows of $\mathcal{O}$.
> - A: Duality without transposing $A$. $[C^{\mathsf T}\ \ AC^{\mathsf T}\ \cdots]$ is not $\mathcal{O}^{\mathsf T}$ in general.
> - B: The rows of $\mathcal{O}$ ($C$, $CA$, ...) are in general not eigenvectors of anything.
> - D: Rows of $\mathcal{O}$ put as columns of $P^{-1}$ do not give the zero blocks $\hat A_{12}=0$ and $\hat C=[\hat C_o\ \ 0]$.

### Q14 (slide 152)

$A=\operatorname{diag}(-1,-2,-3,-4)$, $B=(1,1,0,0)^{\mathsf T}$, $C=(1,0,1,0)$. In which Kalman parts are the modes $-2$ and $-3$, and what is the dimension of a minimal realization? ($c$ controllable, $\bar c$ uncontrollable, $o$ observable, $\bar o$ unobservable.)

- A) $-2$ in $\bar co$, $-3$ in $c\bar o$; minimal dimension 1
- B) $-2$ in $c\bar o$, $-3$ in $\bar co$; minimal dimension 2
- C) $-2$ in $\bar co$, $-3$ in $c\bar o$; minimal dimension 2
- D) $-2$ in $c\bar o$, $-3$ in $\bar co$; minimal dimension 1

> [!success]- Answer
> **D.** With distinct diagonal entries, mode $i$ is controllable iff $b_i\ne 0$ and observable iff $c_i\ne 0$.
> $-2$: $b_2=1$, $c_2=0$, so $c\bar o$. $-3$: $b_3=0$, $c_3=1$, so $\bar co$. ($-1$ is $co$, $-4$ is $\bar c\bar o$.)
> $C(sI-A)^{-1}B=\sum_ic_ib_i/(s-\lambda_i)=\dfrac{1}{s+1}$. Only the $co$ part is left: a minimal realization has 1 state.
> - A: $B$ and $C$ swap roles: controllability is read from $C$ and observability from $B$.
> - B: The minimal dimension is taken as $\operatorname{rank}\mathcal{C}=2$ (or $\operatorname{rank}\mathcal{O}=2$). It is the size of the $co$ part.
> - C: Two slips: $B$ and $C$ swapped (as in A) and the dimension taken as a rank (as in B).

### Q15 (slide 152, minimality)

A realization with 3 states gives, before any cancelling, $C(sI-A)^{-1}B=\dfrac{s+3}{(s+1)(s+2)(s+3)}$, so the eigenvalues of $A$ are $-1,-2,-3$. Without computing $\mathcal{C}$ or $\mathcal{O}$, what can you conclude?

- A) Not minimal. The mode $-3$ is uncontrollable or unobservable, but the transfer function cannot say which.
- B) Not minimal. The mode $-3$ is unobservable, because it is cancelled by a zero of the output.
- C) Not minimal. The mode $-3$ is uncontrollable, because the input cannot reach a cancelled pole.
- D) Minimal. $A$ has three distinct eigenvalues and the denominator has degree 3.

> [!success]- Answer
> **A.** $s+3$ cancels: $\hat g(s)=\dfrac{1}{(s+1)(s+2)}$, degree 2. A minimal realization has 2 states, so this one is not minimal, and by Theorem 3 it is not controllable or not observable (or both).
> A cancellation of $-3$ appears for an uncontrollable mode, an unobservable mode, or both. Only $\mathcal{C}$, $\mathcal{O}$ or the PBH tests at $\lambda=-3$ decide.
> - B: A cancellation does not say which property fails. An uncontrollable mode cancels in the same way.
> - C: The same mistake the other way. An unobservable mode cancels in the same way.
> - D: The degree is counted before cancelling. After cancelling it is 2.

## 6. Observability of LTV systems (slides 161-162)

### Q16 (slide 161)

For an LTV system the dual is $\dot{\hat{\mathbf{x}}}=-A^{\mathsf T}(t)\hat{\mathbf{x}}+C^{\mathsf T}(t)\mathbf{u}$, while the LTI dual uses $A^{\mathsf T}$. For constant $A$, $C$, do the two duals give different observability tests? And for the scalar case $A(t)=2t$, what is the transition matrix $\hat\Phi(t,t_0)$ of the dual?

- A) Different tests, since $-A^{\mathsf T}$ can change the rank. $\hat\Phi(t,t_0)=e^{t_0^2-t^2}$.
- B) The same test, since only signs of blocks change. $\hat\Phi(t,t_0)=e^{t_0^2-t^2}$.
- C) The same test, since only signs of blocks change. $\hat\Phi(t,t_0)=e^{t^2-t_0^2}$.
- D) Different tests, since $-A^{\mathsf T}$ can change the rank. $\hat\Phi(t,t_0)=e^{t^2-t_0^2}$.

> [!success]- Answer
> **B.** The controllability matrix of $(-A^{\mathsf T},C^{\mathsf T})$ is $[C^{\mathsf T}\ \ -A^{\mathsf T}C^{\mathsf T}\ \ (A^{\mathsf T})^2C^{\mathsf T}\ \cdots]$. Only the signs of some blocks change, so the rank is the same: both give $\operatorname{rank}\mathcal{O}=n$.
> Scalar: $\dot{\hat x}=-2t\,\hat x$ gives $\hat\Phi(t,t_0)=e^{-(t^2-t_0^2)}=e^{t_0^2-t^2}=\Phi(t_0,t)$, as the slide formula $\hat\Phi(t,t_0)=\Phi(t_0,t)^{\mathsf T}$ says.
> - A: Multiplying a block by $-1$ does not change the rank.
> - C: The minus sign of $-A^{\mathsf T}$ is dropped: $\dot{\hat x}=2t\,\hat x$ gives $\Phi(t,t_0)$, not $\Phi(t_0,t)$.
> - D: Two slips: the sign change is thought to change the rank (as in A), and the minus sign is dropped (as in C).

### Q17 (slide 162)

$A(t)$ has the rows $(0,t)$ and $(0,0)$, $C=(1,0)$. Use the rank test $N_0=C$, $N_1=N_0A(t)+\dot N_0$. At $t_1=0$ the matrix $[N_0;\ N_1]$ has rank 1. Does that show that the pair is unobservable?

- A) No. The rank is 2 at every $t_1\ne 0$, so the pair is observable at every $t_0$.
- B) No. The rank is 2 only for $t_0\ne 0$, so the pair is observable at every $t_0\ne 0$.
- C) Yes. A rank below $n$ at one $t_1>t_0$ shows that the pair is unobservable.
- D) Yes. The rank is 1 at every $t_1$, so the pair is unobservable at every $t_0$.

> [!success]- Answer
> **A.** $N_0=(1,0)$, $N_1=(1,0)A(t)+(0,0)=(0,t)$. $\det[N_0;\ N_1]=t$.
> For any $t_0$ pick $t_1>t_0$ with $t_1\ne 0$: rank 2, so the pair is observable at $t_0$. The test needs full rank at only one $t_1>t_0$, and it is only sufficient.
> - B: The rank is checked at $t_1=t_0$. The test allows any $t_1>t_0$, so $t_0=0$ also works.
> - C: The test is sufficient only. A low rank at one $t_1$, or even at every $t_1$, proves nothing.
> - D: $N_1$ is built with $A^{\mathsf T}$: $N_0A^{\mathsf T}=(0,0)$. With $A$ it is $(0,t)$.
