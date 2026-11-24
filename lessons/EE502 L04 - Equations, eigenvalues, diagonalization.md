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

## 5. Eigenvalues and eigenvectors (slide 56)
![[ee502_eee501alllecturenotesabo_p056.jpg]]

**Notes.** $\lambda\in\mathbb{C}$ is an **eigenvalue** of $A$ if there is a nonzero $\mathbf{x}\in\mathbb{C}^n$ (an **eigenvector**) with $(A-\lambda I_n)\mathbf{x}=\mathbf{0}$. The **characteristic polynomial** is

$$\Delta(\lambda)=\det(\lambda I_n-A)=\lambda^n+\alpha_1\lambda^{n-1}+\cdots+\alpha_n$$

It has $n$ roots counting multiplicities, non-real roots come in conjugate pairs. $\mathcal{N}(A-\lambda_iI)\neq\{\mathbf{0}\}$ iff $\Delta(\lambda_i)=0$, so the eigenvalues are the roots of $\Delta$.

By hand: compute $\Delta$, find the roots, then row reduce $A-\lambda_iI$ for each root. Checks: $\sum\lambda_i=\operatorname{tr}A$, $\prod\lambda_i=\det A$. For $2\times2$: $\Delta=\lambda^2-(\operatorname{tr}A)\lambda+\det A$.

> [!warning] Watch out
> Eigenvectors are never unique (any nonzero multiple works). A repeated root does not guarantee as many independent eigenvectors as its multiplicity.

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
> [!question]- 1. For $A=\begin{bmatrix}1&2\\2&4\end{bmatrix}$, for which $\mathbf{y}=(a,b)$ is $A\mathbf{x}=\mathbf{y}$ solvable? Solve for $\mathbf{y}=(1,2)$.
> $R_2\leftarrow R_2-2R_1$ gives the row $0=b-2a$. Solvable iff $b=2a$. For $(1,2)$: $x_1+2x_2=1$, so $\mathbf{x}=(1,0)+t(-2,1)$.

> [!question]- 2. All solutions of $x_1+2x_2+3x_3=1$, $2x_1+4x_2+7x_3=3$
> Reduced form: $\begin{bmatrix}1&2&0&-2\\0&0&1&1\end{bmatrix}$. $x_3=1$, $x_1=-2-2x_2$: $\mathbf{x}=(-2,0,1)+t(-2,1,0)$.

> [!question]- 3. For which $k$ is $\begin{bmatrix}1&k\\k&4\end{bmatrix}$ singular?
> $\det=4-k^2=0$, so $k=2$ or $k=-2$.

> [!question]- 4. Compute $Q^{-1}AQ$ for $A=\begin{bmatrix}2&0\\0&3\end{bmatrix}$, $Q=\begin{bmatrix}1&1\\0&1\end{bmatrix}$. Check trace and determinant.
> $Q^{-1}=\begin{bmatrix}1&-1\\0&1\end{bmatrix}$, $AQ=\begin{bmatrix}2&2\\0&3\end{bmatrix}$, $Q^{-1}AQ=\begin{bmatrix}2&-1\\0&3\end{bmatrix}$. Trace 5, determinant 6, as for $A$.

> [!question]- 5. Eigenvalues of $\begin{bmatrix}0&1\\-4&0\end{bmatrix}$?
> Trace 0, determinant 4: $\Delta=\lambda^2+4$, $\lambda=\pm2i$.

> [!question]- 6. Is $\begin{bmatrix}2&1\\0&2\end{bmatrix}$ diagonalizable?
> $\Delta=(\lambda-2)^2$. $A-2I=\begin{bmatrix}0&1\\0&0\end{bmatrix}$, null space $\operatorname{span}\{(1,0)\}$. Geometric 1 < algebraic 2: **not diagonalizable**.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L03 - Vector spaces, norms and rank]]. Next: [[EE502 L05 - Functions of a matrix]]. Jordan form: [[EE502 L07 - Jordan form]]
- Used by Quiz 3 (12 Nov, no calculator, slides 36-64) and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_04_Equations_Eigenvalues.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_04/EE502_Lecture_04_Equations_Eigenvalues.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_04/EE502_Lecture_04_Equations_Eigenvalues.pdf`
- Original slides (PDF, pp. 47-60): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: none.
