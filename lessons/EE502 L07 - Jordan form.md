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

> [!question]- Check (main deck, slide 61, diagonalizable or not): Find the mistake: "A $3\times3$ matrix with $\Delta(\lambda)=(\lambda-3)^3$ is never diagonalizable." Then decide for the matrix $A$ with rows $(3,1,0)$, $(0,3,0)$, $(0,0,3)$.
> The statement is wrong. $3I$ has $\Delta(\lambda)=(\lambda-3)^3$ and is already diagonal.
> A repeated eigenvalue alone does not decide. What decides: the number of independent eigenvectors $\nu(A-\lambda I)$ (geometric multiplicity) against the multiplicity of the root (algebraic multiplicity). Diagonalizable needs them equal.
> For $A=\begin{bmatrix}3&1&0\\0&3&0\\0&0&3\end{bmatrix}$: $A-3I$ has a single nonzero entry, so its rank is 1 and $\nu(A-3I)=3-1=2<3$.
> Only two independent eigenvectors ($\mathbf{e}_1$ and $\mathbf{e}_3$). $A$ is not diagonalizable. One generalized eigenvector is needed.

> [!question]- Check (main deck, slide 61, grade and chain): $A$ has rows $(2,1,1)$, $(0,2,1)$, $(0,0,2)$ and $\lambda=2$. Find the grade of $\mathbf{u}=(0,1,0)$ and of $\mathbf{w}=(0,0,1)$. Build the chain (5) that starts from $\mathbf{w}$.
> $N=A-2I=\begin{bmatrix}0&1&1\\0&0&1\\0&0&0\end{bmatrix}$, $N^2=\begin{bmatrix}0&0&1\\0&0&0\\0&0&0\end{bmatrix}$, $N^3=0$.
> $\mathbf{u}$: $N\mathbf{u}=(1,0,0)\neq\mathbf{0}$ and $N^2\mathbf{u}=\mathbf{0}$. Grade 2.
> $\mathbf{w}$: $N\mathbf{w}=(1,1,0)$, $N^2\mathbf{w}=(1,0,0)\neq\mathbf{0}$, $N^3\mathbf{w}=\mathbf{0}$. Grade 3.
> Chain from $\mathbf{w}$: $\mathbf{v}_3=\mathbf{w}=(0,0,1)$, $\mathbf{v}_2=N\mathbf{v}_3=(1,1,0)$, $\mathbf{v}_1=N\mathbf{v}_2=(1,0,0)$.
> $\mathbf{v}_1$ is a true eigenvector: $N\mathbf{v}_1=\mathbf{0}$.

> [!question]- Check (main deck, slide 62): In the first line of the proof, $(A-\lambda I)^{k-1}$ is applied to $\sum\alpha_i\mathbf{v}_i$. Why do all terms with $i<k$ vanish, and why does $\alpha_k=0$ follow?
> By (5), $\mathbf{v}_i=(A-\lambda I)^{k-i}\mathbf{v}$. So $(A-\lambda I)^{k-1}\mathbf{v}_i=(A-\lambda I)^{2k-1-i}\mathbf{v}$.
> For $i\le k-1$ the power is $2k-1-i\ge k$. Then the result is $\mathbf{0}$, because $(A-\lambda I)^k\mathbf{v}=\mathbf{0}$ by (4).
> For $i=k$ the power is $k-1$, and $(A-\lambda I)^{k-1}\mathbf{v}\neq\mathbf{0}$ by (4).
> What remains is $\alpha_k\cdot(\text{nonzero vector})=\mathbf{0}$. So $\alpha_k=0$. The next line repeats this with the power $k-2$.

## 2. Example 2 continued (slide 63)
![[ee502_eee501alllecturenotesabo_p063.jpg]]

**Notes.** $A=\begin{bmatrix}0&0&-2\\1&1&0\\1&0&3\end{bmatrix}$, $\Delta=(\lambda-1)^2(\lambda-2)$. With $N=A-I$:

$$N=\begin{bmatrix}-1&0&-2\\1&0&0\\1&0&2\end{bmatrix},\qquad N^2=\begin{bmatrix}-1&0&-2\\-1&0&-2\\1&0&2\end{bmatrix}$$

$\mathbf{v}_2=[2\ \ 0\ \ -1]^{\mathsf T}$ satisfies $N^2\mathbf{v}_2=\mathbf{0}$ and $N\mathbf{v}_2\neq\mathbf{0}$: grade 2. Then $\mathbf{v}_1=N\mathbf{v}_2=[0\ \ 2\ \ 0]^{\mathsf T}$. With the eigenvector $\mathbf{q}_2=[1\ \ 1\ \ -1]^{\mathsf T}$ of $\lambda_2=2$ and $Q=[\mathbf{v}_1\ \ \mathbf{v}_2\ \ \mathbf{q}_2]$:

$$AQ=Q\begin{bmatrix}1&1&0\\0&1&0\\0&0&2\end{bmatrix}$$

because $A\mathbf{v}_1=\mathbf{v}_1$, $A\mathbf{v}_2=\mathbf{v}_1+\mathbf{v}_2$, $A\mathbf{q}_2=2\mathbf{q}_2$. In $Q$ the chain is listed bottom-up: eigenvector first, top of the chain last.

> [!warning] Watch out
> The slide prints the second row of $(A-I)^2$ as $[1\ \ 0\ \ -2]$. The correct row is $[-1\ \ 0\ \ -2]$. With the misprint, $\mathbf{v}_2$ would not satisfy $(A-I)^2\mathbf{v}_2=\mathbf{0}$.

> [!question]- Check (main deck, slide 63, new matrix): $A$ has rows $(3,1,0)$, $(-1,1,0)$, $(1,1,4)$ and $\Delta(\lambda)=(\lambda-2)^2(\lambda-4)$. Find a chain for $\lambda_1=2$, the matrix $Q$ and $J=Q^{-1}AQ$.
> $N=A-2I=\begin{bmatrix}1&1&0\\-1&-1&0\\1&1&2\end{bmatrix}$. $N\mathbf{x}=\mathbf{0}$ gives $x_1+x_2=0$ and $x_3=0$: one eigenvector $(1,-1,0)$, nullity 1. Not diagonalizable.
> $N^2=\begin{bmatrix}0&0&0\\0&0&0\\2&2&4\end{bmatrix}$. $N^2\mathbf{x}=\mathbf{0}$ means $x_1+x_2+2x_3=0$.
> Choose $\mathbf{v}_2=(1,1,-1)$: $N^2\mathbf{v}_2=\mathbf{0}$ and $\mathbf{v}_1=N\mathbf{v}_2=(2,-2,0)\neq\mathbf{0}$. Grade 2, and $\mathbf{v}_1$ is an eigenvector.
> $\lambda_2=4$: $(A-4I)\mathbf{x}=\mathbf{0}$ gives $x_1=x_2=0$, so $\mathbf{q}_2=(0,0,1)$.
> $$Q=[\mathbf{v}_1\ \ \mathbf{v}_2\ \ \mathbf{q}_2]=\begin{bmatrix}2&1&0\\-2&1&0\\0&-1&1\end{bmatrix},\qquad J=\begin{bmatrix}2&1&0\\0&2&0\\0&0&4\end{bmatrix}$$
> Check $AQ=QJ$ column by column: $A\mathbf{v}_1=(4,-4,0)=2\mathbf{v}_1$. $A\mathbf{v}_2=(4,0,-2)=\mathbf{v}_1+2\mathbf{v}_2$. $A\mathbf{q}_2=(0,0,4)=4\mathbf{q}_2$.
> Another choice of $\mathbf{v}_2$ gives another $Q$ but the same $J$.

> [!question]- Check (main deck, slide 63, column order): On the slide, $Q=[\mathbf{v}_1\ \ \mathbf{v}_2\ \ \mathbf{q}_2]$. What is $Q^{-1}AQ$ if the first two columns are swapped, $Q=[\mathbf{v}_2\ \ \mathbf{v}_1\ \ \mathbf{q}_2]$?
> Column $j$ of $Q^{-1}AQ$ holds the coordinates of $A\cdot(\text{column }j\text{ of }Q)$ in the basis of the columns of $Q$.
> $A\mathbf{v}_2=\mathbf{v}_2+\mathbf{v}_1$: coordinates $(1,1,0)$ in the basis $(\mathbf{v}_2,\mathbf{v}_1,\mathbf{q}_2)$. $A\mathbf{v}_1=\mathbf{v}_1$: coordinates $(0,1,0)$. $A\mathbf{q}_2=2\mathbf{q}_2$: $(0,0,2)$.
> $$Q^{-1}AQ=\begin{bmatrix}1&0&0\\1&1&0\\0&0&2\end{bmatrix}$$
> The 1 moves below the diagonal. This is not the Jordan form of the theorem. The chain must be listed eigenvector first.

## 3. Jordan normal form theorem (slide 64)
![[ee502_eee501alllecturenotesabo_p064.jpg]]

**Notes.** **Theorem.** Every $A\in\mathbb{R}^{n\times n}$ with $\Delta(\lambda)=(\lambda-\lambda_1)^{n_1}\cdots(\lambda-\lambda_k)^{n_k}$ (distinct $\lambda_i$, $\sum n_i=n$) is similar to

$$J_A=\operatorname{diag}\{\Lambda_1,\dots,\Lambda_k\},\qquad\Lambda_i=\operatorname{diag}\{J_{i1},\dots,J_{i\nu_i}\}\in\mathbb{C}^{n_i\times n_i}$$

- $\Lambda_i$ collects all Jordan blocks of $\lambda_i$, in non-increasing sizes.
- The number of blocks is $\nu_i=\nu(A-\lambda_iI)$, the nullity (number of independent eigenvectors).
- Each Jordan block $J_{il}$ has $\lambda_i$ on the diagonal, ones on the diagonal just above, zeros elsewhere.

Three numbers per eigenvalue: $n_i$ (algebraic multiplicity, total size of $\Lambda_i$), $\nu_i$ (geometric multiplicity, number of blocks), $m_i$ (index, size of the largest block, see [[EE502 L05 - Functions of a matrix]]).

> [!info] Index, minimal polynomial and $e^{Jt}$ (beyond the slides of this lecture)
> These slides stop at the form $J_A$. Lectures 5 and 6 use it as follows.
> - **Index $m_i$**: the size of the largest Jordan block of $\lambda_i$. It is also the smallest $j$ with $\nu\bigl((A-\lambda_iI)^j\bigr)=n_i$. Reason: for a block $J$ of size $m$, $(J-\lambda_iI)^j=0$ exactly when $j\ge m$.
> - **Minimal polynomial**: $\psi(\lambda)=(\lambda-\lambda_1)^{m_1}\cdots(\lambda-\lambda_k)^{m_k}$. It is the monic polynomial of lowest degree with $\psi(A)=0$. Each factor needs the power $m_i$ to make the largest block of $\lambda_i$ zero. $\psi$ divides $\Delta$ because $m_i\le n_i$.
> - $A$ is diagonalizable exactly when every $m_i=1$.
> - **Functions.** $f(A)=Qf(J_A)Q^{-1}$, and $f(J_A)$ is computed block by block. For a block of size 3, with $N=J-\lambda I$ and $N^3=0$:
> $$e^{Jt}=e^{\lambda t}\Bigl(I+tN+\frac{t^2}{2}N^2\Bigr)=e^{\lambda t}\begin{bmatrix}1&t&t^2/2\\0&1&t\\0&0&1\end{bmatrix}$$
> A block of size $m$ gives the terms $e^{\lambda t},te^{\lambda t},\dots,\frac{t^{m-1}}{(m-1)!}e^{\lambda t}$. So the highest power of $t$ next to $e^{\lambda_it}$ in $e^{At}$ is $m_i-1$.

> [!question]- Check (main deck, slide 64, reading the form): $J_A$ is $6\times6$. It has Jordan blocks of sizes 3 and 1 for $\lambda_1=2$ and one block of size 2 for $\lambda_2=-1$. Write $J_A$ and give $n_i$, $\nu_i$, $m_i$ and $\Delta(\lambda)$.
> $$J_A=\begin{bmatrix}2&1&0&0&0&0\\0&2&1&0&0&0\\0&0&2&0&0&0\\0&0&0&2&0&0\\0&0&0&0&-1&1\\0&0&0&0&0&-1\end{bmatrix}$$
> $\lambda_1=2$: $n_1=3+1=4$ (total size), $\nu_1=2$ (number of blocks), $m_1=3$ (largest block).
> $\lambda_2=-1$: $n_2=2$, $\nu_2=1$, $m_2=2$.
> $\Delta(\lambda)=(\lambda-2)^4(\lambda+1)^2$. The blocks of $\lambda_1$ are in non-increasing size, as the theorem asks.

> [!question]- Check (main deck, slide 64, minimal polynomial): For the same $J_A$ (blocks of sizes 3 and 1 for $\lambda_1=2$, one block of size 2 for $\lambda_2=-1$), give the minimal polynomial. Is $(A-2I)^2(A+I)^2=0$ for a matrix $A$ with this Jordan form?
> $\psi(\lambda)=(\lambda-2)^{m_1}(\lambda+1)^{m_2}=(\lambda-2)^3(\lambda+1)^2$. Degree 5, one less than $\Delta$.
> $(A-2I)^2(A+I)^2\neq0$. The block of size 3 has $N^2\neq0$, so it needs the power 3. The factor $(A+I)^2$ is invertible on that block (it has the eigenvalue $(2+1)^2=9$ there), so it cannot repair this.
> In the same way $(A-2I)^3(A+I)\neq0$: the block of $\lambda_2$ has size 2.

> [!question]- Check (main deck, slide 64, exponential of a block): $J$ is one Jordan block of size 3 with $\lambda=-2$. Write $e^{Jt}$. What changes if the same eigenvalue has two blocks, of sizes 2 and 1?
> One block of size 3:
> $$e^{Jt}=e^{-2t}\begin{bmatrix}1&t&t^2/2\\0&1&t\\0&0&1\end{bmatrix}=\begin{bmatrix}e^{-2t}&te^{-2t}&\tfrac{t^2}{2}e^{-2t}\\0&e^{-2t}&te^{-2t}\\0&0&e^{-2t}\end{bmatrix}$$
> Blocks of sizes 2 and 1: compute each block alone.
> $$e^{Jt}=\begin{bmatrix}e^{-2t}&te^{-2t}&0\\0&e^{-2t}&0\\0&0&e^{-2t}\end{bmatrix}$$
> The term $\frac{t^2}{2}e^{-2t}$ is gone, because the index drops from 3 to 2. Both matrices have $\Delta(\lambda)=(\lambda+2)^3$.

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

> [!question]- Check (main deck, slide 65): Take a $5\times5$ matrix with $\Delta(\lambda)=(\lambda-\lambda_1)^3(\lambda-\lambda_2)^2$. How many different Jordan forms are possible? Do $n_i$ and $\nu_i$ fix the form here, against Remark 2?
> $\lambda_1$ ($n_1=3$): block sizes 3, or 2+1, or 1+1+1. Three choices, with $\nu_1=1,2,3$.
> $\lambda_2$ ($n_2=2$): block sizes 2, or 1+1. Two choices, with $\nu_2=1,2$.
> Total: $3\cdot2=6$ Jordan forms.
> Each choice has its own $\nu_i$, so here $n_i$ and $\nu_i$ do fix the form. Remark 2 needs $n_i\ge4$: only then two different lists with the same number of blocks exist (3+1 and 2+2).

> [!question]- Check (main deck, slide 66): For Case 1 and for Case 2 give the nullities $d_j=\nu\bigl((A-\lambda_1I)^j\bigr)$, the index $m_1$ and the minimal polynomial.
> Use: number of blocks of size $\ge j$ equals $d_j-d_{j-1}$.
> Case 1 (one block of size 4): one block of size $\ge j$ for $j=1,2,3,4$. So $d_1=1$, $d_2=2$, $d_3=3$, $d_4=4$. $m_1=4$ and $\psi(\lambda)=(\lambda-\lambda_1)^4(\lambda-\lambda_2)=\Delta(\lambda)$.
> Case 2 (sizes 2, 1, 1): three blocks of size $\ge1$, one of size $\ge2$. So $d_1=3$, $d_2=3+1=4=n_1$. $m_1=2$ and $\psi(\lambda)=(\lambda-\lambda_1)^2(\lambda-\lambda_2)$.
> In Case 1 the nullity grows by one per power. This is why a vector of grade 4 must exist.

> [!question]- Check (main deck, slide 67): $A$ is $4\times4$ with $\Delta(\lambda)=(\lambda-3)^4$. With $N=A-3I$ you find $\nu(N)=2$ and $\nu(N^2)=4$. Give the block sizes, $J$, the index and the minimal polynomial. What changes if $\nu(N^2)=3$?
> Blocks of size $\ge1$: $d_1=2$. Blocks of size $\ge2$: $d_2-d_1=4-2=2$. $d_2=4=n$, so there is no block of size $\ge3$. Sizes 2 and 2. This is Case 4(ii).
> $$J=\begin{bmatrix}3&1&0&0\\0&3&0&0\\0&0&3&1\\0&0&0&3\end{bmatrix}$$
> Index $m=2$, $\psi(\lambda)=(\lambda-3)^2$. $e^{At}$ contains $e^{3t}$ and $te^{3t}$ only.
> If $\nu(N^2)=3$: blocks of size $\ge2$: $3-2=1$. Then $\nu(N^3)=4$ and blocks of size $\ge3$: $4-3=1$. Sizes 3 and 1, Case 4(i). Index 3, $\psi(\lambda)=(\lambda-3)^3$, and $e^{At}$ also contains $\frac{t^2}{2}e^{3t}$.

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

> [!question]- Check (handout, slide 2): A tree like Figure 1 has these boxes. Under $\lambda_1=0$: $\{\mathbf{v}_{111},\mathbf{v}_{112},\mathbf{v}_{113}\}$ and $\{\mathbf{v}_{121},\mathbf{v}_{122}\}$. Under $\lambda_2=4$: $\{\mathbf{v}_{211}\}$ and $\{\mathbf{v}_{221}\}$. Read off the size of $A$, the Jordan blocks and $p(s)$.
> Count the vectors: $3+2+1+1=7$. $A$ is $7\times7$.
> Each box is one Jordan block, and the largest $k$ in the box is its size.
> $\lambda_1=0$: two boxes, so two blocks, of sizes 3 and 2. Algebraic multiplicity $3+2=5$, geometric multiplicity 2.
> $\lambda_2=4$: two boxes with one vector each, so two blocks of size 1. Algebraic and geometric multiplicity 2 (this part is diagonal).
> $J=\operatorname{diag}\{J_3(0),J_2(0),4,4\}$, where $J_m(\lambda)$ is the Jordan block of size $m$. $p(s)=s^5(s-4)^2$.

> [!question]- Check (handout, slides 3-4): $A$ is $7\times7$ with $p(s)=(s-2)^6(s-4)$. The nullity for $\lambda_1=2$ is 4. How many generalized eigenvectors must be produced? Which block sizes are possible, and which computation decides?
> Six independent vectors are needed for $\lambda_1$. Four are simple eigenvectors. So $6-4=2$ generalized eigenvectors must be produced. There are four Jordan blocks for $\lambda_1$.
> Both come from the same eigenvector: sizes 3, 1, 1, 1.
> They come from two different eigenvectors: sizes 2, 2, 1, 1.
> The nullity of $(A-2I)^2$ decides. Blocks of size $\ge2$: $d_2-d_1$. For 3+1+1+1 this is 1, so $d_2=5$. For 2+2+1+1 it is 2, so $d_2=6$.
> $\lambda_2=4$ gives one block of size 1 in both cases.

> [!question]- Check (handout, slide 4, producing): $A$ has rows $(1,0,0)$, $(0,1,1)$, $(0,0,1)$. Its eigenvectors for $\lambda=1$ are $\mathbf{e}_1$ and $\mathbf{e}_2$. Which of them produces a generalized eigenvector, that is, for which is $(A-I)\mathbf{x}=\mathbf{v}$ solvable?
> $N=A-I=\begin{bmatrix}0&0&0\\0&0&1\\0&0&0\end{bmatrix}$, so $N\mathbf{x}=(0,x_3,0)$ for every $\mathbf{x}$.
> $N\mathbf{x}=\mathbf{e}_1=(1,0,0)$: impossible, the first entry of $N\mathbf{x}$ is always 0. $\mathbf{e}_1$ produces nothing.
> $N\mathbf{x}=\mathbf{e}_2=(0,1,0)$: $x_3=1$, for example $\mathbf{x}=\mathbf{e}_3$. So $\mathbf{e}_2$ produces $\mathbf{e}_3$.
> Blocks: sizes 2 (chain $\mathbf{e}_2,\mathbf{e}_3$) and 1 ($\mathbf{e}_1$). The handout says "any of the simple eigenvectors" can produce. That is an assumption. A given eigenvector can fail, as $\mathbf{e}_1$ does here.

> [!question]- Check (handout, slide 5): Keep the handout example ($6\times6$, $p(s)=(s-1)^5(s-5)$, nullity 3). Now assume both generalized eigenvectors are produced by $\mathbf{v}_{111}$ (vectors $\mathbf{v}_{112}$ and $\mathbf{v}_{113}$). Write the new $J$. What is the same as in (1), and what is different?
> Groups: $\{\mathbf{v}_{111},\mathbf{v}_{112},\mathbf{v}_{113}\}$, $\{\mathbf{v}_{121}\}$, $\{\mathbf{v}_{131}\}$ for $\lambda_1=1$ and $\{\mathbf{v}_{211}\}$ for $\lambda_2=5$. Block sizes 3, 1, 1 and 1.
> $$J=\begin{bmatrix}1&1&0&0&0&0\\0&1&1&0&0&0\\0&0&1&0&0&0\\0&0&0&1&0&0\\0&0&0&0&1&0\\0&0&0&0&0&5\end{bmatrix}$$
> Same: the diagonal, three blocks for $\lambda_1$, and two ones above the diagonal ($n_1-\nu_1=5-3=2$).
> Different: the two ones are now in one block (positions $(1,2)$ and $(2,3)$). In (1) they are at $(1,2)$ and $(3,4)$. The largest block has size 3, not 2, so the two matrices are not similar.

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
> [!question]- 1. For $A$ with the rows $(2,1)$ and $(0,2)$ find a chain for $\lambda=2$.
> $N=A-2I=\begin{bmatrix}0&1\\0&0\end{bmatrix}$. Eigenvector $\mathbf{v}_1=\mathbf{e}_1$. $N\mathbf{e}_2=\mathbf{e}_1\neq\mathbf{0}$, $N^2=0$: $\mathbf{v}_2=\mathbf{e}_2$ has grade 2.

> [!question]- 2. For the shift $N$ with the rows $(0,1,0)$, $(0,0,1)$ and $(0,0,0)$, what is the grade of $\mathbf{e}_3$?
> $N\mathbf{e}_3=\mathbf{e}_2$, $N^2\mathbf{e}_3=\mathbf{e}_1\neq\mathbf{0}$, $N^3\mathbf{e}_3=\mathbf{0}$. Grade 3.

> [!question]- 3. (Quiz style) $A$ with the rows $(4,-1)$ and $(1,2)$: eigenvalue, chain, $Q$ and $J$.
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
