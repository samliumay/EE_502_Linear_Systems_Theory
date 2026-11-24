---
course: EE 502 Linear System Theory
lecture: 3
title: Vector spaces, norms and rank
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 36-46)
full_notes: lecture_notes/lecture_03/EE502_Lecture_03_Vector_Spaces_Rank.pdf
---
# EE 502 · Lecture 3 · Vector spaces, norms and rank

> [!summary] In short
> - A subspace is a set closed under adding and scaling. It always contains $\mathbf{0}$.
> - Independent: only the zero combination gives $\mathbf{0}$. Basis: independent and spanning. Dimension: the size of every basis.
> - The representation $\tilde{\mathbf{x}}$ of $\mathbf{x}$ in a basis solves $Q\tilde{\mathbf{x}}=\mathbf{x}$.
> - Three norms: 1, 2, $\infty$. Gram-Schmidt turns independent vectors into an orthonormal set with the same span.
> - Row reduction: $TA=R$ with $T$ invertible. Rank is the number of pivots, and $\operatorname{rank}A+\operatorname{nullity}A=n$.

## 1. Vector space, subspace, span, independence (slides 37-38)
![[ee502_eee501alllecturenotesabo_p037.jpg]]
![[ee502_eee501alllecturenotesabo_p038.jpg]]

**Notes.** A **vector space** is a set $V$ of vectors with a field $\mathbb{F}$ of scalars ($\mathbb{R}$ or $\mathbb{C}$), containing $\mathbf{0}$ and closed under combinations: $\alpha_1\mathbf{v}_1+\alpha_2\mathbf{v}_2\in V$. Here $V=\mathbb{R}^n$ or $\mathbb{C}^n$. Bold $\mathbf{x}_1$ is a vector, italic $x_1$ is the first entry of $\mathbf{x}$.

A **subspace** $S\subseteq V$ is a subset that is itself closed under combinations. Examples in $\mathbb{R}^2$: the horizontal axis $S_1=\{[x_1\ \ 0]^{\mathsf T}\}$ and the line $S_2=\{[x_1\ \ mx_1]^{\mathsf T}\}$. A shifted line (not through the origin) is not a subspace.

**Span**: all linear combinations, $\operatorname{span}\{\mathbf{x}_1,\dots,\mathbf{x}_k\}=\{\alpha_1\mathbf{x}_1+\cdots+\alpha_k\mathbf{x}_k\}$. It is always a subspace.

**Linearly independent**: $\alpha_1\mathbf{x}_1+\cdots+\alpha_k\mathbf{x}_k=\mathbf{0}$ only when all $\alpha_i=0$. **Dependent**: some combination with coefficients not all zero gives $\mathbf{0}$. Equivalent: at least one vector is a combination of the others.

Test: put the vectors as columns of a matrix and row reduce. A column without a pivot (a free variable) means dependent.

> [!example] Test
> $\mathbf{v}_1=(1,0,1)$, $\mathbf{v}_2=(0,1,-1)$, $\mathbf{v}_3=(1,1,0)$. Row reduction leaves column 3 without a pivot. Dependent: $\mathbf{v}_3=\mathbf{v}_1+\mathbf{v}_2$.

> [!warning] Watch out
> - Containing $\mathbf{0}$ does not make a set a subspace (the two coordinate axes together fail addition). Missing $\mathbf{0}$ proves "not a subspace".
> - More than $n$ vectors in $\mathbb{R}^n$ are always dependent. But $n$ or fewer are not automatically independent.

## 2. Dimension, basis, representation (slides 39-40)
![[ee502_eee501alllecturenotesabo_p039.jpg]]
![[ee502_eee501alllecturenotesabo_p040.jpg]]

**Notes.** **Dimension**: the number of vectors in a maximal linearly independent set. $\dim\mathbb{R}^n=n$, $\dim S_1=1$.

**Basis** of $V$: a set that is (i) linearly independent and (ii) spans $V$. The natural basis of $\mathbb{R}^n$ is $\{\mathbf{e}_1,\dots,\mathbf{e}_n\}$, where $\mathbf{e}_i$ has a 1 in place $i$ and zeros elsewhere. Every basis of an $m$-dimensional subspace has exactly $m$ vectors, and any $m$ independent vectors in it form a basis.

**Representation.** Let $\{\mathbf{q}_1,\dots,\mathbf{q}_m\}$ be a basis of $S\subseteq\mathbb{R}^n$ and $Q=[\mathbf{q}_1\ \cdots\ \mathbf{q}_m]$ ($n\times m$). Every $\mathbf{x}\in S$ is $\mathbf{x}=Q\tilde{\mathbf{x}}$ with a unique $\tilde{\mathbf{x}}=[\alpha_1\ \cdots\ \alpha_m]^{\mathsf T}$, the representation of $\mathbf{x}$ in that basis. If $Q$ is square and invertible, $\tilde{\mathbf{x}}=Q^{-1}\mathbf{x}$. In the natural basis $\tilde{\mathbf{x}}=\mathbf{x}$.

**Slide example.** $\mathbf{q}_1=[1\ \ 3]^{\mathsf T}$, $\mathbf{q}_2=[2\ \ 2]^{\mathsf T}$, $\mathbf{x}=[4\ \ 1]^{\mathsf T}$. $\det Q=2-6=-4\neq0$, so it is a basis. Solve $\alpha_1+2\alpha_2=4$, $3\alpha_1+2\alpha_2=1$: $\alpha_2=\frac{11}{4}$, $\alpha_1=-\frac32$.

> [!warning] Watch out
> The slide lists the representation as $[11/4\ \ -3/2]^{\mathsf T}$. That is the order $\{\mathbf{q}_2,\mathbf{q}_1\}$. With $\mathbf{q}_1=[1\ \ 3]^{\mathsf T}$ first, as stated, it is $\tilde{\mathbf{x}}=[-3/2\ \ 11/4]^{\mathsf T}$. The order of the basis vectors fixes the order of the coordinates.

## 3. Norms (slide 41)
![[ee502_eee501alllecturenotesabo_p041.jpg]]

**Notes.** A **norm** $\lVert\cdot\rVert$ is a nonnegative real function on $V$ with: $\lVert\mathbf{x}\rVert=0$ exactly when $\mathbf{x}=\mathbf{0}$, $\lVert\alpha\mathbf{x}\rVert=|\alpha|\lVert\mathbf{x}\rVert$, and the triangle inequality $\lVert\mathbf{x}_1+\mathbf{x}_2\rVert\le\lVert\mathbf{x}_1\rVert+\lVert\mathbf{x}_2\rVert$.

$$\lVert\mathbf{x}\rVert_1=\sum_{i=1}^n|x_i|,\qquad \lVert\mathbf{x}\rVert_2=\sqrt{\mathbf{x}^{\mathsf T}\mathbf{x}}=\sqrt{\sum_{i=1}^n x_i^2},\qquad \lVert\mathbf{x}\rVert_\infty=\max_i|x_i|$$

$\lVert\mathbf{x}\rVert_2$ is the Euclidean length. Useful facts: $|\mathbf{x}^{\mathsf T}\mathbf{y}|\le\lVert\mathbf{x}\rVert_2\lVert\mathbf{y}\rVert_2$ (Cauchy-Schwarz), and $\lVert\mathbf{x}\rVert_\infty\le\lVert\mathbf{x}\rVert_2\le\lVert\mathbf{x}\rVert_1\le n\lVert\mathbf{x}\rVert_\infty$.

> [!example] One vector, three norms
> $\mathbf{x}=[3\ \ -4\ \ 12]^{\mathsf T}$: $\lVert\mathbf{x}\rVert_1=19$, $\lVert\mathbf{x}\rVert_2=\sqrt{169}=13$, $\lVert\mathbf{x}\rVert_\infty=12$. Chain: $12\le13\le19\le36$.

## 4. Orthonormal sets and Gram-Schmidt (slides 42-43)
![[ee502_eee501alllecturenotesabo_p042.jpg]]
![[ee502_eee501alllecturenotesabo_p043.jpg]]

**Notes.** $\mathbf{x}$ is **normalized** if $\lVert\mathbf{x}\rVert=1$. $\mathbf{x}_1,\mathbf{x}_2$ are **orthogonal** if $\mathbf{x}_1^{\mathsf T}\mathbf{x}_2=0$. A set is **orthonormal** if $\mathbf{x}_i^{\mathsf T}\mathbf{x}_j=0$ for $i\neq j$ and $=1$ for $i=j$.

**Gram-Schmidt.** Given independent $\mathbf{v}_1,\dots,\mathbf{v}_m$: from each new vector subtract its projections on the unit vectors already found, then scale to length one.

$$\mathbf{q}_1=\mathbf{v}_1,\quad \mathbf{u}_1=\frac{\mathbf{q}_1}{\lVert\mathbf{q}_1\rVert},\qquad \mathbf{q}_j=\mathbf{v}_j-\sum_{k=1}^{j-1}(\mathbf{u}_k^{\mathsf T}\mathbf{v}_j)\,\mathbf{u}_k,\quad \mathbf{u}_j=\frac{\mathbf{q}_j}{\lVert\mathbf{q}_j\rVert}$$

The result is orthonormal with the same span. $(\mathbf{u}_1^{\mathsf T}\mathbf{v}_2)\mathbf{u}_1$ is the projection of $\mathbf{v}_2$ along $\mathbf{u}_1$.

**Slide example.** $S=\operatorname{span}\{\mathbf{v}_1,\mathbf{v}_2\}$ with $\mathbf{v}_1=[1\ \ 0\ \ 1]^{\mathsf T}$, $\mathbf{v}_2=[0\ \ 1\ \ -1]^{\mathsf T}$.

$$\mathbf{u}_1=\frac{1}{\sqrt2}\begin{bmatrix}1\\0\\1\end{bmatrix},\qquad \mathbf{u}_1^{\mathsf T}\mathbf{v}_2=-\frac{1}{\sqrt2},\qquad \mathbf{q}_2=\begin{bmatrix}0\\1\\-1\end{bmatrix}+\frac12\begin{bmatrix}1\\0\\1\end{bmatrix}=\begin{bmatrix}1/2\\1\\-1/2\end{bmatrix}$$

$$\lVert\mathbf{q}_2\rVert=\sqrt{3/2},\qquad \mathbf{u}_2=\sqrt{\tfrac23}\begin{bmatrix}1/2\\1\\-1/2\end{bmatrix}=\frac{1}{\sqrt6}\begin{bmatrix}1\\2\\-1\end{bmatrix}$$

Check: $\mathbf{u}_1^{\mathsf T}\mathbf{u}_2=0$.

With an orthonormal basis the coordinates are dot products: $\tilde{\mathbf{x}}=Q^{\mathsf T}\mathbf{x}$, no system to solve.

> [!warning] Watch out
> Project onto the unit vectors $\mathbf{u}_k$, not onto the raw $\mathbf{v}_k$. If the list is dependent, some $\mathbf{q}_j=\mathbf{0}$ and the normalization divides by zero.

## 5. Row echelon form (slide 44)
![[ee502_eee501alllecturenotesabo_p044.jpg]]

**Notes.** Elementary row operations: swap two rows, multiply a row by a nonzero constant, add a multiple of one row to another. The **row echelon form** $R$ of $A\in\mathbb{R}^{m\times n}$ has all zero rows at the bottom, and each pivot (first nonzero entry of a row) lies to the right of the pivot above. In the **reduced** form $\tilde R$ every pivot is 1 and is the only nonzero entry in its column. The reduced form is unique.

Each row operation is a left multiplication by an invertible matrix, so $TA=R$ for some invertible $T\in\mathbb{R}^{m\times m}$.

**Slide example.**

$$A=\begin{bmatrix}0&1&1&-3&2\\1&1&2&-2&3\\1&1&2&-2&3\end{bmatrix}\to\begin{bmatrix}1&1&2&-2&3\\0&1&1&-3&2\\0&0&0&0&0\end{bmatrix}\to\tilde R=\begin{bmatrix}1&0&1&1&1\\0&1&1&-3&2\\0&0&0&0&0\end{bmatrix}$$

Steps: $R_1\leftrightarrow R_2$, $R_3\leftarrow R_3-R_1$ (row echelon form), then $R_1\leftarrow R_1-R_2$ (reduced). Here $\tilde T=\begin{bmatrix}-1&1&0\\1&0&0\\0&-1&1\end{bmatrix}$.

Row operations keep column relations: $A\boldsymbol{\alpha}=\mathbf{0}$ exactly when $R\boldsymbol{\alpha}=\mathbf{0}$. In the example, column 3 = column 1 + column 2 in $\tilde R$ and in $A$.

## 6. Rank and nullity (slides 45-46)
![[ee502_eee501alllecturenotesabo_p045.jpg]]
![[ee502_eee501alllecturenotesabo_p046.jpg]]

**Notes.** The columns of $A$ at the pivot positions of $\tilde R$ are the **basic columns**. They are linearly independent. With a column permutation $P$ that brings them first, and $r$ the number of pivots:

$$\tilde RP=\begin{bmatrix}I_r&B\\0&0\end{bmatrix},\qquad \tilde TAP=\tilde T\begin{bmatrix}\hat A_1&\hat A_2\end{bmatrix}=\begin{bmatrix}I_r&B\\0&0\end{bmatrix}\qquad(1)$$

- **Range space** $\mathcal{R}(A)=\{A\mathbf{x}\}$: the span of the columns, a subspace of $\mathbb{R}^m$. Its dimension is the **rank** $r(A)$.
- **Null space** $\mathcal{N}(A)=\{\mathbf{x}\in\mathbb{R}^n: A\mathbf{x}=\mathbf{0}\}$, a subspace of $\mathbb{R}^n$. Its dimension is the **nullity** $\nu(A)$.

**Fact (rank-nullity).** $r(A)=r$ (number of pivots) and $r(A)+\nu(A)=n$.

Proof idea: multiply (1) on the right by $\begin{bmatrix}-B\\ I_{n-r}\end{bmatrix}$. The result is zero, so $\hat A_2=\hat A_1B$: every non-basic column is a combination of basic columns. The $n-r$ columns of $P\begin{bmatrix}-B\\ I_{n-r}\end{bmatrix}$ form a basis of $\mathcal{N}(A)$.

**Recipe.** Row reduce to $\tilde R$. Range basis: the pivot columns of $A$. Null basis: solve each row of $\tilde R\mathbf{x}=\mathbf{0}$ for its pivot variable, one basis vector per free variable.

> [!example] The matrix of slide 44
> Pivots in columns 1, 2, so rank 2 and nullity $5-2=3$. Range basis: $\mathbf{a}_1=(0,1,1)$, $\mathbf{a}_2=(1,1,1)$. Rows of $\tilde R$: $x_1=-x_3-x_4-x_5$, $x_2=-x_3+3x_4-2x_5$. First null vector ($x_3=1$, $x_4=x_5=0$): $\mathbf{n}_1=(-1,-1,1,0,0)$.

> [!warning] Watch out
> Slide errors found by our notes:
> - Slide 45: $B$ is $r\times(n-r)$, not $m\times(n-r)$. "$\check A=AP$" means $[\hat A_1\ \ \hat A_2]=AP$.
> - Slide 46: "reduced column echelon form" should be "reduced row echelon form". The identity block in $\begin{bmatrix}-B\\ I\end{bmatrix}$ has size $n-r$. The last line should read $\nu(A)=n-r=n-r(A)$.
> - $n$ is the number of columns. Take the range basis from the columns of $A$, not of $\tilde R$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Subspace | closed under $\alpha_1\mathbf{x}_1+\alpha_2\mathbf{x}_2$, contains $\mathbf{0}$ |
| Independence | only the zero combination gives $\mathbf{0}$, test by row reduction |
| Basis, dimension | independent and spanning, every basis has $\dim$ vectors |
| Representation | $\mathbf{x}=Q\tilde{\mathbf{x}}$, square $Q$: $\tilde{\mathbf{x}}=Q^{-1}\mathbf{x}$, orthonormal: $\tilde{\mathbf{x}}=Q^{\mathsf T}\mathbf{x}$ |
| Norms | $\lVert\mathbf{x}\rVert_1=\sum\lvert x_i\rvert$, $\lVert\mathbf{x}\rVert_2=\sqrt{\mathbf{x}^{\mathsf T}\mathbf{x}}$, $\lVert\mathbf{x}\rVert_\infty=\max\lvert x_i\rvert$ |
| Gram-Schmidt | $\mathbf{q}_j=\mathbf{v}_j-\sum_{k<j}(\mathbf{u}_k^{\mathsf T}\mathbf{v}_j)\mathbf{u}_k$, $\mathbf{u}_j=\mathbf{q}_j/\lVert\mathbf{q}_j\rVert$ |
| Echelon forms | $TA=R$, $T$ invertible, column relations survive |
| Rank-nullity | rank = number of pivots, $\operatorname{rank}A+\operatorname{nullity}A=n$, $\hat A_2=\hat A_1B$ |

## Check yourself
> [!question]- 1. Is $\{\mathbf{x}\in\mathbb{R}^2: x_1x_2=0\}$ a subspace?
> No. $(1,0)$ and $(0,1)$ are in the set, their sum $(1,1)$ is not ($1\cdot1\neq0$).

> [!question]- 2. Representation of $\mathbf{x}=(3,1)$ in the basis $\mathbf{q}_1=(1,1)$, $\mathbf{q}_2=(1,-1)$?
> $\alpha_1+\alpha_2=3$, $\alpha_1-\alpha_2=1$ gives $\tilde{\mathbf{x}}=(2,1)$. Check: $2(1,1)+(1,-1)=(3,1)$.

> [!question]- 3. Norms of $\mathbf{x}=(1,-2,2)$?
> $\lVert\mathbf{x}\rVert_1=5$, $\lVert\mathbf{x}\rVert_2=\sqrt9=3$, $\lVert\mathbf{x}\rVert_\infty=2$.

> [!question]- 4. Apply Gram-Schmidt to $\mathbf{v}_1=(1,1)$, $\mathbf{v}_2=(1,0)$.
> $\mathbf{u}_1=(1,1)/\sqrt2$. $\mathbf{u}_1^{\mathsf T}\mathbf{v}_2=1/\sqrt2$, $\mathbf{q}_2=(1,0)-(\frac12,\frac12)=(\frac12,-\frac12)$, $\mathbf{u}_2=(1,-1)/\sqrt2$.

> [!question]- 5. Rank, nullity and a null-space basis of $\begin{bmatrix}1&2&3\\2&4&7\end{bmatrix}$
> $R_2\leftarrow R_2-2R_1$, $R_1\leftarrow R_1-3R_2$: $\tilde R=\begin{bmatrix}1&2&0\\0&0&1\end{bmatrix}$. Rank 2, nullity 1. $x_1=-2x_2$, $x_3=0$: basis $\{(-2,1,0)\}$.

> [!question]- 6. (Quiz style) $A=\begin{bmatrix}1&2&0&1\\2&4&1&4\\3&6&1&5\end{bmatrix}$: RREF, rank, range and null bases.
> $\tilde R=\begin{bmatrix}1&2&0&1\\0&0&1&2\\0&0&0&0\end{bmatrix}$, pivots in columns 1 and 3, rank 2. Range basis: $(1,2,3)$, $(0,1,1)$. Null basis: $(-2,1,0,0)$, $(-1,0,-2,1)$. $B=\begin{bmatrix}2&1\\0&2\end{bmatrix}$, so $\mathbf{a}_2=2\mathbf{a}_1$, $\mathbf{a}_4=\mathbf{a}_1+2\mathbf{a}_3$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L02 - LTI models and linearization]]. Next: [[EE502 L04 - Equations, eigenvalues, diagonalization]]
- Used by Quiz 3 (12 Nov, no calculator, slides 36-64) and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_03_Vector_Spaces_Rank.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_03/EE502_Lecture_03_Vector_Spaces_Rank.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_03/EE502_Lecture_03_Vector_Spaces_Rank.pdf`
- Original slides (PDF, pp. 36-46): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: 36 (section title).
