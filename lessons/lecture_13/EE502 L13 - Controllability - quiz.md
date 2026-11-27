---
course: EE 502 Linear System Theory
lesson: EE502 L13 - Controllability
type: quiz
questions: 19
---

# EE502 L13 - Controllability - quiz

Lesson note: [[EE502 L13 - Controllability]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. The model is $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$ with $n$ states. The controllability matrix is $\mathcal{C}=[B\ \ AB\ \cdots\ A^{n-1}B]$, the Gramian is $W_c(t)=\int_0^te^{A\tau}BB^{\mathsf T}e^{A^{\mathsf T}\tau}\,d\tau$, and the PBH test asks $\operatorname{rank}[A-\lambda I\ \ B]=n$ at every eigenvalue $\lambda$ of $A$.

## 1. Definition and two examples (slides 131-132)

### Q1 (slide 131, definition)

A student writes: "If $(A,B)$ is controllable, a bounded input brings the state to $\mathbf{x}_f$ and the state then stays at $\mathbf{x}_f$." Compare this with the definition of controllability. Which judgement is right?

- A) Only "stays at $\mathbf{x}_f$" is wrong. The definition does ask for a bounded input.
- B) Only "bounded input" is wrong. The definition does ask that the state stays at $\mathbf{x}_f$.
- C) Neither part is wrong. A bounded input reaches $\mathbf{x}_f$ and then holds the state.
- D) Both parts are wrong. The input size is free, and only $\mathbf{x}(t_f)=\mathbf{x}_f$ is asked.

> [!success]- Answer
> **D.** The definition: for every $\mathbf{x}_0$ and every $\mathbf{x}_f$ there are a finite $t_f>0$ and some input on $[0,t_f]$ with $\mathbf{x}(t_f)=\mathbf{x}_f$.
> It puts no limit on the input. The input can be very large, mainly for small $t_f$.
> It asks for $\mathbf{x}_f$ only at the one instant $t_f$. To stay there we would need $A\mathbf{x}_f+B\mathbf{u}=\mathbf{0}$, which is in general not possible for every $\mathbf{x}_f$.
> - A: The definition says nothing about the size of the input, so "bounded" is a second mistake.
> - B: The definition says nothing about what happens after $t_f$, so "stays" is a second mistake.
> - C: Both parts add conditions that the definition does not contain.

### Q2 (slide 131, example)

Take $A$ with the rows $(0,1)$, $(1,0)$, $B=(1,1)^{\mathsf T}$ and the output $y=x_1$. In the coordinates $z_1=(x_1+x_2)/2$, $z_2=(x_1-x_2)/2$ the system splits into a controllable part and an uncontrollable part. Which eigenvalue belongs to the uncontrollable mode, and what is the reduced transfer function $G(s)$ from $u$ to $y$?

- A) Uncontrollable mode $\lambda=1$; $G(s)=\dfrac{1}{s-1}$
- B) Uncontrollable mode $\lambda=-1$; $G(s)=\dfrac{1}{s-1}$
- C) Uncontrollable mode $\lambda=-1$; $G(s)=\dfrac{1}{s+1}$
- D) Uncontrollable mode $\lambda=1$; $G(s)=\dfrac{1}{s+1}$

> [!success]- Answer
> **B.** $\dot x_1=x_2+u$, $\dot x_2=x_1+u$. Add and subtract: $\dot z_1=z_1+u$ and $\dot z_2=-z_2$.
> So $\bar A=\operatorname{diag}(1,-1)$, $\bar B=(1,0)^{\mathsf T}$: $z_2$ (mode $\lambda=-1$) gets no input.
> $(sI-A)^{-1}B=\dfrac{1}{s^2-1}(s+1,\ s+1)^{\mathsf T}=\dfrac{1}{s-1}(1,1)^{\mathsf T}$, so $G(s)=\dfrac{1}{s-1}$. The uncontrollable mode cancels.
> - A: The mode that shows up in $G(s)$ is named as the uncontrollable one. It is the controllable one.
> - C: The uncontrollable mode is kept in $G(s)$. In fact it is the one that cancels.
> - D: The two blocks are swapped: the mode and the transfer function are both taken from the wrong block.

### Q3 (slide 132)

The double integrator $\dot x_1=u$, $\dot x_2=x_1$ starts at $\mathbf{x}_0=(0,0)^{\mathsf T}$. With $U(t)=\int_0^tu$ we have $x_1(t)=U(t)$ and $x_2(t)=\int_0^tU$. We want $\mathbf{x}(1)=(1,0)^{\mathsf T}$ with $U(\tau)=a\tau+b\tau^2$. Which input $u(\tau)$ does this?

- A) $u(\tau)=3\tau-\tfrac12$
- B) $u(\tau)=4-6\tau$
- C) $u(\tau)=6\tau-2$
- D) $u(\tau)=3\tau^2-2\tau$

> [!success]- Answer
> **C.** Conditions: $U(1)=a+b=1$ and $\int_0^1U\,d\tau=\tfrac a2+\tfrac b3=0$.
> The second gives $b=-\tfrac{3a}{2}$. Then $a-\tfrac{3a}{2}=1$, so $a=-2$, $b=3$.
> $U(\tau)=3\tau^2-2\tau$ and $u=\dot U=6\tau-2$. Check: $U(1)=1$, $\int_0^1U=1-1=0$.
> $U$ ends at $+1$ with net area $0$, so it must go negative on the way.
> - A: $\int_0^1\tau\,d\tau$ taken as $1$: $a+\tfrac b3=0$ gives $a=-\tfrac12$, $b=\tfrac32$.
> - B: The second condition is set to $1$ (the target of $x_1$) instead of $0$: $a=4$, $b=-3$.
> - D: This is $U(\tau)$, not its derivative $u=\dot U$.

## 2. Main theorem of LTI controllability (slides 133-137)

### Q4 (slide 133, rank test)

Take $A$ with the rows $(1,1,0)$, $(0,1,0)$, $(0,0,1)$ and $B=(0,1,1)^{\mathsf T}$. Build the controllability matrix. What is the rank that decides, and is the pair controllable?

- A) Rank $3$; controllable
- B) Rank $1$; not controllable
- C) Rank $2$; not controllable
- D) Rank $2$; controllable

> [!success]- Answer
> **C.** $AB=(1,1,1)^{\mathsf T}$, $A^2B=A(1,1,1)^{\mathsf T}=(2,1,1)^{\mathsf T}$.
> $\mathcal{C}$ has the rows $(0,1,2)$, $(1,1,1)$, $(1,1,1)$. Rows 2 and 3 are equal, rows 1 and 2 are independent: rank $2<3$.
> Not controllable: $\dot x_2=x_2+u$ and $\dot x_3=x_3+u$ are the same equation, so $x_2-x_3$ cannot be steered.
> - A: This is the rank of $A$, not of $\mathcal{C}$.
> - B: $A^{\mathsf T}$ is used in place of $A$. Then $[B\ \ A^{\mathsf T}B\ \ (A^{\mathsf T})^2B]$ has all three columns equal to $(0,1,1)^{\mathsf T}$: rank $1$.
> - D: Only $[B\ \ AB]$ is built, and its rank $2$ is compared with its $2$ columns instead of with $n=3$.

### Q5 (slide 133, two inputs)

Same $A$ (rows $(1,1,0)$, $(0,1,0)$, $(0,0,1)$). Now $B$ has two columns $\mathbf{b}_1=(0,1,1)^{\mathsf T}$ and $\mathbf{b}_2=(0,0,1)^{\mathsf T}$. What is the size of $\mathcal{C}$, and what is its rank with both inputs?

- A) $\mathcal{C}$ is $3\times3$; rank $3$, controllable
- B) $\mathcal{C}$ is $3\times6$; rank $3$, controllable
- C) $\mathcal{C}$ is $3\times6$; rank $2$, not controllable
- D) $\mathcal{C}$ is $3\times3$; rank $2$, not controllable

> [!success]- Answer
> **B.** With $p=2$ inputs, $\mathcal{C}=[B\ \ AB\ \ A^2B]$ is $n\times np=3\times6$.
> Take the columns $\mathbf{b}_1$, $\mathbf{b}_2$, $A\mathbf{b}_1=(1,1,1)^{\mathsf T}$. The matrix with the rows $(0,0,1)$, $(1,0,1)$, $(1,1,1)$ has $\det=1\ne0$.
> So the rank is $3$: controllable with both inputs, though each alone fails.
> - A: One column per power of $A$ is counted. Each block $A^kB$ has $p=2$ columns.
> - C: The rank is taken as the larger single-input rank ($2$ for $\mathbf{b}_1$). Columns of both inputs together give more.
> - D: $\mathbf{b}_2$ is left out: $[\mathbf{b}_1\ \ A\mathbf{b}_1\ \ A^2\mathbf{b}_1]$ is $3\times3$ with rank $2$ (the single-input pair).

### Q6 (slide 134)

To check the steering input, the slide writes $\mathbf{x}(t_f)=e^{At_f}\mathbf{x}_0-\int_0^{t_f}e^{A(t_f-\tau)}BB^{\mathsf T}e^{A^{\mathsf T}(t_f-\tau)}d\tau\;W_c(t_f)^{-1}\bigl[e^{At_f}\mathbf{x}_0-\mathbf{x}_f\bigr]$. Step 1 takes the factor $W_c(t_f)^{-1}[\dots]$ out of the integral. Step 2 says the integral equals $W_c(t_f)$. Why is each step allowed?

- A) 1: it is a constant vector on the right, so it leaves on the right. 2: put $\sigma=t_f-\tau$.
- B) 1: matrix products commute, so it may leave on the left. 2: put $\sigma=t_f-\tau$.
- C) 1: it is a constant vector on the right, so it leaves on the right. 2: true by definition, no change.
- D) 1: matrix products commute, so it may leave on the left. 2: true by definition, no change.

> [!success]- Answer
> **A.** Step 1: the factor does not depend on $\tau$. It stands on the right of the integrand, so it leaves the integral on the right. The order of the matrix product is kept.
> Step 2: $\sigma=t_f-\tau$, $d\sigma=-d\tau$, the limits $0,t_f$ become $t_f,0$. The sign and the swapped limits cancel:
> $\int_0^{t_f}e^{A\sigma}BB^{\mathsf T}e^{A^{\mathsf T}\sigma}d\sigma=W_c(t_f)$. Then $W_cW_c^{-1}=I$ and only $\mathbf{x}_f$ is left.
> - B: Matrix products do not commute in general. Moving the factor to the left would change the product.
> - C: $W_c$ is defined with $e^{A\sigma}$, not with $e^{A(t_f-\sigma)}$. The change of variable is needed.
> - D: Two slips: commuting matrices, and the definition of $W_c$ misread.

### Q7 (slide 135)

Take $A$ with the rows $(-1,0)$, $(1,-2)$ and $B=(1,1)^{\mathsf T}$. Which eigenvalue of $A$ gives an uncontrollable mode, and what is $\operatorname{rank}\mathcal{C}$?

- A) $\lambda=-2$; $\operatorname{rank}\mathcal{C}=1$
- B) $\lambda=-1$; $\operatorname{rank}\mathcal{C}=1$
- C) $\lambda=-2$; $\operatorname{rank}\mathcal{C}=2$
- D) $\lambda=-1$; $\operatorname{rank}\mathcal{C}=2$

> [!success]- Answer
> **A.** $A$ is triangular: $\lambda=-1,-2$. Left eigenvectors: $(1,0)$ for $-1$ and $(1,-1)$ for $-2$, since $(1,-1)A=(-2,2)$.
> $(1,0)B=1\ne0$ but $(1,-1)B=0$. So $\operatorname{rank}[A+2I\ \ B]=1$: the mode $\lambda=-2$ is uncontrollable.
> $AB=(-1,-1)^{\mathsf T}=-B$, so $\mathcal{C}$ has the rows $(1,-1)$, $(1,-1)$: rank $1$.
> - B: $AB=-B$ makes $B$ a right eigenvector for $\lambda=-1$. That mode is the one the input excites, the controllable one.
> - C: $2$ is the rank of $A$, not of $\mathcal{C}$.
> - D: Two slips: the mode taken from $AB=-B$, and the rank of $A$.

### Q8 (slide 136)

Take $A$ with the rows $(1,1,0)$, $(0,1,0)$, $(0,0,1)$ (only eigenvalue $\lambda=1$) and $B=(0,1,1)^{\mathsf T}$. Find $r_1=\operatorname{rank}[A-I\ \ B]$. Then find $r_2$, the largest value of $\operatorname{rank}[A-I\ \ \mathbf{b}]$ over all single columns $\mathbf{b}\in\mathbb{R}^3$.

- A) $r_1=3$, $r_2=3$
- B) $r_1=2$, $r_2=3$
- C) $r_1=3$, $r_2=2$
- D) $r_1=2$, $r_2=2$

> [!success]- Answer
> **D.** $[A-I\ \ B]$ has the rows $(0,1,0,0)$, $(0,0,0,1)$, $(0,0,0,1)$. Rows 2 and 3 are equal: $r_1=2<3$, PBH fails at $\lambda=1$.
> $A-I$ has only one nonzero entry, so $\operatorname{rank}(A-I)=1$. One extra column raises the rank by at most $1$: $r_2=2<3$.
> So no single input can ever control this $A$. It needs at least two inputs.
> - A: The test is done with $[A\ \ B]$ and $[A\ \ \mathbf{b}]$, that is at $\lambda=0$, which is not an eigenvalue. There PBH always passes.
> - B: The bound for $r_2$ uses $\operatorname{rank}A=3$ instead of $\operatorname{rank}(A-I)=1$.
> - C: $r_1$ is computed at $\lambda=0$ (not an eigenvalue): $\operatorname{rank}[A\ \ B]=3$.

### Q9 (slide 137, Cayley-Hamilton)

Take $A$ with the rows $(1,2)$, $(3,4)$ and $B=(1,0)^{\mathsf T}$. Use the Cayley-Hamilton theorem to write $A^2B=\alpha\,AB+\beta\,B$. What are $\alpha$ and $\beta$?

- A) $\alpha=5$, $\beta=-2$
- B) $\alpha=-5$, $\beta=-2$
- C) $\alpha=5$, $\beta=2$
- D) $\alpha=-5$, $\beta=2$

> [!success]- Answer
> **C.** $\det(sI-A)=s^2-(1+4)s+(4-6)=s^2-5s-2$. Cayley-Hamilton: $A^2-5A-2I=0$, so $A^2=5A+2I$ and $A^2B=5AB+2B$.
> Check: $AB=(1,3)^{\mathsf T}$, $5AB+2B=(7,15)^{\mathsf T}$, and directly $A^2B=A(1,3)^{\mathsf T}=(7,15)^{\mathsf T}$.
> So $A^2B$ adds nothing to the span of $B$, $AB$. That is why $\mathcal{C}$ stops at $A^{n-1}B$.
> - A: Determinant sign slip: $\det A$ taken as $6-4=2$, so $A^2=5A-2I$. This gives $(3,15)^{\mathsf T}$.
> - B: The terms are moved across without changing sign: $A^2=-5A-2I$. This gives $(-7,-15)^{\mathsf T}$.
> - D: Trace sign slip: $s^2+5s-2$, so $A^2=-5A+2I$. This gives $(-3,-15)^{\mathsf T}$.

### Q10 (slide 137, change of coordinates)

Take $A$ with the rows $(1,2)$, $(3,4)$ and $B=(1,0)^{\mathsf T}$, so $\mathcal{C}$ has the rows $(1,1)$, $(0,3)$. Use $\bar{\mathbf{x}}=P\mathbf{x}$ with $P$ with the rows $(1,1)$, $(0,1)$, so $\bar A=PAP^{-1}$, $\bar B=PB$. What is $\bar{\mathcal{C}}=[\bar B\ \ \bar A\bar B]$?

- A) Rows $(1,4)$ and $(0,3)$
- B) Rows $(1,1)$ and $(0,3)$
- C) Rows $(1,-2)$ and $(0,3)$
- D) Rows $(1,2)$ and $(0,3)$

> [!success]- Answer
> **A.** $P^{-1}$ has the rows $(1,-1)$, $(0,1)$. $\bar A=PAP^{-1}$ has the rows $(4,2)$, $(3,1)$, and $\bar B=(1,0)^{\mathsf T}$.
> $\bar A\bar B=(4,3)^{\mathsf T}$, so $\bar{\mathcal{C}}$ has the rows $(1,4)$, $(0,3)$.
> In general $\bar A^k\bar B=PA^kP^{-1}PB=PA^kB$, so $\bar{\mathcal{C}}=P\mathcal{C}$. $P$ is nonsingular, so the rank is the same: controllability does not depend on the coordinates.
> - B: $A$ is not transformed ($\bar A=A$, $\bar B=PB=B$). This just gives $\mathcal{C}$ again.
> - C: $P$ and $P^{-1}$ are swapped ($\bar A=P^{-1}AP$, $\bar B=P^{-1}B$). This gives $P^{-1}\mathcal{C}$.
> - D: The product is taken on the wrong side: $\mathcal{C}P$ instead of $P\mathcal{C}$.

## 3. Gramian example and the double pendulum (slides 138-139)

### Q11 (slide 138, Gramian)

Take $A$ with the rows $(-1,0)$, $(1,-2)$ and $B=(1,1)^{\mathsf T}$. What is the entry $(1,2)$ of the Gramian $W_c(t)$?

- A) $1-e^{-t}$
- B) $\dfrac{1-e^{-2t}}{2}$
- C) $\dfrac{1-e^{-3t}}{3}$
- D) $\dfrac{e^{2t}-1}{2}$

> [!success]- Answer
> **B.** $AB=(-1,-1)^{\mathsf T}=-B$, so $e^{A\tau}B=e^{-\tau}B$ and $B^{\mathsf T}e^{A^{\mathsf T}\tau}=e^{-\tau}B^{\mathsf T}$.
> $W_c(t)=\int_0^te^{-2\tau}d\tau\begin{bmatrix}1&1\\1&1\end{bmatrix}=\dfrac{1-e^{-2t}}{2}\begin{bmatrix}1&1\\1&1\end{bmatrix}$.
> All four entries are equal, so $\det W_c(t)=0$ for every $t$: not controllable. $W_c\mathbf{v}=\mathbf{0}$ for $\mathbf{v}=(1,-1)^{\mathsf T}$.
> - A: The factor $e^{-\tau}$ is not squared: the integrand has two such factors, $e^{-2\tau}$.
> - C: The integrand is $e^{A\tau}BB^{\mathsf T}e^{A\tau}$, without the transpose. Then $B^{\mathsf T}e^{A\tau}=(2e^{-\tau}-e^{-2\tau},\ e^{-2\tau})$ and the entry $(1,2)$ is $\int_0^te^{-3\tau}d\tau$.
> - D: The sign of the eigenvalue is lost: $e^{A\tau}B=e^{\tau}B$.

### Q12 (slide 138, input)

For the double integrator $A$ with the rows $(0,0)$, $(1,0)$ and $B=(1,0)^{\mathsf T}$: $e^{At}$ has the rows $(1,0)$, $(t,1)$ and $W_c(2)$ has the rows $(2,2)$, $(2,\tfrac83)$. Use $\mathbf{u}(\tau)=-B^{\mathsf T}e^{A^{\mathsf T}(t_f-\tau)}W_c(t_f)^{-1}[e^{At_f}\mathbf{x}_0-\mathbf{x}_f]$ to bring $\mathbf{x}_0=(1,0)^{\mathsf T}$ to $\mathbf{x}_f=\mathbf{0}$ in $t_f=2$. What are $u(\tau)$ and its energy $E=\int_0^2u^2\,d\tau$?

- A) $u(\tau)=1-\tfrac32\tau$; $E=2$
- B) $u(\tau)=1-\tfrac32\tau$; $E=\tfrac{62}{3}$
- C) $u(\tau)=\tfrac32\tau-2$; $E=2$
- D) $u(\tau)=\tfrac32\tau-2$; $E=\tfrac{62}{3}$

> [!success]- Answer
> **C.** $W_c(2)^{-1}$ has the rows $(2,-\tfrac32)$, $(-\tfrac32,\tfrac32)$. $\boldsymbol{\xi}=e^{2A}\mathbf{x}_0=(1,2)^{\mathsf T}$, $W_c^{-1}\boldsymbol{\xi}=(-1,\tfrac32)^{\mathsf T}$.
> $B^{\mathsf T}e^{A^{\mathsf T}(2-\tau)}=[1\ \ 2-\tau]$, so $u=-[-1+\tfrac32(2-\tau)]=\tfrac32\tau-2$.
> $E=\int_0^2(\tfrac94\tau^2-6\tau+4)d\tau=6-12+8=2=\boldsymbol{\xi}^{\mathsf T}W_c^{-1}\boldsymbol{\xi}$. It is the minimum energy.
> - A: $e^{A^{\mathsf T}\tau}$ is used instead of $e^{A^{\mathsf T}(t_f-\tau)}$. This input ends at $x_2(2)=2$, not $0$.
> - B: Two slips: $\tau$ in place of $t_f-\tau$, and $E=\boldsymbol{\xi}^{\mathsf T}W_c\,\boldsymbol{\xi}$ without the inverse.
> - D: The energy is taken as $\boldsymbol{\xi}^{\mathsf T}W_c(2)\,\boldsymbol{\xi}=6+\tfrac{44}{3}=\tfrac{62}{3}$, without the inverse.

### Q13 (slide 139)

Double pendulum: $A$ has the rows $(0,1,0,0)$, $(-a,0,b,0)$, $(0,0,0,1)$, $(0,0,-c,0)$ with $a,b,c>0$. Let the input enter the second equation only: $B=(0,1,0,0)^{\mathsf T}$. Which statement is right?

- A) $\operatorname{rank}\mathcal{C}=2$; $x_3$, $x_4$ depend on neither $x_1$, $x_2$ nor $u$.
- B) $\operatorname{rank}\mathcal{C}=2$; $x_1$, $x_2$ depend on neither $x_3$, $x_4$ nor $u$.
- C) $\operatorname{rank}\mathcal{C}=4$; the coupling $b$ in row 2 carries $u$ on to $x_3$.
- D) $\operatorname{rank}\mathcal{C}=4$; $A$ is nonsingular, since $a\ne0$ and $c\ne0$.

> [!success]- Answer
> **A.** $AB=(1,0,0,0)^{\mathsf T}$, $A^2B=(0,-a,0,0)^{\mathsf T}$, $A^3B=(-a,0,0,0)^{\mathsf T}$.
> Rows 3 and 4 of $\mathcal{C}$ are zero: rank $2<4$, not controllable.
> Reason: $\dot x_3=x_4$, $\dot x_4=-cx_3$ contain no $x_1$, $x_2$, $u$. The lower pendulum swings by itself.
> - B: Wrong block: $\dot x_2=-ax_1+bx_3+u$ contains both $x_3$ and $u$.
> - C: $b$ in row 2 means $x_3$ acts on $x_2$, not the other way. Reading it as a path from $x_2$ to $x_3$ is the slip $[B\ \ A^{\mathsf T}B\ \cdots]$, which has rank $4$.
> - D: $\det A=ac\ne0$ is true, but that is the rank of $A$, not of $\mathcal{C}$.

## 4. LTV controllability and the Gramian test (slides 154-156)

### Q14 (slide 154)

Scalar system $\dot x=b(t)u$ with $b(t)=1$ for $t<1$ and $b(t)=0$ for $t\ge1$. Is it controllable at $t_0=0$? Is it controllable at $t_0=2$?

- A) Not at $t_0=0$; yes at $t_0=2$
- B) Yes at $t_0=0$; yes at $t_0=2$
- C) Not at $t_0=0$; not at $t_0=2$
- D) Yes at $t_0=0$; not at $t_0=2$

> [!success]- Answer
> **D.** At $t_0=0$: on $[0,1)$, $\dot x=u$. With $t_f=\tfrac12$ and $u=2(x_f-x_0)$ we get $x(\tfrac12)=x_f$. Controllable.
> At $t_0=2$: $\dot x=0$ for all $t\ge2$, so $x(t)=x_0$ for every input. Not controllable.
> For LTV systems the answer depends on the start time: "controllable at $t_0$".
> - A: $b(t)$ is read the wrong way round (as $0$ before $t=1$ and $1$ after).
> - B: The LTI habit: the answer is taken to be the same for every $t_0$.
> - C: $b(t)$ is taken to need $b\ne0$ at every time. Being nonzero on a part of $[t_0,t_f]$ is enough.

### Q15 (slide 155)

Take $A(t)=0$ and $B(t)=(\cos t,\ \sin t)^{\mathsf T}$. Then $\Phi(t,\tau)=I$ and $W_c(0,t)=\int_0^tB(\tau)B(\tau)^{\mathsf T}d\tau$. What is $\det W_c(0,t)$?

- A) $0$
- B) $\dfrac{t^2-\sin^2t}{4}$
- C) $\dfrac{t^2}{4}$
- D) $\dfrac{t^2}{4}-\dfrac{\sin^22t}{16}$

> [!success]- Answer
> **B.** $W_c(0,t)$ has the rows $\bigl(\tfrac t2+\tfrac{\sin2t}{4},\ \tfrac{\sin^2t}{2}\bigr)$ and $\bigl(\tfrac{\sin^2t}{2},\ \tfrac t2-\tfrac{\sin2t}{4}\bigr)$.
> $\det=\tfrac{t^2}{4}-\tfrac{\sin^22t}{16}-\tfrac{\sin^4t}{4}$, and $\tfrac{\sin^22t}{16}=\tfrac{\sin^2t\cos^2t}{4}$, so $\det=\tfrac{t^2-\sin^2t}{4}$.
> It is $>0$ for $t>0$ since $\lvert\sin t\rvert<t$: controllable at $t_0=0$. The direction of $B(t)$ turns, so over time it covers the plane.
> - A: At each instant $BB^{\mathsf T}$ has rank $1$, but a sum (integral) of rank-1 matrices in different directions can have rank $2$.
> - C: Only the average values are kept: $\cos^2,\sin^2\to\tfrac12$ and the off-diagonal entries are dropped.
> - D: The off-diagonal entries $\tfrac{\sin^2t}{2}$ are dropped.

### Q16 (slide 156)

Take $\dot x=b(t)u$ with $b=0$ on $[0,1]$, $b=1$ for $t>1$, and $t_0=0$. Here $\Phi=1$ and $W_c(0,1)=0$. A student says: "$W_c(0,1)$ is singular, so the system is uncontrollable at $t_0=0$." What is $W_c(0,2)$, and what is the right conclusion?

- A) $W_c(0,2)=1$; controllable at $t_0=0$
- B) $W_c(0,2)=2$; controllable at $t_0=0$
- C) $W_c(0,2)=1$; uncontrollable at $t_0=0$
- D) $W_c(0,2)=2$; uncontrollable at $t_0=0$

> [!success]- Answer
> **A.** $W_c(0,t)=\int_0^tb(\tau)^2d\tau$, so $W_c(0,2)=\int_1^21\,d\tau=1\ne0$.
> Theorem 4 asks for $W_c(t_0,t)$ nonsingular for some $t>t_0$. Singular at one $t$ is not enough. Wait until $t>1$, then steer.
> - B: The integral is taken with $b=1$ on all of $[0,2]$, ignoring $b=0$ on $[0,1]$.
> - C: The student's claim is accepted: one singular $W_c(0,1)$ does not decide anything.
> - D: Two slips: $b=1$ on all of $[0,2]$, and the claim accepted.

## 5. A sufficient rank condition for LTV (slides 157-159)

### Q17 (slide 157)

Take $A(t)$ with the rows $(0,1)$, $(0,t)$ and $B(t)=(0,t)^{\mathsf T}$. Theorem 5: $M_0=B$, $M_{k+1}=-AM_k+\dot M_k$; if $\operatorname{rank}[M_0(t_1)\ M_1(t_1)]=2$ for some $t_1>t_0$, the pair is controllable at $t_0$. What is $\det[M_0\ M_1]$, and for which $t_0$ does the theorem give controllability?

- A) $\det=-t^2$; every $t_0$ except $t_0=0$
- B) $\det=t^2$; every $t_0$
- C) $\det=t^2$; every $t_0$ except $t_0=0$
- D) $\det=-t^2$; every $t_0$

> [!success]- Answer
> **B.** $AM_0=(t,t^2)^{\mathsf T}$ and $\dot M_0=(0,1)^{\mathsf T}$, so $M_1=(-t,\ 1-t^2)^{\mathsf T}$.
> $\det\begin{bmatrix}0&-t\\t&1-t^2\end{bmatrix}=0-(-t)(t)=t^2$.
> Rank $2$ at every $t_1\ne0$. For any $t_0$ there is such a $t_1>t_0$, so the pair is controllable at every $t_0$.
> - A: Two slips: the sign $+AM_0$, and the rank checked at $t_1=t_0$ only.
> - C: The rank is checked at $t_1=t_0$. The theorem needs only some $t_1>t_0$.
> - D: Sign slip $M_1=+AM_0+\dot M_0=(t,\ t^2+1)^{\mathsf T}$, which gives $\det=-t^2$.

### Q18 (slide 158)

Take $A=\operatorname{diag}(1,2)$ and $B(t)=(e^t,e^{2t})^{\mathsf T}$, with $M_0=B$, $M_1=-AM_0+\dot M_0$ (Theorem 5, a sufficient condition). Let $z_1=e^{-t}x_1$, $z_2=e^{-2t}x_2$. Which statement is right?

- A) Rank $1$; Theorem 5 itself proves the pair uncontrollable, since $1<2$.
- B) Rank $2$, since $M_1\ne\mathbf{0}$; Theorem 5 proves the pair controllable.
- C) Rank $1$; Theorem 5 says nothing; $\dot z_1=\dot z_2=u$, so the pair is controllable.
- D) Rank $1$; Theorem 5 says nothing; $z_1-z_2$ is constant, so it is uncontrollable.

> [!success]- Answer
> **D.** $AM_0=(e^t,2e^{2t})^{\mathsf T}=\dot M_0$, so $M_1=\mathbf{0}$ and $\operatorname{rank}[M_0\ M_1]=1$ at every $t_1$.
> Theorem 5 is sufficient only, so rank $1$ proves nothing.
> $\dot z_1=-e^{-t}x_1+e^{-t}(x_1+e^tu)=u$ and likewise $\dot z_2=u$. So $z_1-z_2$ never changes: uncontrollable.
> - A: Theorem 5 is used as if it were necessary. A failed sufficient test gives no verdict.
> - B: $\dot M_0$ is forgotten: $M_1=-AM_0=(-e^t,-2e^{2t})^{\mathsf T}$, with $\det[M_0\ M_1]=-e^{3t}\ne0$.
> - C: Each $z_i$ can be steered alone, but both obey the same equation, so they cannot be steered apart.

### Q19 (slide 159)

Take $A(t)$ with the rows $(t,-1,0)$, $(0,-t,t)$, $(0,0,t)$ and $B=(1,0,0)^{\mathsf T}$. Use $M_0=B$, $M_{k+1}=-AM_k+\dot M_k$ (Theorem 5, a sufficient condition). Which statement is right?

- A) $M_2=(t^2,0,0)^{\mathsf T}$; Theorem 5 proves the pair uncontrollable, since rank $1<3$.
- B) $M_2=(t^2-1,0,0)^{\mathsf T}$; Theorem 5 proves the pair uncontrollable, since rank $1<3$.
- C) $M_2=(t^2-1,0,0)^{\mathsf T}$; Theorem 5 says nothing; $x_2,x_3$ never see $x_1$ or $u$.
- D) $M_2=(t^2,0,0)^{\mathsf T}$; Theorem 5 says nothing; $x_2,x_3$ never see $x_1$ or $u$.

> [!success]- Answer
> **C.** $M_1=-AM_0+\dot M_0=(-t,0,0)^{\mathsf T}$. $AM_1=(-t^2,0,0)^{\mathsf T}$, $\dot M_1=(-1,0,0)^{\mathsf T}$, so $M_2=(t^2-1,0,0)^{\mathsf T}$.
> All columns are multiples of $(1,0,0)^{\mathsf T}$: rank $1<3$. Theorem 5 gives no verdict.
> Another argument decides: $\dot x_2=-tx_2+tx_3$, $\dot x_3=tx_3$ contain no $x_1$ and no $u$. Uncontrollable at every $t_0$.
> - A: Two slips: $\dot M_1$ forgotten, and Theorem 5 used as if it were necessary.
> - B: Theorem 5 is sufficient only. Rank $1$ alone proves nothing.
> - D: $\dot M_1=(-1,0,0)^{\mathsf T}$ is forgotten, so $M_2=-AM_1=(t^2,0,0)^{\mathsf T}$.
