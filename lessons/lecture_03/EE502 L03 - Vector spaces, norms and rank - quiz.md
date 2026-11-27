---
course: EE 502 Linear System Theory
lesson: EE502 L03 - Vector spaces, norms and rank
type: quiz
questions: 10
---

# EE502 L03 - Vector spaces, norms and rank - quiz

Lesson note: [[EE502 L03 - Vector spaces, norms and rank]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz all vectors are column vectors. $(a,b,c)$ is short for $[a\ \ b\ \ c]^{\mathsf T}$.

## 1. Vector space, subspace, span, independence (slides 37-38)

### Q1 (slide 37)

A student writes: "$W=\{\mathbf{x}\in\mathbb{R}^2: x_1\ge 0\}$ contains $\mathbf{0}$, and the sum of two vectors of $W$ is again in $W$. So $W$ is a subspace of $\mathbb{R}^2$." What is wrong?

- A) Nothing. These two facts are all a subspace needs.
- B) Addition fails: $(1,2)+(1,-3)=(2,-1)$ is not in $W$.
- C) $\mathbf{0}$ is not in $W$, because it lies on the edge $x_1=0$.
- D) Scaling fails: $-1\cdot(1,0)=(-1,0)$ is not in $W$.

> [!success]- Answer
> **D.** A subspace must be closed under $\alpha\mathbf{x}$ for every real $\alpha$, also negative ones.
> $\mathbf{x}=(1,0)\in W$, but $-\mathbf{x}=(-1,0)$ has $x_1=-1<0$. So $W$ (the right half-plane) is not a subspace.
> - A: Containing $\mathbf{0}$ and closure under addition are not enough. Closure under scaling is missing.
> - B: $(2,-1)$ has $x_1=2\ge0$, so it is in $W$. Only $x_1$ matters. Addition never fails in $W$.
> - C: $x_1=0$ satisfies $x_1\ge0$, so $\mathbf{0}\in W$.

### Q2 (slide 38)

Take $\mathbf{x}_1=(1,2,1)$, $\mathbf{x}_2=(2,1,3)$, $\mathbf{x}_3=(1,-4,t)$. For which $t$ is the set $\{\mathbf{x}_1,\mathbf{x}_2,\mathbf{x}_3\}$ linearly dependent, and how is $\mathbf{x}_3$ written with $\mathbf{x}_1,\mathbf{x}_2$ for that $t$?

- A) Only for $t=3$. Then $\mathbf{x}_3=-3\mathbf{x}_1+2\mathbf{x}_2$.
- B) Only for $t=1$. Then $\mathbf{x}_3=3\mathbf{x}_1-2\mathbf{x}_2$.
- C) Only for $t=3$. Then $\mathbf{x}_3=3\mathbf{x}_1-2\mathbf{x}_2$.
- D) Only for $t=1$. Then $\mathbf{x}_3=-3\mathbf{x}_1+2\mathbf{x}_2$.

> [!success]- Answer
> **A.** Put the vectors as columns and row reduce. $R_2\leftarrow R_2-2R_1$, $R_3\leftarrow R_3-R_1$ give the rows $(1,2,1)$, $(0,-3,-6)$, $(0,1,t-1)$. Then $R_3\leftarrow R_3+\tfrac13R_2$ gives $(0,0,t-3)$.
> For $t=3$ column 3 has no pivot: dependent. Back substitution gives $3\mathbf{x}_1-2\mathbf{x}_2+\mathbf{x}_3=\mathbf{0}$, so $\mathbf{x}_3=-3\mathbf{x}_1+2\mathbf{x}_2$.
> Check: $-3(1,2,1)+2(2,1,3)=(1,-4,3)$.
> - B: $t=1$ comes from setting $t-1=0$ before the last elimination step. The sign of the combination is also wrong.
> - C: $t$ is right, but $3\mathbf{x}_1-2\mathbf{x}_2=(-1,4,-3)=-\mathbf{x}_3$. The sign was not changed when $\mathbf{x}_3$ was moved to the other side.
> - D: The combination is right, but its third entry is $-3+6=3$, so it fits only $t=3$, not $t=1$.

## 2. Dimension, basis, representation (slides 39-40)

### Q3 (slide 39)

$S=\{\mathbf{x}\in\mathbb{R}^4: x_1=x_2,\ x_3=2x_4\}$. Which pair is a basis of $S$, and is the set $\{(1,1,0,0),\ (0,0,2,1),\ (1,1,2,1)\}$ also a basis of $S$?

- A) $\{(1,1,0,0),(0,0,2,1)\}$. $\dim S=3$, and the set of three is a basis.
- B) $\{(1,1,0,0),(0,0,2,1)\}$. $\dim S=2$, and the set of three is not a basis.
- C) $\{(1,1,0,0),(0,0,1,2)\}$. $\dim S=3$, and the set of three is a basis.
- D) $\{(1,1,0,0),(0,0,1,2)\}$. $\dim S=2$, and the set of three is not a basis.

> [!success]- Answer
> **B.** With $x_2=a$ and $x_4=b$ free: $\mathbf{x}=(a,a,2b,b)=a(1,1,0,0)+b(0,0,2,1)$. The two vectors span $S$ and are independent, so $\dim S=2$.
> The set of three spans $S$, but $(1,1,2,1)=(1,1,0,0)+(0,0,2,1)$. It is dependent, so it is not a basis.
> - A: Spanning is not enough. A basis must also be independent, and every basis of $S$ has 2 vectors.
> - C: $(0,0,1,2)$ has $x_3=1$ and $2x_4=4$, so it is not in $S$ ($x_3=2x_4$ was read as $x_4=2x_3$). The verdict on the three vectors is wrong too.
> - D: The verdict is right, but $(0,0,1,2)$ is not in $S$.

### Q4 (slide 40)

$\mathbf{q}_1=(1,1)$, $\mathbf{q}_2=(1,2)$, $\mathbf{p}_1=(1,0)$, $\mathbf{p}_2=(1,1)$ and $\mathbf{x}=(3,5)$. Let $Q=[\mathbf{q}_1\ \ \mathbf{q}_2]$ and $P=[\mathbf{p}_1\ \ \mathbf{p}_2]$, in this order. $\tilde{\mathbf{x}}$ solves $Q\tilde{\mathbf{x}}=\mathbf{x}$ and $\bar{\mathbf{x}}$ solves $P\bar{\mathbf{x}}=\mathbf{x}$. Find $\tilde{\mathbf{x}}$ and the matrix $M$ with $\bar{\mathbf{x}}=M\tilde{\mathbf{x}}$.

- A) $\tilde{\mathbf{x}}=(2,1)$, $M=\begin{bmatrix}0&-1\\1&2\end{bmatrix}$
- B) $\tilde{\mathbf{x}}=(1,2)$, $M=\begin{bmatrix}2&1\\-1&0\end{bmatrix}$
- C) $\tilde{\mathbf{x}}=(2,1)$, $M=\begin{bmatrix}2&1\\-1&0\end{bmatrix}$
- D) $\tilde{\mathbf{x}}=(1,2)$, $M=\begin{bmatrix}0&-1\\1&2\end{bmatrix}$

> [!success]- Answer
> **D.** $Q^{-1}=\begin{bmatrix}2&-1\\-1&1\end{bmatrix}$, so $\tilde{\mathbf{x}}=Q^{-1}\mathbf{x}=(6-5,\ -3+5)=(1,2)$. Check: $1\,(1,1)+2\,(1,2)=(3,5)$.
> $P\bar{\mathbf{x}}=Q\tilde{\mathbf{x}}$ gives $\bar{\mathbf{x}}=P^{-1}Q\,\tilde{\mathbf{x}}$, and $P^{-1}Q=\begin{bmatrix}1&-1\\0&1\end{bmatrix}\begin{bmatrix}1&1\\1&2\end{bmatrix}=\begin{bmatrix}0&-1\\1&2\end{bmatrix}$.
> Check: $M\tilde{\mathbf{x}}=(-2,5)=\bar{\mathbf{x}}$, and $-2\,(1,0)+5\,(1,1)=(3,5)$.
> - A: $(2,1)$ is the representation in the order $\{\mathbf{q}_2,\mathbf{q}_1\}$. The stated order is $\mathbf{q}_1$ first.
> - B: $\tilde{\mathbf{x}}$ is right, but $M=Q^{-1}P$ maps the other way. $M\tilde{\mathbf{x}}=(4,-1)\neq(-2,5)$.
> - C: Both slips: the wrong basis order and $Q^{-1}P$ in place of $P^{-1}Q$.

## 3. Norms (slide 41)

### Q5 (slide 41)

A student says: "$f(\mathbf{x})=\lvert x_1-x_2\rvert$ is a norm on $\mathbb{R}^2$." Which norm property does $f$ fail? Also, for $\mathbf{x}=(1,-3,2)$, what is the 1-norm $\lVert-2\mathbf{x}\rVert_1$?

- A) The triangle inequality fails. $\lVert-2\mathbf{x}\rVert_1=12$.
- B) $f(\mathbf{x})=0$ for some $\mathbf{x}\neq\mathbf{0}$, e.g. $(1,1)$. $\lVert-2\mathbf{x}\rVert_1=6$.
- C) $f(\mathbf{x})=0$ for some $\mathbf{x}\neq\mathbf{0}$, e.g. $(1,1)$. $\lVert-2\mathbf{x}\rVert_1=12$.
- D) The triangle inequality fails. $\lVert-2\mathbf{x}\rVert_1=6$.

> [!success]- Answer
> **C.** A norm is zero only at $\mathbf{0}$. But $f(1,1)=\lvert1-1\rvert=0$ with $(1,1)\neq\mathbf{0}$. So $f$ is not a norm.
> $-2\mathbf{x}=(-2,6,-4)$, so $\lVert-2\mathbf{x}\rVert_1=2+6+4=12$. Same with scaling: $\lvert-2\rvert\cdot(1+3+2)=12$.
> - A: $f$ does satisfy the triangle inequality: $\lvert(x_1+y_1)-(x_2+y_2)\rvert\le\lvert x_1-x_2\rvert+\lvert y_1-y_2\rvert$.
> - B: $6=\max(2,6,4)$ is the $\infty$-norm, not the 1-norm. ($6$ is also $\lVert\mathbf{x}\rVert_1$ with the factor $\lvert-2\rvert$ forgotten.)
> - D: Both parts wrong: the triangle inequality holds, and $6$ is the $\infty$-norm.

## 4. Orthonormal sets and Gram-Schmidt (slides 42-43)

### Q6 (slide 42)

Let $\mathbf{u}_1=\mathbf{v}_1/\lVert\mathbf{v}_1\rVert_2$ and $\mathbf{q}_2=\mathbf{v}_2-(\mathbf{u}_1^{\mathsf T}\mathbf{v}_2)\mathbf{u}_1$. Then $\mathbf{u}_1^{\mathsf T}\mathbf{q}_2=\mathbf{u}_1^{\mathsf T}\mathbf{v}_2-(\mathbf{u}_1^{\mathsf T}\mathbf{v}_2)(\mathbf{u}_1^{\mathsf T}\mathbf{u}_1)$. Which fact makes this zero? If $\mathbf{v}_1$ replaces $\mathbf{u}_1$ in the formula for $\mathbf{q}_2$, what is $\mathbf{v}_1^{\mathsf T}\mathbf{q}_2$?

- A) $\mathbf{u}_1^{\mathsf T}\mathbf{v}_2=0$. Then $\mathbf{v}_1^{\mathsf T}\mathbf{q}_2=0$ for every $\mathbf{v}_1$.
- B) $\mathbf{u}_1^{\mathsf T}\mathbf{u}_1=1$. Then $\mathbf{v}_1^{\mathsf T}\mathbf{q}_2=0$ for every $\mathbf{v}_1$.
- C) $\mathbf{u}_1^{\mathsf T}\mathbf{u}_1=1$. Then $\mathbf{v}_1^{\mathsf T}\mathbf{q}_2=\mathbf{v}_1^{\mathsf T}\mathbf{v}_2\,(1-\lVert\mathbf{v}_1\rVert_2^2)$.
- D) $\mathbf{u}_1^{\mathsf T}\mathbf{v}_2=0$. Then $\mathbf{v}_1^{\mathsf T}\mathbf{q}_2=\mathbf{v}_1^{\mathsf T}\mathbf{v}_2\,(1-\lVert\mathbf{v}_1\rVert_2^2)$.

> [!success]- Answer
> **C.** $\mathbf{u}_1$ is normalized, so $\mathbf{u}_1^{\mathsf T}\mathbf{u}_1=\lVert\mathbf{u}_1\rVert_2^2=1$ and the two terms cancel.
> With $\mathbf{v}_1$: $\mathbf{v}_1^{\mathsf T}\big(\mathbf{v}_2-(\mathbf{v}_1^{\mathsf T}\mathbf{v}_2)\mathbf{v}_1\big)=\mathbf{v}_1^{\mathsf T}\mathbf{v}_2-(\mathbf{v}_1^{\mathsf T}\mathbf{v}_2)\lVert\mathbf{v}_1\rVert_2^2=\mathbf{v}_1^{\mathsf T}\mathbf{v}_2\,(1-\lVert\mathbf{v}_1\rVert_2^2)$.
> This is not zero unless $\lVert\mathbf{v}_1\rVert_2=1$ or $\mathbf{v}_1^{\mathsf T}\mathbf{v}_2=0$.
> - A: If $\mathbf{u}_1^{\mathsf T}\mathbf{v}_2=0$ there is nothing to subtract. The cancellation works for any $\mathbf{v}_2$. The second part is also wrong.
> - B: The first part is right. But $\mathbf{v}_1$ has the same direction as $\mathbf{u}_1$, not the same length, and the length enters squared.
> - D: The expression is right, but the reason for the zero is $\mathbf{u}_1^{\mathsf T}\mathbf{u}_1=1$.

### Q7 (slide 43)

Apply Gram-Schmidt (2-norm, in the order $\mathbf{v}_1,\mathbf{v}_2,\mathbf{v}_3$) to $\mathbf{v}_1=(1,1,0)$, $\mathbf{v}_2=(1,0,1)$, $\mathbf{v}_3=(0,1,1)$. You get $\mathbf{u}_1=\frac{1}{\sqrt2}(1,1,0)$ and $\mathbf{u}_2=\frac{1}{\sqrt6}(1,-1,2)$. What is $\mathbf{u}_3$?

- A) $\left(-\tfrac23,\ \tfrac23,\ \tfrac23\right)$
- B) $\tfrac{1}{\sqrt3}(-1,\ 1,\ 1)$
- C) $\left(-\tfrac12,\ \tfrac12,\ \tfrac12\right)$
- D) $\tfrac{1}{\sqrt6}(-1,\ 1,\ 2)$

> [!success]- Answer
> **B.** $\mathbf{u}_1^{\mathsf T}\mathbf{v}_3=\frac{1}{\sqrt2}$ and $\mathbf{u}_2^{\mathsf T}\mathbf{v}_3=\frac{1}{\sqrt6}$. The projections are $(\frac12,\frac12,0)$ and $(\frac16,-\frac16,\frac13)$.
> $\mathbf{q}_3=(0,1,1)-(\frac12,\frac12,0)-(\frac16,-\frac16,\frac13)=(-\frac23,\frac23,\frac23)$, $\lVert\mathbf{q}_3\rVert_2=\frac{2}{\sqrt3}$, so $\mathbf{u}_3=\frac{1}{\sqrt3}(-1,1,1)$.
> Check: $\mathbf{u}_1^{\mathsf T}\mathbf{u}_3=0$ and $\mathbf{u}_2^{\mathsf T}\mathbf{u}_3=0$.
> - A: This is $\mathbf{q}_3$. The step without normalising: its length is $\frac{2}{\sqrt3}\neq1$.
> - C: This is $\mathbf{q}_3/\lVert\mathbf{q}_3\rVert_2^2$, the square root forgotten. Its length is $\frac{\sqrt3}{2}\neq1$.
> - D: Only the projection on $\mathbf{u}_1$ was removed: $(-\frac12,\frac12,1)$ normalised. It is not orthogonal to $\mathbf{u}_2$ ($\mathbf{u}_2^{\mathsf T}\mathbf{u}_3=\frac{1}{3}$).

## 5. Row echelon form (slide 44)

### Q8 (slide 44)

$A=\begin{bmatrix}1&2&1\\2&4&3\\1&2&2\end{bmatrix}$. Row reduce $[A\ \ I_3]$ and stop as soon as the left block is the reduced row echelon form $\tilde R$. The right block is then $\tilde T$, with $\tilde TA=\tilde R$. What are $\tilde R$ and the first row of $\tilde T$?

- A) $\tilde R=\begin{bmatrix}1&2&0\\0&0&1\\0&0&0\end{bmatrix}$, first row of $\tilde T$: $(3,-1,0)$
- B) $\tilde R=\begin{bmatrix}1&2&1\\0&0&1\\0&0&0\end{bmatrix}$, first row of $\tilde T$: $(1,-1,0)$
- C) $\tilde R=\begin{bmatrix}1&2&0\\0&0&1\\0&0&0\end{bmatrix}$, first row of $\tilde T$: $(1,-1,0)$
- D) $\tilde R=\begin{bmatrix}1&2&1\\0&0&1\\0&0&0\end{bmatrix}$, first row of $\tilde T$: $(3,-1,0)$

> [!success]- Answer
> **A.** $R_2\leftarrow R_2-2R_1$, $R_3\leftarrow R_3-R_1$, $R_3\leftarrow R_3-R_2$ give the echelon form. The right block now has row 1 $(1,0,0)$ and row 2 $(-2,1,0)$.
> $R_1\leftarrow R_1-R_2$ clears the entry above the second pivot. Left: $(1,2,0)$. Right: $(1,0,0)-(-2,1,0)=(3,-1,0)$.
> Check: $3(1,2,1)-(2,4,3)=(1,2,0)$.
> - B: The left block stopped at the echelon form (not reduced: the 1 above the second pivot stays). On the right, row 2 of $I_3$ was subtracted, not the current row 2.
> - C: $\tilde R$ is right, but $(1,-1,0)A=(-1,-2,-2)\neq(1,2,0)$. The current row 2 $(-2,1,0)$ must be subtracted.
> - D: The last step was done on the right block only. The matrix shown is not reduced.

## 6. Rank and nullity (slides 45-46)

### Q9 (slide 45)

$A=\begin{bmatrix}1&3&2\\2&6&5\end{bmatrix}$ with columns $\mathbf{a}_1,\mathbf{a}_2,\mathbf{a}_3$. The basic columns are the columns of $A$ at the pivot positions of $\tilde R$ (the reduced row echelon form). $P$ brings them first, and $\tilde RP=\begin{bmatrix}I_r&B\end{bmatrix}$. Find the basic columns, $B$ and the range $\mathcal{R}(A)$.

- A) $\mathbf{a}_1,\mathbf{a}_3$. $B=\begin{bmatrix}3\\0\end{bmatrix}$. $\mathcal{R}(A)=\mathbb{R}^2$.
- B) $\mathbf{a}_1,\mathbf{a}_2$. $B=\begin{bmatrix}3\\0\end{bmatrix}$. $\mathcal{R}(A)$ is a plane in $\mathbb{R}^3$.
- C) $\mathbf{a}_1,\mathbf{a}_3$. $B=\begin{bmatrix}3\\6\end{bmatrix}$. $\mathcal{R}(A)$ is a plane in $\mathbb{R}^3$.
- D) $\mathbf{a}_1,\mathbf{a}_2$. $B=\begin{bmatrix}3\\6\end{bmatrix}$. $\mathcal{R}(A)=\mathbb{R}^2$.

> [!success]- Answer
> **A.** $R_2\leftarrow R_2-2R_1$, then $R_1\leftarrow R_1-2R_2$: $\tilde R=\begin{bmatrix}1&3&0\\0&0&1\end{bmatrix}$. Pivots in columns 1 and 3, so the basic columns are $\mathbf{a}_1=(1,2)$, $\mathbf{a}_3=(2,5)$.
> $P$ swaps columns 2 and 3: $\tilde RP=\begin{bmatrix}1&0&3\\0&1&0\end{bmatrix}$, so $B=(3,0)$.
> $\mathcal{R}(A)$ is spanned by two independent vectors of $\mathbb{R}^2$, so $\mathcal{R}(A)=\mathbb{R}^2$ and $r(A)=2$.
> - B: The first two columns are not the basic ones: $\mathbf{a}_2=3\mathbf{a}_1$ is dependent. The range lies in $\mathbb{R}^m=\mathbb{R}^2$, not in $\mathbb{R}^n$.
> - C: $(3,6)$ is the block $\hat A_2$ of $AP$, not $B$ of $\tilde RP$. The range is again put in the wrong space.
> - D: The range is right, but the basic columns are wrong and $B$ was read from $AP$.

### Q10 (slide 46)

A new matrix: $A=\begin{bmatrix}1&2&1\\3&6&4\end{bmatrix}$. Its reduced row echelon form is $\tilde R=\begin{bmatrix}1&2&0\\0&0&1\end{bmatrix}$, so $r=2$. $P=\begin{bmatrix}1&0&0\\0&0&1\\0&1&0\end{bmatrix}$ swaps columns 2 and 3, and $\tilde RP=\begin{bmatrix}I_2&B\end{bmatrix}$. A basis of $\mathcal{N}(A)$ is given by the columns of $P\begin{bmatrix}-B\\I_{n-r}\end{bmatrix}$. Find that basis. Also, what is the nullity of a $4\times6$ matrix with rank 4?

- A) $\{(-2,0,1)\}$. The $4\times6$ matrix has nullity 0.
- B) $\{(-2,1,0)\}$. The $4\times6$ matrix has nullity 2.
- C) $\{(-2,1,0)\}$. The $4\times6$ matrix has nullity 0.
- D) $\{(-2,0,1)\}$. The $4\times6$ matrix has nullity 2.

> [!success]- Answer
> **B.** $\tilde RP=\begin{bmatrix}1&0&2\\0&1&0\end{bmatrix}$, so $B=(2,0)$. $n-r=1$, so $\begin{bmatrix}-B\\I_1\end{bmatrix}=(-2,0,1)$. $P$ swaps entries 2 and 3 back to the original column order: $(-2,1,0)$.
> Check: $A(-2,1,0)=(-2+2,\ -6+6)=(0,0)$. So $\nu(A)=1$ and $2+1=3=n$.
> In $r(A)+\nu(A)=n$, $n$ is the number of columns. For the $4\times6$ matrix: $\nu=6-4=2$.
> - A: $P$ was not applied, and $A(-2,0,1)=(-1,-2)\neq\mathbf{0}$. Nullity 0 uses the number of rows as $n$.
> - C: The basis is right, but $4-4=0$ takes $n$ as the number of rows.
> - D: The nullity is right, but $(-2,0,1)$ is still in the permuted order and is not in $\mathcal{N}(A)$.
