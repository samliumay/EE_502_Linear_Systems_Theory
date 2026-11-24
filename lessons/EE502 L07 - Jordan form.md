---
course: EE 502 Linear System Theory
lecture: 7
title: Jordan form
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 61-67) + lectures/jordanFormExplanation2.pdf
full_notes: lecture_notes/lecture_07/EE502_Lecture_07_Jordan_Form.pdf
---
# EE 502 · Lecture 7 · Jordan form

> [!summary] In short
> - When a repeated eigenvalue has too few eigenvectors, no diagonal form exists. We settle for "almost diagonal".
> - A generalized eigenvector of grade $k$ satisfies $(A-\lambda I)^k\mathbf{v}=\mathbf{0}$ and $(A-\lambda I)^{k-1}\mathbf{v}\neq\mathbf{0}$. It starts a chain of $k$ independent vectors.
> - Each chain gives one Jordan block: $\lambda$ on the diagonal, ones just above.
> - Every square matrix is similar to a Jordan form. Number of blocks of $\lambda_i$ = nullity of $A-\lambda_iI$.
> - Block sizes come from the nullities of the powers $(A-\lambda_iI)^j$.

> [!info] Order of the lectures
> The slides show the Jordan form (pp. 61-67) before matrix functions (pp. 68-80). The syllabus teaches it in week 7. Quiz 3 covers slides 36-64, so sections 1 to 3 below.

## 1. Generalized eigenvectors and chains (slides 61-62)
![[ee502_eee501alllecturenotesabo_p061.jpg]]
![[ee502_eee501alllecturenotesabo_p062.jpg]]

**Notes.** Example 2 of [[EE502 L04 - Equations, eigenvalues, diagonalization]] has only one eigenvector for the double eigenvalue 1, so no $Q$ gives a diagonal $Q^{-1}AQ$.

**Definition.** $\mathbf{v}$ is a **generalized eigenvector of grade $k$** for $\lambda$ if

$$(A-\lambda I)^k\mathbf{v}=\mathbf{0}\quad\text{and}\quad(A-\lambda I)^{k-1}\mathbf{v}\neq\mathbf{0}\qquad(4)$$

**Chain.** From a grade-$k$ vector $\mathbf{v}$ define $\mathbf{v}_j=(A-\lambda I)^{k-j}\mathbf{v}$:

$$\mathbf{v}_k=\mathbf{v},\quad\mathbf{v}_{k-1}=(A-\lambda I)\mathbf{v}_k,\quad\dots,\quad\mathbf{v}_1=(A-\lambda I)\mathbf{v}_2\qquad(5)$$

$\mathbf{v}_1$ is a true eigenvector. **Fact:** $\{\mathbf{v}_1,\dots,\mathbf{v}_k\}$ is linearly independent. Proof idea: apply $(A-\lambda I)^{k-1}$ to $\sum\alpha_i\mathbf{v}_i=\mathbf{0}$. Only the $\mathbf{v}_k$ term survives, so $\alpha_k=0$. Repeat with lower powers.

**A chain gives a Jordan block.** $A\mathbf{v}_1=\lambda\mathbf{v}_1$ and $A\mathbf{v}_j=\mathbf{v}_{j-1}+\lambda\mathbf{v}_j$, so

$$A\begin{bmatrix}\mathbf{v}_1&\cdots&\mathbf{v}_k\end{bmatrix}=\begin{bmatrix}\mathbf{v}_1&\cdots&\mathbf{v}_k\end{bmatrix}\begin{bmatrix}\lambda&1&&\\&\lambda&\ddots&\\&&\ddots&1\\&&&\lambda\end{bmatrix}$$

> [!warning] Watch out
> - Both conditions in (4) are needed. An eigenvector also satisfies $(A-\lambda I)^2\mathbf{v}=\mathbf{0}$, yet its grade is 1.
> - The slide says $\mathbf{v}\in\mathbb{R}^n$. For a non-real $\lambda$ the vector is complex, so $\mathbf{v}\in\mathbb{C}^n$ in general.

## 2. Example 2 continued (slide 63)
![[ee502_eee501alllecturenotesabo_p063.jpg]]

**Notes.** $A=\begin{bmatrix}0&0&-2\\1&1&0\\1&0&3\end{bmatrix}$, $\Delta=(\lambda-1)^2(\lambda-2)$. With $N=A-I$:

$$N=\begin{bmatrix}-1&0&-2\\1&0&0\\1&0&2\end{bmatrix},\qquad N^2=\begin{bmatrix}-1&0&-2\\-1&0&-2\\1&0&2\end{bmatrix}$$

$\mathbf{v}_2=[2\ \ 0\ \ -1]^{\mathsf T}$ satisfies $N^2\mathbf{v}_2=\mathbf{0}$ and $N\mathbf{v}_2\neq\mathbf{0}$: grade 2. Then $\mathbf{v}_1=N\mathbf{v}_2=[0\ \ 2\ \ 0]^{\mathsf T}$. With the eigenvector $\mathbf{q}_2=[1\ \ 1\ \ -1]^{\mathsf T}$ of $\lambda_2=2$ and $Q=[\mathbf{v}_1\ \ \mathbf{v}_2\ \ \mathbf{q}_2]$:

$$AQ=Q\begin{bmatrix}1&1&0\\0&1&0\\0&0&2\end{bmatrix}$$

because $A\mathbf{v}_1=\mathbf{v}_1$, $A\mathbf{v}_2=\mathbf{v}_1+\mathbf{v}_2$, $A\mathbf{q}_2=2\mathbf{q}_2$. In $Q$ the chain is listed bottom-up: eigenvector first, top of the chain last.

> [!warning] Watch out
> The slide prints the second row of $(A-I)^2$ as $[1\ \ 0\ \ -2]$. The correct row is $[-1\ \ 0\ \ -2]$. With the misprint, $\mathbf{v}_2$ would not satisfy $(A-I)^2\mathbf{v}_2=\mathbf{0}$.

## 3. Jordan normal form theorem (slide 64)
![[ee502_eee501alllecturenotesabo_p064.jpg]]

**Notes.** **Theorem.** Every $A\in\mathbb{R}^{n\times n}$ with $\Delta(\lambda)=(\lambda-\lambda_1)^{n_1}\cdots(\lambda-\lambda_k)^{n_k}$ (distinct $\lambda_i$, $\sum n_i=n$) is similar to

$$J_A=\operatorname{diag}\{\Lambda_1,\dots,\Lambda_k\},\qquad\Lambda_i=\operatorname{diag}\{J_{i1},\dots,J_{i\nu_i}\}\in\mathbb{C}^{n_i\times n_i}$$

- $\Lambda_i$ collects all Jordan blocks of $\lambda_i$, in non-increasing sizes.
- The number of blocks is $\nu_i=\nu(A-\lambda_iI)$, the nullity (number of independent eigenvectors).
- Each Jordan block $J_{il}$ has $\lambda_i$ on the diagonal, ones on the diagonal just above, zeros elsewhere.

Three numbers per eigenvalue: $n_i$ (algebraic multiplicity, total size of $\Lambda_i$), $\nu_i$ (geometric multiplicity, number of blocks), $m_i$ (index, size of the largest block, see [[EE502 L05 - Functions of a matrix]]).

## 4. Which Jordan forms are possible (slides 65-67)
![[ee502_eee501alllecturenotesabo_p065.jpg]]
![[ee502_eee501alllecturenotesabo_p066.jpg]]
![[ee502_eee501alllecturenotesabo_p067.jpg]]

**Notes.** **Remark 1.** Lecture 4 Example 1 had $\nu(A-\lambda_1I)=2$: two $1\times1$ blocks, diagonal. Example 2 had $\nu=1$: one $2\times2$ block.

**Remark 2.** $n_i$ and $\nu_i$ are not enough to fix the Jordan form. The grades of the generalized eigenvectors fix the block sizes.

**Counting rule (ours).** With $N=A-\lambda_iI$, $d_j=\nu(N^j)$ and $d_0=0$:

$$\#\{\text{blocks of }\lambda_i\text{ of size}\ge j\}=d_j-d_{j-1}$$

**Example 3.** $A$ is $5\times5$, $\Delta=(\lambda-\lambda_1)^4(\lambda-\lambda_2)$. $\lambda_2$ always gives one $1\times1$ block. For $\lambda_1$:

| $\nu(A-\lambda_1I)$ | Blocks of $\lambda_1$ | $Q$ |
|---|---|---|
| 1 (Case 1) | one block of size 4 | chain $\mathbf{v}_1,\dots,\mathbf{v}_4$, then $\mathbf{q}_1$ |
| 3 (Case 2) | sizes 2, 1, 1 | $[\mathbf{v}_1\ \mathbf{v}_2\ \mathbf{w}_1\ \mathbf{w}_2\ \mathbf{q}_1]$ |
| 4 (Case 3) | sizes 1, 1, 1, 1 (diagonal) | four eigenvectors, then $\mathbf{q}_1$ |
| 2 (Case 4) | sizes 3, 1 **or** 2, 2 | decided by $d_2$: 3 for (3,1), 4 for (2,2) |

**Recipe (by hand).** For each eigenvalue: (1) compute $d_j=\nu(N^j)$ until $d_j=n_i$. (2) Blocks of size $\ge j$: $d_j-d_{j-1}$. (3) For each block of size $m$, pick a vector in $\mathcal{N}(N^m)$ not in $\mathcal{N}(N^{m-1})$, multiply down by $N$ to get the chain, and put it in $Q$ bottom-up. (4) Check $AQ=QJ$ column by column.

> [!warning] Watch out
> - Slide 66, Case 1: "an eigenvector of multiplicity $n_1$" means an **eigenvalue** of multiplicity $n_1$. Case 2: $\Lambda_1=\{J_{11},J_{12},J_{13}\}$ means $\operatorname{diag}\{J_{11},J_{12},J_{13}\}$.
> - Slide 67, Case 4(i) lists the $1\times1$ block $\lambda_1$ outside $\Lambda_1$. Consistent with the theorem: $\Lambda_1=\operatorname{diag}\{J_{11},J_{12}\}$ with $J_{12}=\lambda_1$. Same matrix.
> - Same eigenvalues do not imply similar. Two matrices with the same $\Delta$ and the same $\nu_1$ can have different $d_2$.

## 5. Instructor's handout: the tree of eigenvectors (handout pages 2-5)
![[ee502_jordanformexplanation2_p002.jpg]]
![[ee502_jordanformexplanation2_p003.jpg]]
![[ee502_jordanformexplanation2_p004.jpg]]
![[ee502_jordanformexplanation2_p005.jpg]]

**Notes.** A. Yıldız's handout (posted 11 Nov 2026) draws the Jordan form as a tree of vectors $\mathbf{v}_{ijk}$:

- $i$ counts the distinct eigenvalues. Each gives a group of Jordan blocks.
- $j$ counts the simple (true) eigenvectors of $\lambda_i$. Each gives one Jordan block.
- $k$ is the grade inside chain $j$. The largest $k$ is the size of that block.

**Handout example.** $A$ is $6\times6$, $p(s)=(s-1)^5(s-5)$. The nullity for $\lambda_1=1$ is 3: three simple eigenvectors $\mathbf{v}_{111},\mathbf{v}_{121},\mathbf{v}_{131}$, so three Jordan blocks. Five vectors are needed for $\lambda_1$, so two generalized eigenvectors are missing. The handout assumes $\mathbf{v}_{111}$ produces $\mathbf{v}_{112}$ and $\mathbf{v}_{121}$ produces $\mathbf{v}_{122}$. Block sizes: 2, 2, 1. $\lambda_2=5$ gives one block of size 1.

$$J=\begin{bmatrix}1&1&0&0&0&0\\0&1&0&0&0&0\\0&0&1&1&0&0\\0&0&0&1&0&0\\0&0&0&0&1&0\\0&0&0&0&0&5\end{bmatrix}$$

To produce a generalized eigenvector from an eigenvector, solve $(A-\lambda_iI)\mathbf{x}=\mathbf{v}_{ij1}$.

> [!warning] Watch out
> - Direction: the handout goes up from the eigenvector (solve $N\mathbf{x}=\mathbf{v}_{ij1}$). The slides go down from the top vector (multiply by $N$). Same $J$.
> - The handout assumes which eigenvector produces what. With $n_1=5$ and nullity 3, both 2+2+1 and 3+1+1 fit. The counting rule decides: $d_2=5$ for 2+2+1, $d_2=4$ for 3+1+1.
> - Not every eigenvector produces a generalized one: $N\mathbf{x}=\mathbf{v}$ can have no solution. Sometimes only a combination of the eigenvectors works.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Generalized eigenvector, grade $k$ | $(A-\lambda I)^k\mathbf{v}=\mathbf{0}\neq(A-\lambda I)^{k-1}\mathbf{v}$ |
| Chain | $\mathbf{v}_{j-1}=(A-\lambda I)\mathbf{v}_j$, $\mathbf{v}_1$ is an eigenvector |
| Chain relation | $A\mathbf{v}_1=\lambda\mathbf{v}_1$, $A\mathbf{v}_j=\mathbf{v}_{j-1}+\lambda\mathbf{v}_j$ |
| Jordan block | $\lambda$ on the diagonal, ones just above |
| Jordan form | $Q^{-1}AQ=J_A=\operatorname{diag}\{\Lambda_1,\dots,\Lambda_k\}$ |
| Number of blocks of $\lambda_i$ | $\nu_i=\nu(A-\lambda_iI)$ |
| Blocks of size $\ge j$ | $\nu\bigl((A-\lambda_iI)^j\bigr)-\nu\bigl((A-\lambda_iI)^{j-1}\bigr)$ |
| Order in $Q$ | each chain bottom-up: eigenvector first |
| Symmetric $M$ (look ahead) | real eigenvalues, orthogonal eigenvectors, no Jordan block of size $\ge2$ |

## Check yourself
> [!question]- 1. For $A=\begin{bmatrix}2&1\\0&2\end{bmatrix}$ find a chain for $\lambda=2$.
> $N=A-2I=\begin{bmatrix}0&1\\0&0\end{bmatrix}$. Eigenvector $\mathbf{v}_1=\mathbf{e}_1$. $N\mathbf{e}_2=\mathbf{e}_1\neq\mathbf{0}$, $N^2=0$: $\mathbf{v}_2=\mathbf{e}_2$ has grade 2.

> [!question]- 2. For the shift $N=\begin{bmatrix}0&1&0\\0&0&1\\0&0&0\end{bmatrix}$, what is the grade of $\mathbf{e}_3$?
> $N\mathbf{e}_3=\mathbf{e}_2$, $N^2\mathbf{e}_3=\mathbf{e}_1\neq\mathbf{0}$, $N^3\mathbf{e}_3=\mathbf{0}$. Grade 3.

> [!question]- 3. (Quiz style) $A=\begin{bmatrix}4&-1\\1&2\end{bmatrix}$: eigenvalue, chain, $Q$ and $J$.
> $\Delta=\lambda^2-6\lambda+9=(\lambda-3)^2$. $N=A-3I=\begin{bmatrix}1&-1\\1&-1\end{bmatrix}$, eigenvector $\mathbf{v}_1=(1,1)$, nullity 1. Solve $N\mathbf{v}_2=\mathbf{v}_1$: $x_1-x_2=1$, take $\mathbf{v}_2=(1,0)$. $Q=\begin{bmatrix}1&1\\1&0\end{bmatrix}$, $J=\begin{bmatrix}3&1\\0&3\end{bmatrix}$. Check: $A\mathbf{v}_2=(4,1)=\mathbf{v}_1+3\mathbf{v}_2$.

> [!question]- 4. $A$ is $3\times3$, $\Delta=(\lambda-1)^3$, $\nu(A-I)=2$. Jordan form?
> Two blocks with sizes adding to 3: sizes 2 and 1. $J=\begin{bmatrix}1&1&0\\0&1&0\\0&0&1\end{bmatrix}$.

> [!question]- 5. For $n_1=4$ you find $d_1=2$, $d_2=3$, $d_3=4$. Block sizes?
> Size $\ge1$: 2 blocks. Size $\ge2$: $3-2=1$. Size $\ge3$: $4-3=1$. Size $\ge4$: 0. So sizes 3 and 1.

> [!question]- 6. In the handout example, why is the Jordan form not fixed by $n_1=5$ and nullity 3 alone?
> Three blocks adding to 5 can be 2+2+1 or 3+1+1. The handout assumes two eigenvectors each produce one generalized eigenvector (2+2+1). Check with $d_2$: 5 for 2+2+1, 4 for 3+1+1.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L06 - Matrix exponential]]. Background: [[EE502 L04 - Equations, eigenvalues, diagonalization]], [[EE502 L05 - Functions of a matrix]]
- Used by Quiz 3 (12 Nov, no calculator, slides 36-64: up to the Jordan theorem) and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_07_Jordan_Form.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_07/EE502_Lecture_07_Jordan_Form.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_07/EE502_Lecture_07_Jordan_Form.pdf`
- Original slides (PDF, pp. 61-67): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Jordan-form handout (PDF, 5 pages): [jordanFormExplanation2.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/jordanFormExplanation2.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/jordanFormExplanation2.pdf`

Slides not embedded: handout page 1 (title page).
