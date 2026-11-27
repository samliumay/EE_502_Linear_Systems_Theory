---
course: EE 502 Linear System Theory
lesson: EE502 L07 - Jordan form
type: quiz
questions: 15
---

# EE502 L07 - Jordan form - quiz

Lesson note: [[EE502 L07 - Jordan form]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. $\nu(M)$ is the nullity of $M$ (dimension of its null space). A Jordan block has $\lambda$ on the diagonal and ones just above it. $J_m(\lambda)$ is the Jordan block of size $m$.

## 1. Generalized eigenvectors and chains (slides 61-62)

### Q1 (main deck, slide 61, diagonalizable or not)

$A$ is the $3\times3$ matrix with the rows $(3,1,0)$, $(0,3,0)$, $(0,0,3)$, so $\Delta(\lambda)=(\lambda-3)^3$. What is the number of independent eigenvectors $\nu(A-3I)$, and is $A$ diagonalizable?

- A) $\nu(A-3I)=2$. $A$ is not diagonalizable.
- B) $\nu(A-3I)=1$. $A$ is not diagonalizable.
- C) $\nu(A-3I)=2$. $A$ is diagonalizable.
- D) $\nu(A-3I)=1$. $A$ is diagonalizable.

> [!success]- Answer
> **A.** $A-3I$ has a single nonzero entry (the 1 at position $(1,2)$). Its rank is 1, so $\nu(A-3I)=3-1=2$.
> Diagonalizable needs as many independent eigenvectors as the algebraic multiplicity 3. Here $2<3$: not diagonalizable. One generalized eigenvector is needed.
> Note: a repeated root alone does not decide. $3I$ also has $\Delta(\lambda)=(\lambda-3)^3$ and is diagonal.
> - B: The rank 1 of $A-3I$ was taken as the nullity.
> - C: $\nu=2$ was compared with the number of distinct eigenvalues (1), not with the algebraic multiplicity 3.
> - D: Both slips: rank taken as nullity, then $\nu=1$ compared with the one distinct eigenvalue.

### Q2 (main deck, slide 61, grade and chain)

$A$ has the rows $(2,1,1)$, $(0,2,1)$, $(0,0,2)$ and $\lambda=2$. $\mathbf{w}=(0,0,1)$. The grade of $\mathbf{w}$ is the $k$ with $(A-2I)^k\mathbf{w}=\mathbf{0}$ and $(A-2I)^{k-1}\mathbf{w}\neq\mathbf{0}$. The chain (5) is $\mathbf{v}_k=\mathbf{w}$ and $\mathbf{v}_{j-1}=(A-2I)\mathbf{v}_j$ down to $\mathbf{v}_1$. What is the grade of $\mathbf{w}$, and what is $\mathbf{v}_1$?

- A) Grade 3, and $\mathbf{v}_1=(0,0,1)$.
- B) Grade 3, and $\mathbf{v}_1=(1,0,0)$.
- C) Grade 2, and $\mathbf{v}_1=(1,0,0)$.
- D) Grade 2, and $\mathbf{v}_1=(0,0,1)$.

> [!success]- Answer
> **B.** $N=A-2I$ has the rows $(0,1,1)$, $(0,0,1)$, $(0,0,0)$.
> $N\mathbf{w}=(1,1,0)$, $N^2\mathbf{w}=(1,0,0)\neq\mathbf{0}$, $N^3\mathbf{w}=\mathbf{0}$. So the grade is 3.
> Chain: $\mathbf{v}_3=\mathbf{w}=(0,0,1)$, $\mathbf{v}_2=N\mathbf{v}_3=(1,1,0)$, $\mathbf{v}_1=N\mathbf{v}_2=(1,0,0)$. Check: $N\mathbf{v}_1=\mathbf{0}$, so $\mathbf{v}_1$ is a true eigenvector.
> - A: The chain was built in the wrong direction: $\mathbf{w}$ was put at the bottom as $\mathbf{v}_1$. But $N\mathbf{w}\neq\mathbf{0}$, so $\mathbf{w}$ is not an eigenvector.
> - C: The grade was taken as the largest power with $N^k\mathbf{w}\neq\mathbf{0}$ (that is 2). The grade is one more: the first power that gives $\mathbf{0}$.
> - D: Both slips: grade off by one and the chain in the wrong direction.

### Q3 (main deck, slide 62)

$\mathbf{v}$ has grade $k$ for $\lambda$, and the chain is $\mathbf{v}_i=(A-\lambda I)^{k-i}\mathbf{v}$ for $i=1,\dots,k$. To prove independence, the proof applies $(A-\lambda I)^{k-1}$ to $\sum_{i=1}^{k}\alpha_i\mathbf{v}_i=\mathbf{0}$ and concludes $\alpha_k=0$. Which reasoning is correct?

- A) Each $\mathbf{v}_i$ with $i<k$ is an eigenvector, so already $(A-\lambda I)\mathbf{v}_i=\mathbf{0}$. Only $\mathbf{v}_k$ is not one, so $\alpha_k=0$ follows.
- B) $(A-\lambda I)^{k-1}\mathbf{v}_i=(A-\lambda I)^{2k-1-i}\mathbf{v}$. For $i<k$ the power is at least $k$, so $\mathbf{0}$. For $i=k$ it is nonzero, so $\alpha_k=0$.
- C) $(A-\lambda I)^{k-1}\mathbf{v}_i=(A-\lambda I)^{k+i-2}\mathbf{v}$. For $i\ge2$ the power is at least $k$, so $\mathbf{0}$. Only $i=1$ is left, so $\alpha_1=0$ first.
- D) The vectors $\mathbf{v}_1,\dots,\mathbf{v}_k$ are linearly independent, so the terms with $i<k$ give $\mathbf{0}$. The term with $i=k$ is left, so $\alpha_k=0$.

> [!success]- Answer
> **B.** $(A-\lambda I)^{k-1}\mathbf{v}_i=(A-\lambda I)^{k-1}(A-\lambda I)^{k-i}\mathbf{v}=(A-\lambda I)^{2k-1-i}\mathbf{v}$.
> For $i\le k-1$: $2k-1-i\ge k$, and $(A-\lambda I)^k\mathbf{v}=\mathbf{0}$ (grade $k$). So these terms are $\mathbf{0}$.
> For $i=k$: the power is $k-1$, and $(A-\lambda I)^{k-1}\mathbf{v}\neq\mathbf{0}$ (grade $k$). So $\alpha_k\cdot(\text{nonzero vector})=\mathbf{0}$ and $\alpha_k=0$.
> - A: Only $\mathbf{v}_1$ is an eigenvector. For example $\mathbf{v}_2$ has $(A-\lambda I)\mathbf{v}_2=\mathbf{v}_1\neq\mathbf{0}$.
> - C: This uses the chain in the wrong direction, $\mathbf{v}_i=(A-\lambda I)^{i-1}\mathbf{v}$. In (5) the top vector is $\mathbf{v}_k=\mathbf{v}$, not $\mathbf{v}_1$.
> - D: Circular: independence is what the proof wants to show, so it cannot be used as a step.

## 2. Example 2 continued (slide 63)

### Q4 (main deck, slide 63, new matrix)

$A$ has the rows $(3,1,0)$, $(-1,1,0)$, $(1,1,4)$ and $\Delta(\lambda)=(\lambda-2)^2(\lambda-4)$. Take $\mathbf{v}_2=(1,1,-1)$ as the top of a chain for $\lambda_1=2$ (it has grade 2). $\mathbf{v}_1$ is the eigenvector at the bottom of this chain, $\mathbf{q}_2=(0,0,1)$ is an eigenvector for $\lambda_2=4$, and $Q=[\mathbf{v}_1\ \ \mathbf{v}_2\ \ \mathbf{q}_2]$. Find $\mathbf{v}_1$ and $Q^{-1}AQ$.

- A) $\mathbf{v}_1=(4,0,-2)$ and $Q^{-1}AQ=\begin{bmatrix}2&1&0\\0&2&0\\0&0&4\end{bmatrix}$
- B) $\mathbf{v}_1=(2,-2,0)$ and $Q^{-1}AQ=\begin{bmatrix}2&0&0\\1&2&0\\0&0&4\end{bmatrix}$
- C) $\mathbf{v}_1=(4,0,-2)$ and $Q^{-1}AQ=\begin{bmatrix}2&0&0\\1&2&0\\0&0&4\end{bmatrix}$
- D) $\mathbf{v}_1=(2,-2,0)$ and $Q^{-1}AQ=\begin{bmatrix}2&1&0\\0&2&0\\0&0&4\end{bmatrix}$

> [!success]- Answer
> **D.** $N=A-2I$ has the rows $(1,1,0)$, $(-1,-1,0)$, $(1,1,2)$. $\mathbf{v}_1=N\mathbf{v}_2=(1+1,\ -1-1,\ 1+1-2)=(2,-2,0)$, and $N\mathbf{v}_1=\mathbf{0}$.
> Columns of $AQ$: $A\mathbf{v}_1=(4,-4,0)=2\mathbf{v}_1$. $A\mathbf{v}_2=(4,0,-2)=\mathbf{v}_1+2\mathbf{v}_2$. $A\mathbf{q}_2=(0,0,4)=4\mathbf{q}_2$.
> The coordinates $(2,0,0)$, $(1,2,0)$, $(0,0,4)$ are the columns of $Q^{-1}AQ$: the 1 is above the diagonal.
> - A: $\mathbf{v}_1$ was computed as $A\mathbf{v}_2$ instead of $(A-2I)\mathbf{v}_2$, and $J$ was then copied from the theorem without a check. $(4,0,-2)$ is not an eigenvector: $(A-2I)(4,0,-2)=(4,-4,0)\neq\mathbf{0}$. With this $Q$, $Q^{-1}AQ$ has the rows $(4,1,0)$, $(-4,0,0)$, $(0,0,4)$.
> - B: The coordinates of $A\mathbf{v}_2$ were written as a row: the 1 was put below the diagonal.
> - C: Both slips: $A\mathbf{v}_2$ used as $\mathbf{v}_1$ and the 1 below the diagonal.

### Q5 (main deck, slide 63, column order)

$A$ has the rows $(0,0,-2)$, $(1,1,0)$, $(1,0,3)$. For $\lambda_1=1$ the chain is $\mathbf{v}_2=(2,0,-1)$ (grade 2) and $\mathbf{v}_1=(A-I)\mathbf{v}_2=(0,2,0)$. $\mathbf{q}_2=(1,1,-1)$ is an eigenvector for $\lambda_2=2$. Now the first two columns are swapped: $Q=[\mathbf{v}_2\ \ \mathbf{v}_1\ \ \mathbf{q}_2]$. What is $Q^{-1}AQ$?

- A) $\begin{bmatrix}1&0&0\\1&1&0\\0&0&2\end{bmatrix}$
- B) $\begin{bmatrix}1&1&0\\0&1&0\\0&0&2\end{bmatrix}$
- C) $\begin{bmatrix}1&1&0\\1&0&0\\0&0&2\end{bmatrix}$
- D) $\begin{bmatrix}0&1&0\\1&1&0\\0&0&2\end{bmatrix}$

> [!success]- Answer
> **A.** Column $j$ of $Q^{-1}AQ$ holds the coordinates of $A\cdot(\text{column }j\text{ of }Q)$ in the basis $(\mathbf{v}_2,\mathbf{v}_1,\mathbf{q}_2)$.
> $A\mathbf{v}_2=(2,2,-1)=\mathbf{v}_2+\mathbf{v}_1$: coordinates $(1,1,0)$. $A\mathbf{v}_1=(0,2,0)=\mathbf{v}_1$: coordinates $(0,1,0)$. $A\mathbf{q}_2=(2,2,-2)=2\mathbf{q}_2$: $(0,0,2)$.
> The 1 is below the diagonal. This is not the Jordan form of the theorem: the chain must be listed eigenvector first.
> - B: The order of the columns was ignored. This is $Q^{-1}AQ$ for $Q=[\mathbf{v}_1\ \ \mathbf{v}_2\ \ \mathbf{q}_2]$.
> - C: Only the columns of the old result were swapped. $Q^{-1}$ also swaps the rows.
> - D: Only the rows of the old result were swapped. The columns of $Q$ swap the columns too.

## 3. Jordan normal form theorem (slide 64)

### Q6 (main deck, slide 64, reading the form)

$J_A$ is $6\times6$. It has Jordan blocks of sizes 3 and 1 for $\lambda_1=2$ and one Jordan block of size 2 for $\lambda_2=-1$. For $\lambda_1=2$ give the algebraic multiplicity $n_1$, the geometric multiplicity $\nu_1=\nu(J_A-2I)$ and the index $m_1$ (smallest $j$ with $\nu\bigl((J_A-2I)^j\bigr)=n_1$).

- A) $n_1=4$, $\nu_1=3$, $m_1=2$
- B) $n_1=3$, $\nu_1=3$, $m_1=2$
- C) $n_1=4$, $\nu_1=2$, $m_1=3$
- D) $n_1=3$, $\nu_1=2$, $m_1=3$

> [!success]- Answer
> **C.** $n_1$ is the total size of the blocks of $\lambda_1$: $3+1=4$. $\nu_1$ is the number of blocks: 2. $m_1$ is the size of the largest block: 3.
> So $\Delta(\lambda)=(\lambda-2)^4(\lambda+1)^2$. For $\lambda_2=-1$: $n_2=2$, $\nu_2=1$, $m_2=2$.
> - A: $\nu_1$ and $m_1$ were swapped: the nullity was taken as the largest block size.
> - B: Both slips: only the first block counted for $n_1$, and $\nu_1$ and $m_1$ swapped.
> - D: Only the block of size 3 was counted for $n_1$. The block of size 1 adds one more.

### Q7 (main deck, slide 64, minimal polynomial)

$A$ has the Jordan form with blocks of sizes 3 and 1 for $\lambda_1=2$ and one block of size 2 for $\lambda_2=-1$ ($6\times6$). The minimal polynomial $\psi$ is the monic polynomial of lowest degree with $\psi(A)=0$. Find $\psi(\lambda)$. Is $(A-2I)^2(A+I)^2=0$?

- A) $\psi(\lambda)=(\lambda-2)^4(\lambda+1)^2$. No, $(A-2I)^2(A+I)^2\neq0$.
- B) $\psi(\lambda)=(\lambda-2)^3(\lambda+1)^2$. No, $(A-2I)^2(A+I)^2\neq0$.
- C) $\psi(\lambda)=(\lambda-2)^2(\lambda+1)$. Yes, $(A-2I)^2(A+I)^2=0$.
- D) $\psi(\lambda)=(\lambda-2)(\lambda+1)$. Yes, $(A-2I)^2(A+I)^2=0$.

> [!success]- Answer
> **B.** The exponent of each factor of $\psi$ is the size of the largest block: $m_1=3$, $m_2=2$. So $\psi(\lambda)=(\lambda-2)^3(\lambda+1)^2$, degree 5.
> On the block of size 3, $N=J-2I$ has $N^2\neq0$ (one 1 in the corner), so it needs the power 3.
> $(A+I)^2$ is invertible on that block (eigenvalue $(2+1)^2=9$), so it cannot make up for the missing power. The product is not 0.
> - A: The exponents are the algebraic multiplicities. That is $\Delta(\lambda)$, degree 6, not the minimal polynomial. With it, the answer No is right, but $\psi$ is not.
> - C: The exponent was taken as the number of blocks $\nu_i$ ($\nu_1=2$, $\nu_2=1$), not the largest block size. Then $\psi$ divides $(\lambda-2)^2(\lambda+1)^2$, which gives the wrong Yes.
> - D: Each eigenvalue was taken once, as for a diagonalizable matrix. That holds only when all blocks have size 1. It also gives the wrong Yes.

### Q8 (main deck, slide 64, exponential of a block)

$J$ is one Jordan block of size 3 with $\lambda=-2$. Which matrix is $e^{Jt}$?

- A) $e^{-2t}\begin{bmatrix}1&t&t^2\\0&1&t\\0&0&1\end{bmatrix}$
- B) $e^{-2t}\begin{bmatrix}1&t&t^2/2\\0&1&t\\0&0&1\end{bmatrix}$
- C) $e^{-2t}\begin{bmatrix}1&0&0\\t&1&0\\t^2/2&t&1\end{bmatrix}$
- D) $e^{-2t}\begin{bmatrix}1&0&0\\t&1&0\\t^2&t&1\end{bmatrix}$

> [!success]- Answer
> **B.** $J=-2I+N$ with $N$ the ones above the diagonal. $N^2$ has a single 1 at $(1,3)$ and $N^3=0$. $-2I$ and $N$ commute, so
> $e^{Jt}=e^{-2t}\bigl(I+tN+\tfrac{t^2}{2!}N^2\bigr)$. The $t$ terms sit above the diagonal, $t^2/2$ in the corner $(1,3)$.
> With blocks of sizes 2 and 1 instead, the $(1,3)$ entry is 0: the term $\tfrac{t^2}{2}e^{-2t}$ is gone, because the index drops from 3 to 2.
> - A: $\tfrac{t^2}{2!}$ was written as $t^2$: the $k!$ was dropped.
> - C: The ones of $N$ were put below the diagonal, so the result is transposed.
> - D: Both slips: transposed and without the $2!$.

## 4. Which Jordan forms are possible (slides 65-67)

### Q9 (main deck, slide 65)

$A$ is $5\times5$ with $\Delta(\lambda)=(\lambda-\lambda_1)^3(\lambda-\lambda_2)^2$, $\lambda_1\neq\lambda_2$. Blocks are listed $\lambda_1$ first, each eigenvalue with larger blocks first, so block order gives no new forms. How many different Jordan forms are possible? For this $\Delta$, do $n_i$ and $\nu_i=\nu(A-\lambda_iI)$ together fix the Jordan form?

- A) 6 forms. Yes, $n_i$ and $\nu_i$ fix the form here.
- B) 5 forms. Yes, $n_i$ and $\nu_i$ fix the form here.
- C) 6 forms. No, $n_i$ and $\nu_i$ do not fix the form here.
- D) 5 forms. No, $n_i$ and $\nu_i$ do not fix the form here.

> [!success]- Answer
> **A.** $\lambda_1$ ($n_1=3$): sizes 3, or 2+1, or 1+1+1, with $\nu_1=1,2,3$. $\lambda_2$ ($n_2=2$): sizes 2, or 1+1, with $\nu_2=1,2$.
> The choices are independent: $3\cdot2=6$ forms.
> Each list has its own number of blocks $\nu_i$, so $n_i$ and $\nu_i$ fix the form. Remark 2 needs $n_i\ge4$ (3+1 and 2+2 both have two blocks).
> - B: The choices were added ($3+2$), not multiplied.
> - C: Remark 2 was applied without checking: here no two lists have the same number of blocks.
> - D: Both slips: added, and Remark 2 applied.

### Q10 (main deck, slide 66)

$A$ is $5\times5$ with $\Delta(\lambda)=(\lambda-\lambda_1)^4(\lambda-\lambda_2)$. The Jordan blocks of $\lambda_1$ have the sizes 2, 1, 1 (Case 2). Let $d_j=\nu\bigl((A-\lambda_1I)^j\bigr)$. Find $d_1$, $d_2$ and the minimal polynomial $\psi(\lambda)$.

- A) $d_1=3$, $d_2=1$, $\psi(\lambda)=(\lambda-\lambda_1)^2(\lambda-\lambda_2)$
- B) $d_1=3$, $d_2=1$, $\psi(\lambda)=(\lambda-\lambda_1)^3(\lambda-\lambda_2)$
- C) $d_1=3$, $d_2=4$, $\psi(\lambda)=(\lambda-\lambda_1)^2(\lambda-\lambda_2)$
- D) $d_1=3$, $d_2=4$, $\psi(\lambda)=(\lambda-\lambda_1)^3(\lambda-\lambda_2)$

> [!success]- Answer
> **C.** Rule: number of blocks of size $\ge j$ is $d_j-d_{j-1}$, with $d_0=0$.
> Three blocks of size $\ge1$: $d_1=3$. One block of size $\ge2$: $d_2=d_1+1=4=n_1$.
> The largest block has size 2, so $m_1=2$ and $\psi(\lambda)=(\lambda-\lambda_1)^2(\lambda-\lambda_2)$.
> - A: $d_2$ was taken as the number of blocks of size $\ge2$ (1). That number is the difference $d_2-d_1$, not $d_2$.
> - B: Both slips: $d_2$ as the difference, and the exponent of $\psi$ taken as the number of blocks (3).
> - D: The exponent in $\psi$ was taken as the number of blocks $\nu_1=3$. It is the size of the largest block.

### Q11 (main deck, slide 67)

$A$ is $4\times4$ with $\Delta(\lambda)=(\lambda-3)^4$ and $N=A-3I$. You find $\nu(N)=2$. List the block sizes from large to small. What are they if $\nu(N^2)=4$, and what are they if $\nu(N^2)=3$?

- A) If $\nu(N^2)=4$: sizes 3, 1. If $\nu(N^2)=3$: sizes 2, 2.
- B) If $\nu(N^2)=4$: sizes 2, 2. If $\nu(N^2)=3$: sizes 2, 2.
- C) If $\nu(N^2)=4$: sizes 3, 1. If $\nu(N^2)=3$: sizes 3, 1.
- D) If $\nu(N^2)=4$: sizes 2, 2. If $\nu(N^2)=3$: sizes 3, 1.

> [!success]- Answer
> **D.** Blocks of size $\ge j$: $d_j-d_{j-1}$, with $d_j=\nu(N^j)$.
> $\nu(N^2)=4$: two blocks of size $\ge1$ and $4-2=2$ of size $\ge2$. $d_2=4=n$, so none of size 3. Sizes 2, 2; index 2.
> $\nu(N^2)=3$: one block of size $\ge2$ ($3-2$). Then $\nu(N^3)=4$, one block of size $\ge3$. Sizes 3, 1; index 3.
> - A: The two cases were swapped: a larger $\nu(N^2)$ means more blocks of size $\ge2$, not a larger block.
> - B: $n=4$ and $\nu=2$ were thought to fix the form, and 2, 2 was picked for both cases. They do not fix it: $\nu(N^2)$ decides.
> - C: The same slip, with 3, 1 picked for both cases.

## 5. Instructor's handout: the tree of eigenvectors (handout pages 2-5)

### Q12 (handout, slide 2)

In the handout's tree (Figure 1, below, shows its own example) $\mathbf{v}_{ijk}$ is the vector of grade $k$ in the chain of the $j$-th simple eigenvector of the $i$-th eigenvalue. Each box holds the vectors with the same $i$ and $j$. A new tree has these boxes. Under $\lambda_1=0$: $\{\mathbf{v}_{111},\mathbf{v}_{112},\mathbf{v}_{113}\}$ and $\{\mathbf{v}_{121},\mathbf{v}_{122}\}$. Under $\lambda_2=4$: $\{\mathbf{v}_{211}\}$ and $\{\mathbf{v}_{221}\}$. Which Jordan blocks does $A$ have (larger blocks first)?

![[ee502_jordanformexplanation2_p002.jpg]]

- A) $\lambda_1=0$: sizes 3 and 2. $\lambda_2=4$: sizes 1 and 1.
- B) $\lambda_1=0$: sizes 3 and 2. $\lambda_2=4$: one block of size 2.
- C) $\lambda_1=0$: one block of size 5. $\lambda_2=4$: sizes 1 and 1.
- D) $\lambda_1=0$: one block of size 5. $\lambda_2=4$: one block of size 2.

> [!success]- Answer
> **A.** Each box is one chain, so one Jordan block. Its size is the largest $k$ in the box.
> $\lambda_1=0$: boxes with $k\le3$ and $k\le2$, so blocks of sizes 3 and 2. $\lambda_2=4$: two boxes with one vector each, so two blocks of size 1.
> $A$ is $7\times7$, $J=\operatorname{diag}\{J_3(0),J_2(0),4,4\}$ and $p(s)=s^5(s-4)^2$.
> - B: The two one-vector boxes of $\lambda_2$ were joined into one chain. But $\mathbf{v}_{211}$ and $\mathbf{v}_{221}$ both have $k=1$: two eigenvectors, two blocks.
> - C: The two boxes of $\lambda_1$ were joined into one chain of length 5. Two values of $j$ mean two simple eigenvectors, so two blocks.
> - D: One block per eigenvalue: all boxes under an eigenvalue were joined.

### Q13 (handout, slides 3-4)

$A$ is $7\times7$ with $p(s)=(s-2)^6(s-4)$ and $\nu(A-2I)=4$, so $\lambda_1=2$ needs two generalized eigenvectors $\mathbf{x}$ and $\mathbf{y}$. Assume every equation below has a solution. Case (i), one chain: $(A-2I)\mathbf{x}=\mathbf{v}$ and $(A-2I)\mathbf{y}=\mathbf{x}$ for one simple eigenvector $\mathbf{v}$. Case (ii), two chains: $(A-2I)\mathbf{x}=\mathbf{v}$ and $(A-2I)\mathbf{y}=\mathbf{v}'$ for two independent simple eigenvectors $\mathbf{v}$, $\mathbf{v}'$. What is $d_2=\nu\bigl((A-2I)^2\bigr)$ in each case?

- A) (i): $d_2=6$. (ii): $d_2=5$.
- B) (i): $d_2=5$. (ii): $d_2=5$.
- C) (i): $d_2=6$. (ii): $d_2=6$.
- D) (i): $d_2=5$. (ii): $d_2=6$.

> [!success]- Answer
> **D.** $\lambda_1$ needs 6 vectors and has 4 simple eigenvectors, so $6-4=2$ generalized eigenvectors. There are 4 blocks.
> (i) One chain $\mathbf{v},\mathbf{x},\mathbf{y}$ of length 3: sizes 3, 1, 1, 1. One block of size $\ge2$, so $d_2=d_1+1=5$.
> (ii) Two chains $\mathbf{v},\mathbf{x}$ and $\mathbf{v}',\mathbf{y}$ of length 2: sizes 2, 2, 1, 1. Two blocks of size $\ge2$, so $d_2=4+2=6$.
> - A: The two cases were swapped: a longer chain was thought to give a larger nullity.
> - B: The nullity was assumed to grow by one per power, as in a single chain. That holds only when one block has size $\ge2$.
> - C: $(A-2I)^2$ was assumed to vanish on all 6 vectors of $\lambda_1$. In case (i) the block of size 3 needs the power 3.

### Q14 (handout, slide 4, producing)

$A$ has the rows $(1,0,0)$, $(0,1,1)$, $(0,0,1)$. Its eigenvectors for $\lambda=1$ are $\mathbf{e}_1$ and $\mathbf{e}_2$. An eigenvector $\mathbf{v}$ produces a generalized eigenvector when $(A-I)\mathbf{x}=\mathbf{v}$ has a solution. Which statement is right?

- A) Only $\mathbf{e}_1$ produces one: like $\mathbf{v}_{111}$ in the handout, the first eigenvector starts the chain.
- B) Both produce one: any simple eigenvector can start a chain of generalized eigenvectors.
- C) Only $\mathbf{e}_2$ produces one: $(A-I)\mathbf{x}=\mathbf{e}_2$ is solved by $\mathbf{x}=\mathbf{e}_3$.
- D) Neither produces one: $(A-I)\mathbf{v}=\mathbf{0}$, so $(A-I)\mathbf{x}=\mathbf{v}$ has no solution.

> [!success]- Answer
> **C.** $N=A-I$ has the single entry 1 at position $(2,3)$, so $N\mathbf{x}=(0,x_3,0)$ for every $\mathbf{x}$.
> $N\mathbf{x}=\mathbf{e}_2$: $x_3=1$, for example $\mathbf{x}=\mathbf{e}_3$. $N\mathbf{x}=\mathbf{e}_1$: impossible, the first entry of $N\mathbf{x}$ is always 0.
> Blocks: size 2 (chain $\mathbf{e}_2,\mathbf{e}_3$) and size 1 ($\mathbf{e}_1$).
> - A: The handout's example lets $\mathbf{v}_{111}$ produce, but that is a choice for the example, not a rule. Here $N\mathbf{x}=\mathbf{e}_1$ has no solution.
> - B: This is the handout's assumption. A given eigenvector can fail, as $\mathbf{e}_1$ does here.
> - D: $N\mathbf{v}=\mathbf{0}$ says nothing about $N\mathbf{x}=\mathbf{v}$. Here $\mathbf{e}_2$ is in the column space of $N$.

### Q15 (handout, slide 5)

$A$ is $6\times6$ with $p(s)=(s-1)^5(s-5)$ and $\nu(A-I)=3$, with simple eigenvectors $\mathbf{v}_{111},\mathbf{v}_{121},\mathbf{v}_{131}$. Both generalized eigenvectors come from $\mathbf{v}_{111}$ (they are $\mathbf{v}_{112}$ and $\mathbf{v}_{113}$). Give the block sizes of $\lambda_1=1$ (larger first) and the minimal polynomial $\psi(s)$.

- A) Sizes 3, 1, 1. $\psi(s)=(s-1)^2(s-5)$.
- B) Sizes 2, 2, 1. $\psi(s)=(s-1)^3(s-5)$.
- C) Sizes 3, 1, 1. $\psi(s)=(s-1)^3(s-5)$.
- D) Sizes 2, 2, 1. $\psi(s)=(s-1)^2(s-5)$.

> [!success]- Answer
> **C.** Groups: $\{\mathbf{v}_{111},\mathbf{v}_{112},\mathbf{v}_{113}\}$, $\{\mathbf{v}_{121}\}$, $\{\mathbf{v}_{131}\}$, so sizes 3, 1, 1. $\lambda_2=5$ gives one block of size 1.
> The largest block of $\lambda_1$ has size 3: $\psi(s)=(s-1)^3(s-5)$.
> Same as the handout's form (2, 2, 1): diagonal, three blocks, two ones above the diagonal. Different: both ones are now in one block, so the two forms are not similar.
> - A: The exponent was taken as the number of ones above the diagonal ($n_1-\nu_1=2$), not the largest block size.
> - B: The producer was thought not to matter, so the handout's sizes 2, 2, 1 were kept. Also the exponent was taken as the number of blocks (3).
> - D: The producer was thought not to matter: these are the sizes and $\psi$ of the handout's own case, where the two generalized eigenvectors come from two different eigenvectors.
