---
course: EE 502 Linear System Theory
lecture: 4
title: Equations, eigenvalues, diagonalization
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 47-60)
full_notes: lecture_notes/lecture_04/EE502_Lecture_04_Equations_Eigenvalues.pdf
---
# EE 502 · Lecture 4 · Equations, eigenvalues, diagonalization

> [!summary] In short
> - $A\mathbf{x}=\mathbf{y}$ has a solution exactly when $\operatorname{rank}A=\operatorname{rank}[A\ \ \mathbf{y}]$. All solutions: one particular solution plus the null space.
> - $\det A=0$ exactly when the columns are dependent. $A^{-1}=\operatorname{adj}A/\det A$.
> - $\hat A=Q^{-1}AQ$ is the same map in another basis. Similar matrices share eigenvalues, determinant, trace and rank.
> - Eigenvalues are the roots of $\Delta(\lambda)=\det(\lambda I-A)$.
> - Distinct eigenvalues give $Q^{-1}AQ=\Lambda$. With a repeated eigenvalue, compare the nullity of $A-\lambda I$ with the multiplicity.

## 1. Existence of solutions of Ax = y (slides 47-48)
![[ee502_eee501alllecturenotesabo_p047.jpg]]
![[ee502_eee501alllecturenotesabo_p048.jpg]]

**Notes.** $A\mathbf{x}=\mathbf{y}$ (2), with $A\in\mathbb{R}^{m\times n}$: $m$ equations, $n$ unknowns. $A\mathbf{x}$ is a combination of the columns of $A$, so the question is whether $\mathbf{y}$ can be built from the columns.

**Theorem 1 (existence).**
1. A solution exists if and only if $\mathbf{y}\in\mathcal{R}(A)$, equivalently $r(A)=r([A\ \ \mathbf{y}])$.
2. A solution exists for every $\mathbf{y}\in\mathbb{R}^m$ if and only if $r(A)=m$.

In practice: row reduce $[A\ \ \mathbf{y}]$. A pivot in the last column means a row "$0=\text{nonzero}$": no solution.

> [!warning] Watch out
> - Slide 48, converse of (ii): it says "has a solution for **a** $\mathbf{y}$". The argument needs a solution for **every** $\mathbf{y}\in\mathbb{R}^m$. ($\mathbf{y}=\mathbf{0}$ is always solvable, whatever the rank.)
> - Part (ii) needs $n\ge m$. That is necessary, not sufficient: $\begin{bmatrix}1&2\\2&4\end{bmatrix}$ has rank 1.

> [!info] Full row rank and full column rank (beyond the slides)
> $A$ is $m\times n$ and $r(A)\le\min(m,n)$. Two extreme cases are worth knowing by name.
> - **Full row rank**, $r(A)=m$: the rows are independent. Every row of the echelon form has a pivot, so no row "$0=\text{nonzero}$" can appear. A solution exists for every $\mathbf{y}$. This is Theorem 1 (ii).
> - **Full column rank**, $r(A)=n$: the columns are independent, so $\nu(A)=n-r(A)=0$. A solution does not always exist, but when it exists it is the only one (Theorem 2 in the next section).
> - Square and nonsingular: both hold. Exactly one solution for every $\mathbf{y}$.

> [!question]- Check (slide 47): $A$ has the rows $(1,2,1)$, $(2,4,3)$, $(3,6,4)$. Is $A\mathbf{x}=\mathbf{y}$ solvable for $\mathbf{y}=(1,3,4)$? For $\mathbf{y}=(1,3,5)$? For every $\mathbf{y}\in\mathbb{R}^3$?
> Row 3 of $A$ is row 1 plus row 2, and rows 1 and 2 are not multiples of each other. So $r(A)=2$.
> $\mathbf{y}=(1,3,4)$: $R_3\leftarrow R_3-R_1-R_2$ gives $[0\ \ 0\ \ 0\ \mid\ 4-1-3]=[0\ \ 0\ \ 0\ \mid\ 0]$. So $r([A\ \ \mathbf{y}])=2=r(A)$: **solvable**.
> $\mathbf{y}=(1,3,5)$: the same step gives $[0\ \ 0\ \ 0\ \mid\ 5-1-3]=[0\ \ 0\ \ 0\ \mid\ 1]$. This is a pivot in the last column, so $r([A\ \ \mathbf{y}])=3\neq2$: **no solution**.
> Every $\mathbf{y}$: this needs $r(A)=m=3$. Here $r(A)=2$, so **no**.

> [!question]- Check (slide 48): $A$ is $3\times2$ with the rows $(1,0)$, $(0,1)$, $(1,1)$. Count pivots as in the proof: is there a solution for $\mathbf{y}=(1,1,0)$? For $\mathbf{y}=(1,1,2)$? Can $A\mathbf{x}=\mathbf{y}$ be solvable for every $\mathbf{y}$?
> $A$ has 2 pivots (columns 1 and 2), so $r(A)=2$. There are $m=3$ rows, so $r(A)<m$ and part (ii) says: **not solvable for every** $\mathbf{y}$.
> $\mathbf{y}=(1,1,0)$: $R_3\leftarrow R_3-R_1-R_2$ gives $[0\ \ 0\ \mid\ 0-1-1]=[0\ \ 0\ \mid\ -2]$. The last column gets a pivot, $r([A\ \ \mathbf{y}])=3$: **no solution**.
> $\mathbf{y}=(1,1,2)$: the same step gives $[0\ \ 0\ \mid\ 2-1-1]=[0\ \ 0\ \mid\ 0]$. Rank 2 on both sides: **solvable**, with $x_1=1$, $x_2=1$.
> $A$ has full column rank, so this solution is the only one.

## 2. The set of all solutions (slides 49-51)
![[ee502_eee501alllecturenotesabo_p049.jpg]]
![[ee502_eee501alllecturenotesabo_p050.jpg]]
![[ee502_eee501alllecturenotesabo_p051.jpg]]

**Notes.** **Theorem 2.** Let $\mathbf{x}_p$ be one particular solution and $\nu=\nu(A)=n-r(A)$ the nullity. If $\nu=0$, $\mathbf{x}_p$ is the unique solution. If $\nu>0$ and $\{\mathbf{n}_1,\dots,\mathbf{n}_\nu\}$ is a basis of $\mathcal{N}(A)$, all solutions are

$$\mathbf{x}=\mathbf{x}_p+\alpha_1\mathbf{n}_1+\cdots+\alpha_\nu\mathbf{n}_\nu\qquad(4)$$

**Recipe.** Row reduce $[A\ \ \mathbf{y}]$ to reduced form. Unknowns of pivot columns are basic, the others are free. Solve each nonzero row for its pivot unknown, then split $\mathbf{x}$ into a constant part ($\mathbf{x}_p$) and one vector per free unknown.

**Slide example.**

$$[A\ \ \mathbf{y}]=\begin{bmatrix}0&0&1&-3&2\\1&1&2&-2&3\\1&1&2&-2&3\end{bmatrix}\to\begin{bmatrix}1&1&0&4&-1\\0&0&1&-3&2\\0&0&0&0&0\end{bmatrix}$$

Steps: $R_1\leftrightarrow R_2$, $R_3\leftarrow R_3-R_1$, $R_1\leftarrow R_1-2R_2$. Rows: $x_1=-1-x_2-4x_4$, $x_3=2+3x_4$. Free: $x_2$, $x_4$.

$$\mathbf{x}=\underbrace{\begin{bmatrix}-1\\0\\2\\0\end{bmatrix}}_{\mathbf{x}_p}+x_2\underbrace{\begin{bmatrix}-1\\1\\0\\0\end{bmatrix}}_{\mathbf{n}_1}+x_4\underbrace{\begin{bmatrix}-4\\0\\3\\1\end{bmatrix}}_{\mathbf{n}_2}$$

The slide does the same with the permutation $P$ (swap columns 2 and 3) and $B=\begin{bmatrix}1&4\\0&-3\end{bmatrix}$. The two columns of $P\begin{bmatrix}-B\\ I\end{bmatrix}$ are $\mathbf{n}_1,\mathbf{n}_2$.

> [!warning] Watch out
> - Slide 49 writes $\alpha_1,\dots,\alpha_n$. There are only $\nu$ coefficients.
> - Slide 50: "reduced column echelon form" should be "reduced row echelon form", and the identity block is $I_{n-r}$.

> [!question]- Check (slide 49): $A$ has the rows $(1,1,1)$, $(1,2,3)$ and $\mathbf{y}=(6,14)$. Both $\mathbf{x}_a=(1,2,3)$ and $\mathbf{x}_b=(3,-2,5)$ solve $A\mathbf{x}=\mathbf{y}$. How many free parameters does the solution set have? Write all solutions and find the $\alpha$ that gives $\mathbf{x}_b$.
> The rows are not multiples of each other, so $r(A)=2$ and $\nu(A)=n-r(A)=3-2=1$: **one** free parameter.
> Null space: $x_1+x_2+x_3=0$ and $x_1+2x_2+3x_3=0$. Subtract: $x_2+2x_3=0$, so $x_2=-2x_3$. Then $x_1=-x_2-x_3=x_3$. With $x_3=1$: $\mathbf{n}_1=(1,-2,1)$.
> All solutions, with $\mathbf{x}_p=\mathbf{x}_a$: $\mathbf{x}=(1,2,3)+\alpha(1,-2,1)$.
> $\mathbf{x}_b-\mathbf{x}_a=(2,-4,2)=2\,\mathbf{n}_1$, so $\alpha=2$. This is the proof of the slide: the difference of two solutions is in $\mathcal{N}(A)$.

> [!question]- Check (slide 50): $[A\ \ \mathbf{y}]$ has the rows $(1,2,1,3\mid4)$, $(2,4,3,8\mid9)$, $(1,2,2,5\mid5)$. Bring it to reduced row echelon form. Give $r(A)$, the pivot columns, the basic and free unknowns and the block $B$. Is the system solvable?
> $R_2\leftarrow R_2-2R_1$: $(0,0,1,2\mid1)$. $R_3\leftarrow R_3-R_1$: $(0,0,1,2\mid1)$. $R_3\leftarrow R_3-R_2$: $(0,0,0,0\mid0)$. $R_1\leftarrow R_1-R_2$: $(1,2,0,1\mid3)$.
> $$[\tilde R\ \ \tilde{\mathbf{y}}]=\begin{bmatrix}1&2&0&1&3\\0&0&1&2&1\\0&0&0&0&0\end{bmatrix}$$
> Pivot columns: 1 and 3, so $r(A)=2$. Basic unknowns: $x_1,x_3$. Free unknowns: $x_2,x_4$.
> No pivot in the last column, so $r([A\ \ \mathbf{y}])=2=r(A)$: **solvable**.
> Swap columns 2 and 3 of $\tilde R$ (this is $P$): $\tilde RP=\begin{bmatrix}1&0&2&1\\0&1&0&2\\0&0&0&0\end{bmatrix}$, so $B=\begin{bmatrix}2&1\\0&2\end{bmatrix}$.

> [!question]- Check (slide 51): Continue with the system of the previous check. Write all solutions as $\mathbf{x}_p$ plus the null space, and show how $\mathbf{n}_1,\mathbf{n}_2$ come from $-B$.
> Rows of the reduced form: $x_1+2x_2+x_4=3$ and $x_3+2x_4=1$. So $x_1=3-2x_2-x_4$ and $x_3=1-2x_4$.
> $$\mathbf{x}=\underbrace{\begin{bmatrix}3\\0\\1\\0\end{bmatrix}}_{\mathbf{x}_p}+x_2\underbrace{\begin{bmatrix}-2\\1\\0\\0\end{bmatrix}}_{\mathbf{n}_1}+x_4\underbrace{\begin{bmatrix}-1\\0\\-2\\1\end{bmatrix}}_{\mathbf{n}_2}$$
> From $-B$: in the order $(x_1,x_3,x_2,x_4)$ the block $\begin{bmatrix}-B\\ I\end{bmatrix}$ has the columns $(-2,0,1,0)$ and $(-1,-2,0,1)$. $P$ swaps entries 2 and 3 back: $(-2,1,0,0)$ and $(-1,0,-2,1)$. These are $\mathbf{n}_1,\mathbf{n}_2$.
> Check with the first row of $A$, $(1,2,1,3)$: $\mathbf{x}_p$ gives $3+1=4$, $\mathbf{n}_1$ gives $-2+2=0$, $\mathbf{n}_2$ gives $-1-2+3=0$.

## 3. Determinants and inverses (slides 52-53)
![[ee502_eee501alllecturenotesabo_p052.jpg]]
![[ee502_eee501alllecturenotesabo_p053.jpg]]

**Notes.** Laplace's formula, for any fixed column $j$:

$$\det A=\sum_{i=1}^n a_{ij}c_{ij},\qquad c_{ij}=(-1)^{i+j}\det M_{ij}$$

$M_{ij}$ is the matrix $A$ without row $i$ and column $j$, $c_{ij}$ is the cofactor. For $2\times2$: $ad-bc$. Triangular matrix: product of the diagonal entries. $\det(AB)=\det A\det B$.

**Fact.** $\det A=0$ iff the rows are dependent iff the columns are dependent iff $\nu(A)>0$.

**Inverse** (when $\det A\neq0$): $A^{-1}=\dfrac{1}{\det A}[c_{ij}]^{\mathsf T}$, where $\operatorname{adj}A=[c_{ij}]^{\mathsf T}$ is the adjoint. Properties: $A^{-1}A=AA^{-1}=I_n$ and $(\operatorname{adj}A)A=A(\operatorname{adj}A)=(\det A)I_n$.

$$\begin{bmatrix}a&b\\c&d\end{bmatrix}^{-1}=\frac{1}{ad-bc}\begin{bmatrix}d&-b\\-c&a\end{bmatrix}$$

**Fact.** The inverse of a nonsingular triangular matrix is triangular of the same kind, with diagonal entries $1/a_{ii}$.

> [!warning] Watch out
> Slide errors found by our notes:
> - Slide 52 says "$\det A=0$ iff ... columns of $A$ are linearly **independent**". It must be **dependent**.
> - $M_{ij}$ is the matrix, not its determinant. The triangular product rule is a consequence of Laplace's formula, not a definition.
> - Slide 53 proof: the correct ranges are $b_{nj}=0$ for $j=1,\dots,n-1$ and $b_{(n-1)j}=0$ for $j=1,\dots,n-2$.
> - $\det(A+B)\neq\det A+\det B$, and $\det(cA)=c^n\det A$.

> [!question]- Check (slide 52): $A$ has the rows $(2,0,1)$, $(1,3,0)$, $(0,1,4)$. Compute $\det A$ with Laplace's formula along column 2. Are the columns of $A$ linearly independent?
> Column 2 is $(a_{12},a_{22},a_{32})=(0,3,1)$, so $\det A=0\cdot c_{12}+3c_{22}+1\cdot c_{32}$.
> $c_{22}=(-1)^{2+2}\det\begin{bmatrix}2&1\\0&4\end{bmatrix}=8-0=8$.
> $c_{32}=(-1)^{3+2}\det\begin{bmatrix}2&1\\1&0\end{bmatrix}=-(0-1)=1$.
> $\det A=3\cdot8+1\cdot1=25$.
> $\det A\neq0$, so the columns are **independent** (and $\nu(A)=0$).

> [!question]- Check (slide 53): $A$ is upper triangular with the rows $(2,1,0)$, $(0,1,3)$, $(0,0,4)$. Compute $A^{-1}$ with the adjoint. Which two things does the Fact above (slide 53 and Notes) predict about the result?
> $\det A=2\cdot1\cdot4=8$.
> Cofactors: $c_{11}=1\cdot4-3\cdot0=4$, $c_{12}=-(0\cdot4-3\cdot0)=0$, $c_{13}=0$.
> $c_{21}=-(1\cdot4-0\cdot0)=-4$, $c_{22}=2\cdot4-0=8$, $c_{23}=-(2\cdot0-1\cdot0)=0$.
> $c_{31}=1\cdot3-0\cdot1=3$, $c_{32}=-(2\cdot3-0\cdot0)=-6$, $c_{33}=2\cdot1-1\cdot0=2$.
> $$\operatorname{adj}A=[c_{ij}]^{\mathsf T}=\begin{bmatrix}4&-4&3\\0&8&-6\\0&0&2\end{bmatrix},\qquad A^{-1}=\frac18\operatorname{adj}A=\begin{bmatrix}\tfrac12&-\tfrac12&\tfrac38\\0&1&-\tfrac34\\0&0&\tfrac14\end{bmatrix}$$
> Prediction: $A^{-1}$ is again **upper triangular**, and its diagonal is $1/a_{ii}$: $\tfrac12,\ 1,\ \tfrac14$. Both hold.

## 4. Similarity transformation and companion form (slides 54-55)
![[ee502_eee501alllecturenotesabo_p054.jpg]]
![[ee502_eee501alllecturenotesabo_p055.jpg]]

**Notes.** A matrix $A\in\mathbb{R}^{n\times n}$ defines the linear map $\mathbf{x}\mapsto A\mathbf{x}$. Column $i$ of $A$ is the image of $\mathbf{e}_i$, so $A$ is the representation of the map in the natural basis. In another basis $\{\mathbf{q}_1,\dots,\mathbf{q}_n\}$, with $Q=[\mathbf{q}_1\ \cdots\ \mathbf{q}_n]$, write $A\mathbf{q}_i=Q\hat{\mathbf{a}}_i$. Then

$$AQ=Q\hat A\quad\Longleftrightarrow\quad \hat A=Q^{-1}AQ\qquad(2)$$

$\hat A$ and $A$ are **similar**, $Q$ is a **similarity transformation**. Column $i$ of $\hat A$ says where $\mathbf{q}_i$ goes, written in the $\mathbf{q}$'s. Similar matrices have the same characteristic polynomial, eigenvalues, determinant, trace and rank.

**Companion form.** If $\{\mathbf{b},A\mathbf{b},\dots,A^{n-1}\mathbf{b}\}$ is independent, take $Q=[\mathbf{b}\ \ A\mathbf{b}\ \cdots\ A^{n-1}\mathbf{b}]$ and write $A^n\mathbf{b}=\beta_1\mathbf{b}+\beta_2A\mathbf{b}+\cdots+\beta_nA^{n-1}\mathbf{b}$. Then $AQ=QB$ with

$$B=\begin{bmatrix}0&0&\cdots&0&\beta_1\\1&0&\cdots&0&\beta_2\\0&1&\cdots&0&\beta_3\\ \vdots&\vdots&\ddots&\vdots&\vdots\\0&0&\cdots&1&\beta_n\end{bmatrix}$$

$B$ is the companion matrix of $s^n-\beta_ns^{n-1}-\cdots-\beta_2s-\beta_1$, which is the characteristic polynomial of $B$ and of $A$.

> [!warning] Watch out
> - Slide 55 prints the third row of $B$ as $[1\ \ 1\ \cdots\ 0\ \ \beta_3]$. The correct row is $[0\ \ 1\ \cdots\ 0\ \ \beta_3]$.
> - Similar implies same eigenvalues. The converse is false (the two examples of section 7).

> [!question]- Check (slide 54): $A$ has the rows $(0,1)$, $(-2,-3)$. The new basis is $\mathbf{q}_1=(1,0)$, $\mathbf{q}_2=(1,-1)$. Find $\hat A$ column by column from $A\mathbf{q}_i=Q\hat{\mathbf{a}}_i$, without computing $Q^{-1}$. Check trace and determinant.
> Column 1: $A\mathbf{q}_1=(0,-2)$. Write it as $\alpha_1\mathbf{q}_1+\alpha_2\mathbf{q}_2=(\alpha_1+\alpha_2,\ -\alpha_2)$. So $\alpha_2=2$ and $\alpha_1=-2$: $\hat{\mathbf{a}}_1=(-2,2)$.
> Column 2: $A\mathbf{q}_2=(0\cdot1+1\cdot(-1),\ -2\cdot1-3\cdot(-1))=(-1,1)=-\mathbf{q}_2$. So $\hat{\mathbf{a}}_2=(0,-1)$.
> $$\hat A=\begin{bmatrix}-2&0\\2&-1\end{bmatrix}$$
> Trace: $-2-1=-3=0-3$. Determinant: $(-2)(-1)-0=2=0\cdot(-3)-1\cdot(-2)$. Same as for $A$, as similar matrices must have.

> [!question]- Check (slide 55): $A$ has the rows $(1,2)$, $(3,4)$ and $\mathbf{b}=(1,0)$. Build $Q=[\mathbf{b}\ \ A\mathbf{b}]$, find $\beta_1,\beta_2$ and the companion matrix $B$. Which polynomial belongs to $B$?
> $A\mathbf{b}=(1,3)$. $\mathbf{b}$ and $A\mathbf{b}$ are independent, so $Q=\begin{bmatrix}1&1\\0&3\end{bmatrix}$ is nonsingular.
> $A^2\mathbf{b}=A(1,3)=(1+6,\ 3+12)=(7,15)$.
> Solve $\beta_1\mathbf{b}+\beta_2A\mathbf{b}=(\beta_1+\beta_2,\ 3\beta_2)=(7,15)$: $\beta_2=5$, $\beta_1=2$.
> $$B=\begin{bmatrix}0&\beta_1\\1&\beta_2\end{bmatrix}=\begin{bmatrix}0&2\\1&5\end{bmatrix}$$
> Polynomial: $s^2-\beta_2s-\beta_1=s^2-5s-2$. Check with $A$: $\Delta(s)=s^2-(\operatorname{tr}A)s+\det A=s^2-5s-2$. The same.

## 5. Eigenvalues and eigenvectors (slide 56)
![[ee502_eee501alllecturenotesabo_p056.jpg]]

**Notes.** $\lambda\in\mathbb{C}$ is an **eigenvalue** of $A$ if there is a nonzero $\mathbf{x}\in\mathbb{C}^n$ (an **eigenvector**) with $(A-\lambda I_n)\mathbf{x}=\mathbf{0}$. The **characteristic polynomial** is

$$\Delta(\lambda)=\det(\lambda I_n-A)=\lambda^n+\alpha_1\lambda^{n-1}+\cdots+\alpha_n$$

It has $n$ roots counting multiplicities, non-real roots come in conjugate pairs. $\mathcal{N}(A-\lambda_iI)\neq\{\mathbf{0}\}$ iff $\Delta(\lambda_i)=0$, so the eigenvalues are the roots of $\Delta$.

By hand: compute $\Delta$, find the roots, then row reduce $A-\lambda_iI$ for each root. Checks: $\sum\lambda_i=\operatorname{tr}A$, $\prod\lambda_i=\det A$. For $2\times2$: $\Delta=\lambda^2-(\operatorname{tr}A)\lambda+\det A$.

> [!warning] Watch out
> Eigenvectors are never unique (any nonzero multiple works). A repeated root does not guarantee as many independent eigenvectors as its multiplicity.

> [!question]- Check (slide 56): $A$ has the rows $(1,2,0)$, $(4,3,0)$, $(1,0,2)$. Find $\Delta(\lambda)$, the eigenvalues and one eigenvector for each. Check with trace and determinant.
> $$\Delta(\lambda)=\det\begin{bmatrix}\lambda-1&-2&0\\-4&\lambda-3&0\\-1&0&\lambda-2\end{bmatrix}$$
> Expand along column 3 (only the entry $\lambda-2$ is nonzero): $\Delta=(\lambda-2)[(\lambda-1)(\lambda-3)-8]=(\lambda-2)(\lambda^2-4\lambda-5)=(\lambda-2)(\lambda-5)(\lambda+1)$.
> Eigenvalues: $2,\ 5,\ -1$.
> $\lambda=2$: $A-2I$ has the rows $(-1,2,0)$, $(4,1,0)$, $(1,0,0)$. Row 3: $x_1=0$. Row 1: $x_2=0$. $x_3$ is free: $\mathbf{q}=(0,0,1)$.
> $\lambda=5$: $A-5I$ has the rows $(-4,2,0)$, $(4,-2,0)$, $(1,0,-3)$. $x_2=2x_1$ and $x_1=3x_3$. With $x_3=1$: $\mathbf{q}=(3,6,1)$.
> $\lambda=-1$: $A+I$ has the rows $(2,2,0)$, $(4,4,0)$, $(1,0,3)$. $x_2=-x_1$ and $x_1=-3x_3$. With $x_3=1$: $\mathbf{q}=(-3,3,1)$.
> Checks: $2+5-1=6=\operatorname{tr}A=1+3+2$. $2\cdot5\cdot(-1)=-10=\det A=2(1\cdot3-2\cdot4)$.

## 6. Diagonalization, distinct eigenvalues (slides 57-58)
![[ee502_eee501alllecturenotesabo_p057.jpg]]
![[ee502_eee501alllecturenotesabo_p058.jpg]]

**Notes.** **Case 1.** If the eigenvalues are distinct, the eigenvectors $\mathbf{q}_1,\dots,\mathbf{q}_n$ are linearly independent. Proof idea: suppose $\sum_i\alpha_i\mathbf{q}_i=\mathbf{0}$ and apply $\prod_{j\neq k}(A-\lambda_jI)$. Every term dies except the $k$-th, leaving $\prod_{j\neq k}(\lambda_k-\lambda_j)\,\alpha_k\mathbf{q}_k=\mathbf{0}$, so $\alpha_k=0$ for every $k$.

With $Q=[\mathbf{q}_1\ \cdots\ \mathbf{q}_n]$ and $\Lambda=\operatorname{diag}\{\lambda_1,\dots,\lambda_n\}$:

$$AQ=Q\Lambda\quad\Longrightarrow\quad Q^{-1}AQ=\Lambda$$

Keep the same order in $Q$ and $\Lambda$. Checking $AQ=Q\Lambda$ column by column is cheaper than computing $Q^{-1}$.

> [!example] Small case (ours)
> $A=\begin{bmatrix}4&1\\2&3\end{bmatrix}$: $\Delta=\lambda^2-7\lambda+10=(\lambda-2)(\lambda-5)$. $\mathbf{q}_1=(1,-2)$, $\mathbf{q}_2=(1,1)$. $Q=\begin{bmatrix}1&1\\-2&1\end{bmatrix}$, $\Lambda=\operatorname{diag}\{2,5\}$.

> [!warning] Watch out
> Distinct eigenvalues imply diagonalizable. The converse is false: $I_n$ is diagonal with all eigenvalues equal.

> [!info] Complex eigenvalues and the real (modal) form (beyond the slides)
> The slides allow $\lambda\in\mathbb{C}$, but show no complex example. For a real $A$ with a pair $\lambda=\sigma\pm i\omega$ ($\omega\neq0$):
> - The eigenvalues $\lambda$ and $\bar\lambda$ are distinct, so Case 1 applies. If $\mathbf{q}$ is an eigenvector for $\lambda$, then $\bar{\mathbf{q}}$ is one for $\bar\lambda$. $Q=[\mathbf{q}\ \ \bar{\mathbf{q}}]$ and $\Lambda=\operatorname{diag}\{\lambda,\bar\lambda\}$ are complex.
> - A real form: write $\mathbf{q}=\mathbf{u}+i\mathbf{v}$ with real $\mathbf{u},\mathbf{v}$. Then $A(\mathbf{u}+i\mathbf{v})=(\sigma+i\omega)(\mathbf{u}+i\mathbf{v})$. Compare real and imaginary parts: $A\mathbf{u}=\sigma\mathbf{u}-\omega\mathbf{v}$ and $A\mathbf{v}=\omega\mathbf{u}+\sigma\mathbf{v}$.
> - So with the real matrix $Q_r=[\mathbf{u}\ \ \mathbf{v}]=[\operatorname{Re}\mathbf{q}\ \ \operatorname{Im}\mathbf{q}]$:
>
> $$Q_r^{-1}AQ_r=\begin{bmatrix}\sigma&\omega\\-\omega&\sigma\end{bmatrix}$$
>
> This block is the **modal form**. It is not diagonal, but it is real: $\sigma$ sets the decay ($\sigma<0$) or growth ($\sigma>0$) and $\omega$ is the oscillation frequency.

> [!question]- Check (slide 57): Take $n=3$, eigenvalues $\lambda_1=1$, $\lambda_2=2$, $\lambda_3=4$ and $k=2$. Apply $(A-\lambda_1I)(A-\lambda_3I)$ to $\alpha_1\mathbf{q}_1+\alpha_2\mathbf{q}_2+\alpha_3\mathbf{q}_3=\mathbf{0}$. What remains, and what does it prove? Where does the argument fail if $\lambda_3=2$?
> Use $(A-\lambda_jI)\mathbf{q}_i=(\lambda_i-\lambda_j)\mathbf{q}_i$. The two factors commute, so each $\mathbf{q}_i$ can meet "its own" factor first.
> $\mathbf{q}_1$: the factor $(A-\lambda_1I)$ gives $(1-1)\mathbf{q}_1=\mathbf{0}$. $\mathbf{q}_3$: the factor $(A-\lambda_3I)$ gives $(4-4)\mathbf{q}_3=\mathbf{0}$.
> $\mathbf{q}_2$: $(\lambda_2-\lambda_1)(\lambda_2-\lambda_3)\mathbf{q}_2=(2-1)(2-4)\mathbf{q}_2=-2\,\mathbf{q}_2$.
> What remains: $-2\,\alpha_2\mathbf{q}_2=\mathbf{0}$. Since $\mathbf{q}_2\neq\mathbf{0}$, $\alpha_2=0$. Doing the same for $k=1$ and $k=3$ gives $\alpha_1=\alpha_3=0$: the eigenvectors are independent.
> With $\lambda_3=2=\lambda_2$ the number is $(2-1)(2-2)=0$. The equation becomes $\mathbf{0}=\mathbf{0}$ and says nothing about $\alpha_2$. This is why Case 2 needs a separate study.

> [!question]- Check (slide 58): $A$ has the rows $(0,1)$, $(-5,-2)$. Find the eigenvalues, an eigenvector, $Q$ and $\Lambda$, and check $AQ=Q\Lambda$ on the first column. Then give the real modal form (info box above).
> $\Delta(\lambda)=\lambda^2-(\operatorname{tr}A)\lambda+\det A=\lambda^2+2\lambda+5$. Roots: $\lambda=\dfrac{-2\pm\sqrt{4-20}}{2}=-1\pm2i$.
> $\lambda_1=-1+2i$: the first row of $(A-\lambda_1I)\mathbf{q}=\mathbf{0}$ is $-\lambda_1q_1+q_2=0$, so $\mathbf{q}_1=(1,\lambda_1)=(1,\,-1+2i)$. Then $\mathbf{q}_2=\bar{\mathbf{q}}_1=(1,\,-1-2i)$.
> $$Q=\begin{bmatrix}1&1\\-1+2i&-1-2i\end{bmatrix},\qquad\Lambda=\begin{bmatrix}-1+2i&0\\0&-1-2i\end{bmatrix}$$
> First column: $A\mathbf{q}_1=(-1+2i,\ -5-2(-1+2i))=(-1+2i,\ -3-4i)$. $\lambda_1\mathbf{q}_1=(-1+2i,\ (-1+2i)^2)=(-1+2i,\ 1-4i-4)=(-1+2i,\ -3-4i)$. Equal. $\det Q=-4i\neq0$, so $Q^{-1}AQ=\Lambda$.
> Modal form: $\sigma=-1$, $\omega=2$, $\mathbf{u}=\operatorname{Re}\mathbf{q}_1=(1,-1)$, $\mathbf{v}=\operatorname{Im}\mathbf{q}_1=(0,2)$.
> $$Q_r=\begin{bmatrix}1&0\\-1&2\end{bmatrix},\qquad Q_r^{-1}AQ_r=\begin{bmatrix}-1&2\\-2&-1\end{bmatrix}$$
> Check: $AQ_r=\begin{bmatrix}-1&2\\-3&-4\end{bmatrix}$ and $Q_r\begin{bmatrix}-1&2\\-2&-1\end{bmatrix}=\begin{bmatrix}-1&2\\1-4&-2-2\end{bmatrix}=\begin{bmatrix}-1&2\\-3&-4\end{bmatrix}$. Equal.

## 7. Diagonalization, repeated eigenvalues (slides 59-60)
![[ee502_eee501alllecturenotesabo_p059.jpg]]
![[ee502_eee501alllecturenotesabo_p060.jpg]]

**Notes.** **Case 2.** With repeated eigenvalues, diagonalization may or may not be possible. Rule: $A$ is diagonalizable exactly when, for every eigenvalue, the nullity of $A-\lambda_iI$ (geometric multiplicity) equals its multiplicity as a root of $\Delta$ (algebraic multiplicity).

**Example 1 (diagonalizable).** $A=\begin{bmatrix}0&0&-2\\0&1&0\\1&0&3\end{bmatrix}$, $\Delta(\lambda)=(\lambda-1)^2(\lambda-2)$.

$$\mathcal{N}(A-I)=\mathcal{N}\begin{bmatrix}-1&0&-2\\0&0&0\\1&0&2\end{bmatrix}=\operatorname{span}\left\{\begin{bmatrix}0\\1\\0\end{bmatrix},\begin{bmatrix}2\\0\\-1\end{bmatrix}\right\},\qquad \mathcal{N}(A-2I)=\operatorname{span}\left\{\begin{bmatrix}1\\0\\-1\end{bmatrix}\right\}$$

Nullity 2 = multiplicity 2. $Q=\begin{bmatrix}0&2&1\\1&0&0\\0&-1&-1\end{bmatrix}$ gives $Q^{-1}AQ=\operatorname{diag}\{1,1,2\}$.

**Example 2 (not diagonalizable).** $A=\begin{bmatrix}0&0&-2\\1&1&0\\1&0&3\end{bmatrix}$, same $\Delta(\lambda)=(\lambda-1)^2(\lambda-2)$. Now

$$\mathcal{N}(A-I)=\mathcal{N}\begin{bmatrix}-1&0&-2\\1&0&0\\1&0&2\end{bmatrix}=\operatorname{span}\left\{\begin{bmatrix}0\\1\\0\end{bmatrix}\right\},\qquad \mathcal{N}(A-2I)=\operatorname{span}\left\{\begin{bmatrix}1\\1\\-1\end{bmatrix}\right\}$$

Only one eigenvector for the double eigenvalue 1 (nullity 1 < 2). No diagonal form: this leads to the Jordan form, [[EE502 L07 - Jordan form]].

> [!warning] Watch out
> Slide 59 prints the third row of $A-I$ in Example 1 as $[1\ \ 0\ \ -2]$. Since $a_{33}=3$, the correct row is $[1\ \ 0\ \ 2]$.

> [!question]- Check (slide 59): $A$ has the rows $(3,0,2)$, $(0,2,0)$, $(1,0,4)$. Find the eigenvalues with their algebraic and geometric multiplicities. Is $A$ diagonalizable? If yes, give $Q$ and $\Lambda$ and check $AQ=Q\Lambda$.
> Expand $\det(\lambda I-A)$ along row 2: $\Delta=(\lambda-2)[(\lambda-3)(\lambda-4)-2]=(\lambda-2)(\lambda^2-7\lambda+10)=(\lambda-2)^2(\lambda-5)$.
> $\lambda=2$, algebraic multiplicity 2: $A-2I$ has the rows $(1,0,2)$, $(0,0,0)$, $(1,0,2)$. Rank 1, nullity $3-1=2$. One equation $x_1+2x_3=0$, with $x_2$ and $x_3$ free: $\mathbf{q}_{11}=(0,1,0)$, $\mathbf{q}_{12}=(2,0,-1)$.
> $\lambda=5$, algebraic multiplicity 1: $A-5I$ has the rows $(-2,0,2)$, $(0,-3,0)$, $(1,0,-1)$. $x_2=0$, $x_1=x_3$: $\mathbf{q}_2=(1,0,1)$. Geometric multiplicity 1.
> Geometric = algebraic for both eigenvalues ($2=2$ and $1=1$): **diagonalizable**.
> $$Q=\begin{bmatrix}0&2&1\\1&0&0\\0&-1&1\end{bmatrix},\qquad\Lambda=\operatorname{diag}\{2,2,5\},\qquad AQ=Q\Lambda=\begin{bmatrix}0&4&5\\2&0&0\\0&-2&5\end{bmatrix}$$
> $\det Q=-3\neq0$, so $Q^{-1}AQ=\Lambda$.

> [!question]- Check (slide 60): $A(k)$ has the rows $(2,k,0)$, $(0,2,0)$, $(1,0,5)$. Its characteristic polynomial is $(\lambda-2)^2(\lambda-5)$ for every $k$. For which $k$ is $A(k)$ diagonalizable?
> Only the double eigenvalue 2 can cause a problem. $A(k)-2I$ has the rows $(0,k,0)$, $(0,0,0)$, $(1,0,3)$.
> $k=0$: only the row $(1,0,3)$ is nonzero. Rank 1, nullity 2. Eigenvectors $(0,1,0)$ and $(-3,0,1)$. Geometric 2 = algebraic 2: **diagonalizable**.
> $k\neq0$: the rows $(0,k,0)$ and $(1,0,3)$ are independent. Rank 2, nullity 1. Only the eigenvector $(-3,0,1)$. Geometric 1 < algebraic 2: **not diagonalizable**.
> So $A(k)$ is diagonalizable only for $k=0$. This is the situation of the slide: Example 1 and Example 2 differ in one entry, have the same $\Delta(\lambda)$, and only one of them has a diagonal form.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Existence | $A\mathbf{x}=\mathbf{y}$ solvable iff $\operatorname{rank}A=\operatorname{rank}[A\ \ \mathbf{y}]$, for all $\mathbf{y}$ iff $\operatorname{rank}A=m$ |
| All solutions | $\mathbf{x}=\mathbf{x}_p+\alpha_1\mathbf{n}_1+\cdots+\alpha_\nu\mathbf{n}_\nu$ |
| Determinant | $\det A=\sum_i a_{ij}c_{ij}$, $\det A=0$ iff dependent columns iff nullity $>0$ |
| Inverse | $A^{-1}=\operatorname{adj}A/\det A$, $\operatorname{adj}A=[c_{ij}]^{\mathsf T}$ |
| Similarity | $\hat A=Q^{-1}AQ$, same $\Delta$, eigenvalues, $\det$, trace, rank |
| Companion matrix | ones under the diagonal, last column $\beta_1,\dots,\beta_n$ |
| Characteristic polynomial | $\Delta(\lambda)=\det(\lambda I-A)$ |
| Eigenvector | $(A-\lambda I)\mathbf{q}=\mathbf{0}$, $\mathbf{q}\neq\mathbf{0}$ |
| Diagonalization | $Q^{-1}AQ=\Lambda$, possible iff geometric = algebraic multiplicity for every $\lambda_i$ |

## Check yourself
> [!question]- 1. For $A$ with the rows $(1,2)$, $(2,4)$, for which $\mathbf{y}=(a,b)$ is $A\mathbf{x}=\mathbf{y}$ solvable? Solve for $\mathbf{y}=(1,2)$.
> $A=\begin{bmatrix}1&2\\2&4\end{bmatrix}$.
> $R_2\leftarrow R_2-2R_1$ gives the row $0=b-2a$. Solvable iff $b=2a$. For $(1,2)$: $x_1+2x_2=1$, so $\mathbf{x}=(1,0)+t(-2,1)$.

> [!question]- 2. All solutions of $x_1+2x_2+3x_3=1$, $2x_1+4x_2+7x_3=3$
> Reduced form: $\begin{bmatrix}1&2&0&-2\\0&0&1&1\end{bmatrix}$. $x_3=1$, $x_1=-2-2x_2$: $\mathbf{x}=(-2,0,1)+t(-2,1,0)$.

> [!question]- 3. For which $k$ is the matrix with the rows $(1,k)$, $(k,4)$ singular?
> The matrix is $\begin{bmatrix}1&k\\k&4\end{bmatrix}$.
> $\det=4-k^2=0$, so $k=2$ or $k=-2$.

> [!question]- 4. Compute $Q^{-1}AQ$ for $A$ with the rows $(2,0)$, $(0,3)$ and $Q$ with the rows $(1,1)$, $(0,1)$. Check trace and determinant.
> $A=\begin{bmatrix}2&0\\0&3\end{bmatrix}$, $Q=\begin{bmatrix}1&1\\0&1\end{bmatrix}$.
> $Q^{-1}=\begin{bmatrix}1&-1\\0&1\end{bmatrix}$, $AQ=\begin{bmatrix}2&2\\0&3\end{bmatrix}$, $Q^{-1}AQ=\begin{bmatrix}2&-1\\0&3\end{bmatrix}$. Trace 5, determinant 6, as for $A$.

> [!question]- 5. Eigenvalues of the matrix with the rows $(0,1)$, $(-4,0)$?
> The matrix is $\begin{bmatrix}0&1\\-4&0\end{bmatrix}$.
> Trace 0, determinant 4: $\Delta=\lambda^2+4$, $\lambda=\pm2i$.

> [!question]- 6. Is the matrix $A$ with the rows $(2,1)$, $(0,2)$ diagonalizable?
> $A=\begin{bmatrix}2&1\\0&2\end{bmatrix}$.
> $\Delta=(\lambda-2)^2$. $A-2I=\begin{bmatrix}0&1\\0&0\end{bmatrix}$, null space $\operatorname{span}\{(1,0)\}$. Geometric 1 < algebraic 2: **not diagonalizable**.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L03 - Vector spaces, norms and rank]]. Next: [[EE502 L05 - Functions of a matrix]]. Jordan form: [[EE502 L07 - Jordan form]]
- Used by Quiz 3 (12 Nov, no calculator, slides 36-64) and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_04_Equations_Eigenvalues.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_04/EE502_Lecture_04_Equations_Eigenvalues.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_04/EE502_Lecture_04_Equations_Eigenvalues.pdf`
- Original slides (PDF, pp. 47-60): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L04 - Equations, eigenvalues, diagonalization - quiz]]

Slides not embedded: none.
