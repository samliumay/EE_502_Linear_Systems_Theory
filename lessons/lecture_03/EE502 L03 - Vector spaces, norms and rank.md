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

> [!question]- Check (slide 37): Find the mistake. "$W=\{\mathbf{x}\in\mathbb{R}^2: x_1\ge 0\}$ contains $\mathbf{0}$ and the sum of two vectors of $W$ is again in $W$. So $W$ is a subspace of $\mathbb{R}^2$."
> The two facts are true, but they are not enough. A subspace must also be closed under multiplication by every scalar $\alpha\in\mathbb{R}$, also negative ones.
> Take $\mathbf{x}=[1\ \ 0]^{\mathsf T}\in W$ and $\alpha=-1$. Then $\alpha\mathbf{x}=[-1\ \ 0]^{\mathsf T}$ has $x_1=-1<0$, so it is not in $W$.
> $W$ (the right half-plane) is not a subspace. The slide's condition $\alpha_1\mathbf{x}_1+\alpha_2\mathbf{x}_2\in S$ for all $\alpha_1,\alpha_2\in\mathbb{R}$ checks both operations at once.

> [!question]- Check (slide 38): For which values of $t$ is the set $\mathbf{x}_1=(1,2,1)$, $\mathbf{x}_2=(2,1,3)$, $\mathbf{x}_3=(1,-4,t)$ linearly independent? For the other value, write $\mathbf{x}_3$ as a combination of $\mathbf{x}_1,\mathbf{x}_2$.
> Set up $\alpha_1\mathbf{x}_1+\alpha_2\mathbf{x}_2+\alpha_3\mathbf{x}_3=\mathbf{0}$. The vectors are the columns of the coefficient matrix:
> $$\begin{bmatrix}1&2&1\\2&1&-4\\1&3&t\end{bmatrix}\begin{bmatrix}\alpha_1\\\alpha_2\\\alpha_3\end{bmatrix}=\mathbf{0}$$
> Row reduce. $R_2\leftarrow R_2-2R_1$ and $R_3\leftarrow R_3-R_1$, then $R_3\leftarrow R_3+\tfrac13R_2$:
> $$\begin{bmatrix}1&2&1\\0&-3&-6\\0&1&t-1\end{bmatrix}\to\begin{bmatrix}1&2&1\\0&-3&-6\\0&0&t-3\end{bmatrix}$$
> If $t\neq3$ there are three pivots. Then $\alpha_3=0$, $\alpha_2=0$, $\alpha_1=0$ is the only solution: independent.
> If $t=3$ the third column has no pivot, so $\alpha_3$ is free: dependent. Row 2: $\alpha_2=-2\alpha_3$. Row 1: $\alpha_1=-2\alpha_2-\alpha_3=3\alpha_3$. With $\alpha_3=1$: $3\mathbf{x}_1-2\mathbf{x}_2+\mathbf{x}_3=\mathbf{0}$, so $\mathbf{x}_3=-3\mathbf{x}_1+2\mathbf{x}_2$.
> Check: $-3(1,2,1)+2(2,1,3)=(1,-4,3)$.

## 2. Dimension, basis, representation (slides 39-40)
![[ee502_eee501alllecturenotesabo_p039.jpg]]
![[ee502_eee501alllecturenotesabo_p040.jpg]]

**Notes.** **Dimension**: the number of vectors in a maximal linearly independent set. $\dim\mathbb{R}^n=n$, $\dim S_1=1$.

**Basis** of $V$: a set that is (i) linearly independent and (ii) spans $V$. The natural basis of $\mathbb{R}^n$ is $\{\mathbf{e}_1,\dots,\mathbf{e}_n\}$, where $\mathbf{e}_i$ has a 1 in place $i$ and zeros elsewhere. Every basis of an $m$-dimensional subspace has exactly $m$ vectors, and any $m$ independent vectors in it form a basis.

**Representation.** Let $\{\mathbf{q}_1,\dots,\mathbf{q}_m\}$ be a basis of $S\subseteq\mathbb{R}^n$ and $Q=[\mathbf{q}_1\ \cdots\ \mathbf{q}_m]$ ($n\times m$). Every $\mathbf{x}\in S$ is $\mathbf{x}=Q\tilde{\mathbf{x}}$ with a unique $\tilde{\mathbf{x}}=[\alpha_1\ \cdots\ \alpha_m]^{\mathsf T}$, the representation of $\mathbf{x}$ in that basis. If $Q$ is square and invertible, $\tilde{\mathbf{x}}=Q^{-1}\mathbf{x}$. In the natural basis $\tilde{\mathbf{x}}=\mathbf{x}$.

**Slide example.** $\mathbf{q}_1=[1\ \ 3]^{\mathsf T}$, $\mathbf{q}_2=[2\ \ 2]^{\mathsf T}$, $\mathbf{x}=[4\ \ 1]^{\mathsf T}$. $\det Q=2-6=-4\neq0$, so it is a basis. Solve $\alpha_1+2\alpha_2=4$, $3\alpha_1+2\alpha_2=1$: $\alpha_2=\frac{11}{4}$, $\alpha_1=-\frac32$.

> [!warning] Watch out
> The slide lists the representation as $[11/4\ \ -3/2]^{\mathsf T}$. That is the order $\{\mathbf{q}_2,\mathbf{q}_1\}$. With $\mathbf{q}_1=[1\ \ 3]^{\mathsf T}$ first, as stated, it is $\tilde{\mathbf{x}}=[-3/2\ \ 11/4]^{\mathsf T}$. The order of the basis vectors fixes the order of the coordinates.

> [!info] Change of basis (beyond the slides)
> Let $Q$ and $P$ be two square invertible matrices whose columns are two bases of $\mathbb{R}^n$. The same vector has two representations: $\mathbf{x}=Q\tilde{\mathbf{x}}$ and $\mathbf{x}=P\bar{\mathbf{x}}$.
> Set them equal: $P\bar{\mathbf{x}}=Q\tilde{\mathbf{x}}$, so $\bar{\mathbf{x}}=P^{-1}Q\,\tilde{\mathbf{x}}$.
> The matrix $P^{-1}Q$ is the **change-of-basis matrix** from the $Q$-coordinates to the $P$-coordinates. Its column $i$ is the representation of $\mathbf{q}_i$ in the basis $P$.
> The vector itself does not change. Only its list of coordinates changes. Lecture 4 uses the same idea for matrices (similarity transformation).

> [!question]- Check (slide 39): $S=\{\mathbf{x}\in\mathbb{R}^4: x_1=x_2,\ x_3=2x_4\}$. Find a basis and the dimension of $S$. Is $\{(1,1,0,0),\ (0,0,2,1),\ (1,1,2,1)\}$ also a basis of $S$?
> Two entries are free. Write $x_2=a$ and $x_4=b$. Then $\mathbf{x}=(a,a,2b,b)=a(1,1,0,0)+b(0,0,2,1)$.
> So $\mathbf{b}_1=(1,1,0,0)$ and $\mathbf{b}_2=(0,0,2,1)$ span $S$. They are independent: $a\mathbf{b}_1+b\mathbf{b}_2=(a,a,2b,b)=\mathbf{0}$ forces $a=0$ and $b=0$.
> Both conditions of the slide hold, so $\{\mathbf{b}_1,\mathbf{b}_2\}$ is a basis and $\dim S=2$.
> The set of three vectors is not a basis. It spans $S$, but $(1,1,2,1)=\mathbf{b}_1+\mathbf{b}_2$, so it is dependent. Every basis of $S$ has exactly 2 vectors.

> [!question]- Check (slide 40): $\mathbf{q}_1=(1,1)$, $\mathbf{q}_2=(1,2)$ and $\mathbf{x}=(3,5)$. (a) Find the representation $\tilde{\mathbf{x}}$ with $Q^{-1}$. (b) Find the representation $\bar{\mathbf{x}}$ of the same $\mathbf{x}$ in the basis $\mathbf{p}_1=(1,0)$, $\mathbf{p}_2=(1,1)$, and the matrix that maps $\tilde{\mathbf{x}}$ to $\bar{\mathbf{x}}$.
> (a) $Q=\begin{bmatrix}1&1\\1&2\end{bmatrix}$, $\det Q=2-1=1\neq0$, so it is a basis.
> $$Q^{-1}=\begin{bmatrix}2&-1\\-1&1\end{bmatrix},\qquad \tilde{\mathbf{x}}=Q^{-1}\mathbf{x}=\begin{bmatrix}2\cdot3-5\\-3+5\end{bmatrix}=\begin{bmatrix}1\\2\end{bmatrix}$$
> Check: $1\,(1,1)+2\,(1,2)=(3,5)$.
> (b) $P=\begin{bmatrix}1&1\\0&1\end{bmatrix}$, $P^{-1}=\begin{bmatrix}1&-1\\0&1\end{bmatrix}$, so $\bar{\mathbf{x}}=P^{-1}\mathbf{x}=(3-5,\ 5)=(-2,5)$. Check: $-2\,(1,0)+5\,(1,1)=(3,5)$.
> The map is $\bar{\mathbf{x}}=P^{-1}Q\,\tilde{\mathbf{x}}$ with
> $$P^{-1}Q=\begin{bmatrix}1&-1\\0&1\end{bmatrix}\begin{bmatrix}1&1\\1&2\end{bmatrix}=\begin{bmatrix}0&-1\\1&2\end{bmatrix},\qquad \begin{bmatrix}0&-1\\1&2\end{bmatrix}\begin{bmatrix}1\\2\end{bmatrix}=\begin{bmatrix}-2\\5\end{bmatrix}$$

## 3. Norms (slide 41)
![[ee502_eee501alllecturenotesabo_p041.jpg]]

**Notes.** A **norm** $\lVert\cdot\rVert$ is a nonnegative real function on $V$ with: $\lVert\mathbf{x}\rVert=0$ exactly when $\mathbf{x}=\mathbf{0}$, $\lVert\alpha\mathbf{x}\rVert=|\alpha|\lVert\mathbf{x}\rVert$, and the triangle inequality $\lVert\mathbf{x}_1+\mathbf{x}_2\rVert\le\lVert\mathbf{x}_1\rVert+\lVert\mathbf{x}_2\rVert$.

$$\lVert\mathbf{x}\rVert_1=\sum_{i=1}^n|x_i|,\qquad \lVert\mathbf{x}\rVert_2=\sqrt{\mathbf{x}^{\mathsf T}\mathbf{x}}=\sqrt{\sum_{i=1}^n x_i^2},\qquad \lVert\mathbf{x}\rVert_\infty=\max_i|x_i|$$

$\lVert\mathbf{x}\rVert_2$ is the Euclidean length. Useful facts: $|\mathbf{x}^{\mathsf T}\mathbf{y}|\le\lVert\mathbf{x}\rVert_2\lVert\mathbf{y}\rVert_2$ (Cauchy-Schwarz), and $\lVert\mathbf{x}\rVert_\infty\le\lVert\mathbf{x}\rVert_2\le\lVert\mathbf{x}\rVert_1\le n\lVert\mathbf{x}\rVert_\infty$.

> [!example] One vector, three norms
> $\mathbf{x}=[3\ \ -4\ \ 12]^{\mathsf T}$: $\lVert\mathbf{x}\rVert_1=19$, $\lVert\mathbf{x}\rVert_2=\sqrt{169}=13$, $\lVert\mathbf{x}\rVert_\infty=12$. Chain: $12\le13\le19\le36$.

> [!question]- Check (slide 41): Find the mistake. "$f(\mathbf{x})=\lvert x_1-x_2\rvert$ is a norm on $\mathbb{R}^2$, because it is nonnegative, $f(\alpha\mathbf{x})=\lvert\alpha\rvert f(\mathbf{x})$, and it satisfies the triangle inequality." Then compute $\lVert-2\mathbf{x}\rVert_1$ for $\mathbf{x}=(1,-3,2)$ in two ways.
> The three properties in the sentence are true for $f$. The missing one is the second half of the first condition on the slide: $\lVert\mathbf{x}\rVert=0$ if and only if $\mathbf{x}=\mathbf{0}$.
> Counterexample: $\mathbf{x}=(1,1)$ is not the zero vector, but $f(\mathbf{x})=\lvert1-1\rvert=0$. So $f$ is not a norm. A norm gives length zero only to $\mathbf{0}$.
> Computation, direct: $-2\mathbf{x}=(-2,6,-4)$, so $\lVert-2\mathbf{x}\rVert_1=2+6+4=12$.
> With the scaling property: $\lVert\mathbf{x}\rVert_1=1+3+2=6$ and $\lvert-2\rvert\cdot6=12$. Same result.

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

> [!question]- Check (slide 42): Show with one line of algebra that $\mathbf{q}_2=\mathbf{v}_2-(\mathbf{u}_1^{\mathsf T}\mathbf{v}_2)\mathbf{u}_1$ is orthogonal to $\mathbf{u}_1$. Which property of $\mathbf{u}_1$ do you need? What goes wrong if you use $\mathbf{v}_1$ in place of $\mathbf{u}_1$ in this formula?
> Multiply from the left by $\mathbf{u}_1^{\mathsf T}$. The number $\mathbf{u}_1^{\mathsf T}\mathbf{v}_2$ is a scalar, so it moves out:
> $$\mathbf{u}_1^{\mathsf T}\mathbf{q}_2=\mathbf{u}_1^{\mathsf T}\mathbf{v}_2-(\mathbf{u}_1^{\mathsf T}\mathbf{v}_2)(\mathbf{u}_1^{\mathsf T}\mathbf{u}_1)=\mathbf{u}_1^{\mathsf T}\mathbf{v}_2-\mathbf{u}_1^{\mathsf T}\mathbf{v}_2=0$$
> The step needs $\mathbf{u}_1^{\mathsf T}\mathbf{u}_1=\lVert\mathbf{u}_1\rVert_2^2=1$: $\mathbf{u}_1$ is normalized.
> With $\mathbf{v}_1$ the same product gives $\mathbf{v}_1^{\mathsf T}\mathbf{v}_2\,(1-\lVert\mathbf{v}_1\rVert_2^2)$. This is not zero unless $\lVert\mathbf{v}_1\rVert_2=1$ or $\mathbf{v}_1^{\mathsf T}\mathbf{v}_2=0$. The result is then not orthogonal to $\mathbf{v}_1$.

> [!question]- Check (slide 43): Apply Gram-Schmidt to $\mathbf{v}_1=(1,1,0)$, $\mathbf{v}_2=(1,0,1)$, $\mathbf{v}_3=(0,1,1)$.
> Step 1: $\mathbf{q}_1=\mathbf{v}_1$, $\lVert\mathbf{q}_1\rVert=\sqrt2$, $\mathbf{u}_1=\frac{1}{\sqrt2}(1,1,0)$.
> Step 2: $\mathbf{u}_1^{\mathsf T}\mathbf{v}_2=\frac{1}{\sqrt2}$, so the projection is $\frac{1}{\sqrt2}\mathbf{u}_1=(\frac12,\frac12,0)$.
> $\mathbf{q}_2=(1,0,1)-(\frac12,\frac12,0)=(\frac12,-\frac12,1)$, $\lVert\mathbf{q}_2\rVert=\sqrt{\frac14+\frac14+1}=\sqrt{\frac32}$, $\mathbf{u}_2=\frac{1}{\sqrt6}(1,-1,2)$.
> Step 3: $\mathbf{u}_1^{\mathsf T}\mathbf{v}_3=\frac{1}{\sqrt2}$ and $\mathbf{u}_2^{\mathsf T}\mathbf{v}_3=\frac{-1+2}{\sqrt6}=\frac{1}{\sqrt6}$. The two projections are $(\frac12,\frac12,0)$ and $\frac16(1,-1,2)=(\frac16,-\frac16,\frac13)$.
> $\mathbf{q}_3=(0,1,1)-(\frac12,\frac12,0)-(\frac16,-\frac16,\frac13)=(-\frac23,\frac23,\frac23)$, $\lVert\mathbf{q}_3\rVert=\sqrt{\frac{12}{9}}=\frac{2}{\sqrt3}$, $\mathbf{u}_3=\frac{1}{\sqrt3}(-1,1,1)$.
> Check: $\mathbf{u}_1^{\mathsf T}\mathbf{u}_2=\frac{1-1}{\sqrt{12}}=0$, $\mathbf{u}_1^{\mathsf T}\mathbf{u}_3=\frac{-1+1}{\sqrt6}=0$, $\mathbf{u}_2^{\mathsf T}\mathbf{u}_3=\frac{-1-1+2}{\sqrt{18}}=0$.

## 5. Row echelon form (slide 44)
![[ee502_eee501alllecturenotesabo_p044.jpg]]

**Notes.** Elementary row operations: swap two rows, multiply a row by a nonzero constant, add a multiple of one row to another. The **row echelon form** $R$ of $A\in\mathbb{R}^{m\times n}$ has all zero rows at the bottom, and each pivot (first nonzero entry of a row) lies to the right of the pivot above. In the **reduced** form $\tilde R$ every pivot is 1 and is the only nonzero entry in its column. The reduced form is unique.

Each row operation is a left multiplication by an invertible matrix, so $TA=R$ for some invertible $T\in\mathbb{R}^{m\times m}$.

**Slide example.**

$$A=\begin{bmatrix}0&1&1&-3&2\\1&1&2&-2&3\\1&1&2&-2&3\end{bmatrix}\to\begin{bmatrix}1&1&2&-2&3\\0&1&1&-3&2\\0&0&0&0&0\end{bmatrix}\to\tilde R=\begin{bmatrix}1&0&1&1&1\\0&1&1&-3&2\\0&0&0&0&0\end{bmatrix}$$

Steps: $R_1\leftrightarrow R_2$, $R_3\leftarrow R_3-R_1$ (row echelon form), then $R_1\leftarrow R_1-R_2$ (reduced). Here $\tilde T=\begin{bmatrix}-1&1&0\\1&0&0\\0&-1&1\end{bmatrix}$.

Row operations keep column relations: $A\boldsymbol{\alpha}=\mathbf{0}$ exactly when $R\boldsymbol{\alpha}=\mathbf{0}$. In the example, column 3 = column 1 + column 2 in $\tilde R$ and in $A$.

> [!info] How to find $T$ (beyond the slides)
> The slide says only that $T$ exists. To compute it, do the same row operations on the identity matrix $I_m$. In practice, row reduce the block matrix $[A\ \ I_m]$. When the left block has become $R$, the right block is $T$, because every step multiplies both blocks from the left by the same matrix: $T[A\ \ I_m]=[TA\ \ T]=[R\ \ T]$.
> $T$ is invertible because each row operation can be undone by another row operation.
> For the slide example: $I_3$ after $R_1\leftrightarrow R_2$, then $R_3\leftarrow R_3-R_1$, then $R_1\leftarrow R_1-R_2$ becomes the $\tilde T$ given above.

> [!question]- Check (slide 44): $A$ has the rows $(1,2,1)$, $(2,4,3)$, $(1,2,2)$. Find a row echelon form, the reduced row echelon form $\tilde R$, and a matrix $\tilde T$ with $\tilde TA=\tilde R$.
> $A=\begin{bmatrix}1&2&1\\2&4&3\\1&2&2\end{bmatrix}$. Row reduce $[A\ \ I_3]$. $R_2\leftarrow R_2-2R_1$ and $R_3\leftarrow R_3-R_1$:
> $$\left[\begin{array}{ccc|ccc}1&2&1&1&0&0\\0&0&1&-2&1&0\\0&0&1&-1&0&1\end{array}\right]$$
> $R_3\leftarrow R_3-R_2$ gives a row echelon form (pivots in columns 1 and 3, zero row at the bottom):
> $$\left[\begin{array}{ccc|ccc}1&2&1&1&0&0\\0&0&1&-2&1&0\\0&0&0&1&-1&1\end{array}\right]$$
> $R_1\leftarrow R_1-R_2$ clears the entry above the second pivot:
> $$\tilde R=\begin{bmatrix}1&2&0\\0&0&1\\0&0&0\end{bmatrix},\qquad \tilde T=\begin{bmatrix}3&-1&0\\-2&1&0\\1&-1&1\end{bmatrix}$$
> Check of row 1 of $\tilde TA$: $3(1,2,1)-(2,4,3)=(1,2,0)$. Row 3: $(1,2,1)-(2,4,3)+(1,2,2)=(0,0,0)$.

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

> [!info] The two "Why?" of slides 45-46 (beyond the slides)
> **Why are the basic columns independent?** Take only the first $r$ columns of (1): $\tilde T\hat A_1=\begin{bmatrix}I_r\\0\end{bmatrix}$. Suppose $\hat A_1\mathbf{c}=\mathbf{0}$. Multiply by $\tilde T$: $\begin{bmatrix}I_r\\0\end{bmatrix}\mathbf{c}=\begin{bmatrix}\mathbf{c}\\\mathbf{0}\end{bmatrix}=\mathbf{0}$, so $\mathbf{c}=\mathbf{0}$. Only the zero combination of the basic columns gives $\mathbf{0}$.
>
> **Why do the columns of $P\begin{bmatrix}-B\\I_{n-r}\end{bmatrix}$ form a basis of $\mathcal{N}(\tilde R)$?** A permutation matrix is invertible, so every $\mathbf{x}\in\mathbb{R}^n$ is $\mathbf{x}=P\mathbf{y}$ with $\mathbf{y}=\begin{bmatrix}\mathbf{y}_1\\\mathbf{y}_2\end{bmatrix}$, $\mathbf{y}_1\in\mathbb{R}^r$ (pivot variables), $\mathbf{y}_2\in\mathbb{R}^{n-r}$ (free variables). Then
> $$\tilde R\mathbf{x}=\tilde RP\mathbf{y}=\begin{bmatrix}I_r&B\\0&0\end{bmatrix}\begin{bmatrix}\mathbf{y}_1\\\mathbf{y}_2\end{bmatrix}=\begin{bmatrix}\mathbf{y}_1+B\mathbf{y}_2\\\mathbf{0}\end{bmatrix}$$
> This is zero exactly when $\mathbf{y}_1=-B\mathbf{y}_2$, that is $\mathbf{x}=P\begin{bmatrix}-B\\I_{n-r}\end{bmatrix}\mathbf{y}_2$ with $\mathbf{y}_2$ free. So the $n-r$ columns span $\mathcal{N}(\tilde R)$. They are independent because of the block $I_{n-r}$ (the combination is zero only if $\mathbf{y}_2=\mathbf{0}$).
>
> **Why is $\mathcal{N}(\tilde R)=\mathcal{N}(A)$?** $\tilde R=\tilde TA$ with $\tilde T$ invertible. So $A\mathbf{x}=\mathbf{0}$ gives $\tilde R\mathbf{x}=\tilde T\mathbf{0}=\mathbf{0}$, and $\tilde R\mathbf{x}=\mathbf{0}$ gives $A\mathbf{x}=\tilde T^{-1}\mathbf{0}=\mathbf{0}$.

> [!question]- Check (slide 45): $A$ has the rows $(1,3,2)$ and $(2,6,5)$. Find $\tilde R$, the basic columns, a permutation $P$, and the blocks $B$, $\hat A_1$, $\hat A_2$ of equation (1). What are $\mathcal{R}(A)$ and $r(A)$?
> $A=\begin{bmatrix}1&3&2\\2&6&5\end{bmatrix}$. $R_2\leftarrow R_2-2R_1$ gives $\begin{bmatrix}1&3&2\\0&0&1\end{bmatrix}$. $R_1\leftarrow R_1-2R_2$ gives $\tilde R=\begin{bmatrix}1&3&0\\0&0&1\end{bmatrix}$.
> Pivots are in columns 1 and 3. The basic columns of $A$ are $\mathbf{a}_1=(1,2)$ and $\mathbf{a}_3=(2,5)$. So $r=2$.
> $P$ swaps columns 2 and 3 to bring the basic columns first:
> $$P=\begin{bmatrix}1&0&0\\0&0&1\\0&1&0\end{bmatrix},\qquad \tilde RP=\begin{bmatrix}1&0&3\\0&1&0\end{bmatrix}=\begin{bmatrix}I_2&B\end{bmatrix},\qquad B=\begin{bmatrix}3\\0\end{bmatrix}$$
> There is no zero row because $r=m=2$. $B$ is $r\times(n-r)=2\times1$.
> $AP=\begin{bmatrix}1&2&3\\2&5&6\end{bmatrix}$, so $\hat A_1=\begin{bmatrix}1&2\\2&5\end{bmatrix}$ and $\hat A_2=\begin{bmatrix}3\\6\end{bmatrix}$.
> $\mathcal{R}(A)=\operatorname{span}\{(1,2),(2,5)\}$. Two independent vectors in $\mathbb{R}^2$ span all of it, so $\mathcal{R}(A)=\mathbb{R}^2$ and $r(A)=2$.

> [!question]- Check (slide 46): Use the matrix of the slide 45 check. (a) Verify $\hat A_2=\hat A_1B$. (b) Find a basis of $\mathcal{N}(A)$ with the formula of the proof ($P$ times the block matrix with $-B$ on top of $I_{n-r}$) and verify rank-nullity. (c) Find the mistake: "A $4\times6$ matrix with rank 4 has nullity $4-4=0$."
> (a) $\hat A_1B=\begin{bmatrix}1&2\\2&5\end{bmatrix}\begin{bmatrix}3\\0\end{bmatrix}=\begin{bmatrix}3\\6\end{bmatrix}=\hat A_2$. In words: $\mathbf{a}_2=3\mathbf{a}_1+0\,\mathbf{a}_3$.
> (b) $n-r=3-2=1$, so the identity block is $1\times1$:
> $$\begin{bmatrix}-B\\I_1\end{bmatrix}=\begin{bmatrix}-3\\0\\1\end{bmatrix},\qquad P\begin{bmatrix}-3\\0\\1\end{bmatrix}=\begin{bmatrix}-3\\1\\0\end{bmatrix}$$
> $P$ puts the entries back in the original column order. Check: $A(-3,1,0)^{\mathsf T}=(-3+3,\ -6+6)=(0,0)$.
> Basis of $\mathcal{N}(A)$: $\{(-3,1,0)\}$, so $\nu(A)=1$ and $r(A)+\nu(A)=2+1=3=n$.
> (c) The $n$ in $r(A)+\nu(A)=n$ is the number of columns, not of rows. Here $n=6$, so $\nu(A)=6-4=2$. A matrix with more columns than rows always has a nonzero null vector, because $r\le m<n$.

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

> [!question]- 5. Rank, nullity and a null-space basis of the matrix $A$ with the rows $(1,2,3)$ and $(2,4,7)$
> $R_2\leftarrow R_2-2R_1$, $R_1\leftarrow R_1-3R_2$: $\tilde R=\begin{bmatrix}1&2&0\\0&0&1\end{bmatrix}$. Rank 2, nullity 1. $x_1=-2x_2$, $x_3=0$: basis $\{(-2,1,0)\}$.

> [!question]- 6. (Quiz style) $A$ has the rows $(1,2,0,1)$, $(2,4,1,4)$, $(3,6,1,5)$: RREF, rank, range and null bases.
> $\tilde R=\begin{bmatrix}1&2&0&1\\0&0&1&2\\0&0&0&0\end{bmatrix}$, pivots in columns 1 and 3, rank 2. Range basis: $(1,2,3)$, $(0,1,1)$. Null basis: $(-2,1,0,0)$, $(-1,0,-2,1)$. $B=\begin{bmatrix}2&1\\0&2\end{bmatrix}$, so $\mathbf{a}_2=2\mathbf{a}_1$, $\mathbf{a}_4=\mathbf{a}_1+2\mathbf{a}_3$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L02 - LTI models and linearization]]. Next: [[EE502 L04 - Equations, eigenvalues, diagonalization]]
- Used by Quiz 3 (12 Nov, no calculator, slides 36-64) and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_03_Vector_Spaces_Rank.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_03/EE502_Lecture_03_Vector_Spaces_Rank.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_03/EE502_Lecture_03_Vector_Spaces_Rank.pdf`
- Original slides (PDF, pp. 36-46): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L03 - Vector spaces, norms and rank - quiz]]

Slides not embedded: 36 (section title).
