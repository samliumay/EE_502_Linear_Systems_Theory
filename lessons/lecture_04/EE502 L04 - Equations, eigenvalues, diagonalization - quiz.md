---
course: EE 502 Linear System Theory
lesson: EE502 L04 - Equations, eigenvalues, diagonalization
type: quiz
questions: 14
---

# EE502 L04 - Equations, eigenvalues, diagonalization - quiz

Lesson note: [[EE502 L04 - Equations, eigenvalues, diagonalization]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz all vectors are column vectors. $(a,b,c)$ is short for $[a\ \ b\ \ c]^{\mathsf T}$. A matrix "with the rows" $(\dots)$ is written row by row.

## 1. Existence of solutions of Ax = y (slides 47-48)

### Q1 (slide 47)

$A$ has the rows $(1,2,1)$, $(2,4,3)$, $(3,6,4)$. Find $r(A)$ and decide whether $A\mathbf{x}=\mathbf{y}$ is solvable for $\mathbf{y}_1=(1,3,4)$ and for $\mathbf{y}_2=(1,3,5)$.

- A) $r(A)=1$. Not solvable for $\mathbf{y}_1$, solvable for $\mathbf{y}_2$.
- B) $r(A)=2$. Solvable for $\mathbf{y}_1$, not solvable for $\mathbf{y}_2$.
- C) $r(A)=1$. Solvable for $\mathbf{y}_1$, not solvable for $\mathbf{y}_2$.
- D) $r(A)=2$. Not solvable for $\mathbf{y}_1$, solvable for $\mathbf{y}_2$.

> [!success]- Answer
> **B.** Row 3 of $A$ is row 1 plus row 2, and rows 1 and 2 are not multiples of each other. So $r(A)=2$.
> $R_3\leftarrow R_3-R_1-R_2$ turns the last column into $y_3-y_1-y_2$.
> $\mathbf{y}_1$: $4-1-3=0$, so $r([A\ \ \mathbf{y}_1])=2=r(A)$: solvable. $\mathbf{y}_2$: $5-1-3=1\neq0$, a pivot in the last column, $r([A\ \ \mathbf{y}_2])=3$: no solution.
> Since $r(A)=2<m=3$, the system is not solvable for every $\mathbf{y}$.
> - A: Both parts are wrong: $r(A)=2$ (columns 1 and 3 are independent), and the solvable right side is $\mathbf{y}_1$.
> - C: Column 2 is twice column 1, but column 3 is not a multiple of column 1. Two columns are independent, so $r(A)=2$, not 1.
> - D: The rank is right, but the two results are swapped. The zero row needs $y_3-y_1-y_2=0$, which holds for $\mathbf{y}_1$ ($4-1-3=0$), not for $\mathbf{y}_2$.

### Q2 (slide 48)

$A$ is $3\times2$ with the rows $(1,0)$, $(0,1)$, $(1,1)$. For exactly one of $\mathbf{y}=(1,1,0)$ and $\mathbf{y}=(1,1,2)$ the system $A\mathbf{x}=\mathbf{y}$ is solvable. Which one, and how many solutions does it have?

- A) $\mathbf{y}=(1,1,0)$, with infinitely many solutions.
- B) $\mathbf{y}=(1,1,0)$, with exactly one solution.
- C) $\mathbf{y}=(1,1,2)$, with infinitely many solutions.
- D) $\mathbf{y}=(1,1,2)$, with exactly one solution.

> [!success]- Answer
> **D.** $r(A)=2$ (pivots in both columns). $R_3\leftarrow R_3-R_1-R_2$ gives the last entry $y_3-y_1-y_2$.
> $(1,1,0)$: $0-1-1=-2\neq0$, no solution. $(1,1,2)$: $2-1-1=0$, solvable with $x_1=1$, $x_2=1$.
> $\nu(A)=n-r(A)=2-2=0$ (full column rank), so this solution is the only one.
> - A: Both parts are wrong: $(1,1,0)$ gives the row $0=-2$, and $\nu(A)=n-r(A)=0$.
> - B: This comes from a sign slip, $R_3\leftarrow R_3-R_1+R_2$: then $0-1+1=0$. The correct step is $R_3-R_1-R_2$, which gives $-2$ for $(1,1,0)$.
> - C: The right side is right, but the nullity is $n-r(A)=2-2=0$, not $m-r(A)=1$. The solution is unique.

## 2. The set of all solutions (slides 49-51)

### Q3 (slide 49)

$A$ has the rows $(1,1,1)$, $(1,2,3)$ and $\mathbf{y}=(6,14)$. Both $\mathbf{x}_a=(1,2,3)$ and $\mathbf{x}_b=(3,-2,5)$ solve $A\mathbf{x}=\mathbf{y}$. Write all solutions as $\mathbf{x}=\mathbf{x}_a+\alpha\,\mathbf{n}_1$, with $\mathbf{n}_1$ a null-space vector whose third entry is 1. Which $\mathbf{n}_1$, and which $\alpha$ gives $\mathbf{x}_b$?

- A) $\mathbf{n}_1=(-3,2,1)$ and $\alpha=-2$.
- B) $\mathbf{n}_1=(1,-2,1)$ and $\alpha=-2$.
- C) $\mathbf{n}_1=(1,-2,1)$ and $\alpha=2$.
- D) $\mathbf{n}_1=(-3,2,1)$ and $\alpha=2$.

> [!success]- Answer
> **C.** $r(A)=2$, so $\nu(A)=3-2=1$: one free parameter.
> Null space: subtract the equations, $x_2+2x_3=0$, so $x_2=-2x_3$ and $x_1=-x_2-x_3=x_3$. With $x_3=1$: $\mathbf{n}_1=(1,-2,1)$.
> $\mathbf{x}_b-\mathbf{x}_a=(2,-4,2)=2\,\mathbf{n}_1$, so $\alpha=2$.
> - A: Two slips: $x_2=+2x_3$ gives $(-3,2,1)$, which is not a null vector (row 2 gives $4$), and $\alpha=-2$ comes from $\mathbf{x}_a-\mathbf{x}_b$.
> - B: The null vector is right, but $\alpha=-2$ comes from $\mathbf{x}_a-\mathbf{x}_b$. We need $\mathbf{x}_b=\mathbf{x}_a+\alpha\mathbf{n}_1$, so $\alpha\mathbf{n}_1=\mathbf{x}_b-\mathbf{x}_a$.
> - D: Sign slip: $x_2=+2x_3$ instead of $-2x_3$. Check with row 2: $-3+4+3=4\neq0$, so $(-3,2,1)$ is not in $\mathcal{N}(A)$.

### Q4 (slide 50)

$[A\ \ \mathbf{y}]$ has the rows $(1,2,1,3\mid4)$, $(2,4,3,8\mid9)$, $(1,2,2,5\mid5)$. Let $\tilde R$ be the reduced row echelon form of $A$ and $P$ the matrix that swaps columns 2 and 3. Then $\tilde RP=\begin{bmatrix}I_2&B\\0&0\end{bmatrix}$. Which $B$, and is the system solvable?

- A) $B=\begin{bmatrix}2&1\\0&2\end{bmatrix}$, and the system is solvable.
- B) $B=\begin{bmatrix}0&1\\1&2\end{bmatrix}$, and the system is solvable.
- C) $B=\begin{bmatrix}0&1\\1&2\end{bmatrix}$, and the system is not solvable.
- D) $B=\begin{bmatrix}2&1\\0&2\end{bmatrix}$, and the system is not solvable.

> [!success]- Answer
> **A.** $R_2\leftarrow R_2-2R_1$ and $R_3\leftarrow R_3-R_1$ both give $(0,0,1,2\mid1)$. $R_3\leftarrow R_3-R_2$ gives a zero row. $R_1\leftarrow R_1-R_2$ gives $(1,2,0,1\mid3)$.
> Pivots in columns 1 and 3, $r(A)=2$. Basic: $x_1,x_3$. Free: $x_2,x_4$.
> Swap columns 2 and 3: $\tilde RP$ has the rows $(1,0,2,1)$, $(0,1,0,2)$, $(0,0,0,0)$, so $B=\begin{bmatrix}2&1\\0&2\end{bmatrix}$.
> The last row is $(0,0,0,0\mid0)$: no pivot in the last column, $r([A\ \ \mathbf{y}])=2=r(A)$. Solvable.
> - B: This is columns 3 and 4 of $\tilde R$, read without the swap $P$. The pivot columns must come first.
> - C: $P$ was forgotten, and a zero row with a zero right side does not block a solution.
> - D: $B$ is right, but a zero row $(0\ 0\ 0\ 0\mid0)$ is harmless. Only a row $(0\ 0\ 0\ 0\mid c)$ with $c\neq0$ means no solution.

### Q5 (slide 51)

$[A\ \ \mathbf{y}]$ has the rows $(1,2,1,3\mid4)$, $(2,4,3,8\mid9)$, $(1,2,2,5\mid5)$. Write all solutions as $\mathbf{x}=\mathbf{x}_p+x_2\mathbf{n}_1+x_4\mathbf{n}_2$, where $x_2,x_4$ are the free unknowns and $\mathbf{x}_p$ has $x_2=x_4=0$. Which option is right?

- A) $\mathbf{x}_p=(3,1,0,0)$, $\mathbf{n}_1=(2,1,0,0)$, $\mathbf{n}_2=(1,0,2,1)$
- B) $\mathbf{x}_p=(3,0,1,0)$, $\mathbf{n}_1=(-2,1,0,0)$, $\mathbf{n}_2=(-1,0,-2,1)$
- C) $\mathbf{x}_p=(3,1,0,0)$, $\mathbf{n}_1=(-2,1,0,0)$, $\mathbf{n}_2=(-1,0,-2,1)$
- D) $\mathbf{x}_p=(3,0,1,0)$, $\mathbf{n}_1=(2,1,0,0)$, $\mathbf{n}_2=(1,0,2,1)$

> [!success]- Answer
> **B.** Reduced rows: $x_1+2x_2+x_4=3$ and $x_3+2x_4=1$. So $x_1=3-2x_2-x_4$ and $x_3=1-2x_4$.
> Constant part: $\mathbf{x}_p=(3,0,1,0)$. Coefficient of $x_2$: $(-2,1,0,0)$. Coefficient of $x_4$: $(-1,0,-2,1)$.
> Check with row 1 of $A$, $(1,2,1,3)$: $3+1=4$, $-2+2=0$, $-1-2+3=0$.
> - A: $\mathbf{x}_p$ is not swapped back with $P$, and the null vectors use $+B$ instead of $-B$.
> - C: The null vectors are right, but $\mathbf{x}_p$ is written in the order $(x_1,x_3,x_2,x_4)$ and not swapped back. Row 1: $3+2=5\neq4$.
> - D: $\mathbf{x}_p$ is right, but the null vectors use $+B$ instead of $-B$. Row 1 of $A$ gives $2+2=4\neq0$ for $(2,1,0,0)$.

## 3. Determinants and inverses (slides 52-53)

### Q6 (slide 52)

$A$ has the rows $(2,0,1)$, $(1,3,0)$, $(0,1,4)$. Compute $\det A$ with Laplace's formula along column 2.

- A) $\det A=23$
- B) $\det A=-25$
- C) $\det A=25$
- D) $\det A=9$

> [!success]- Answer
> **C.** Column 2 is $(0,3,1)$, so $\det A=0\cdot c_{12}+3c_{22}+1\cdot c_{32}$.
> $c_{22}=(+1)\det\begin{bmatrix}2&1\\0&4\end{bmatrix}=8$. $c_{32}=(-1)\det\begin{bmatrix}2&1\\1&0\end{bmatrix}=-(0-1)=1$.
> $\det A=3\cdot8+1\cdot1=25\neq0$, so the columns are linearly independent.
> - A: The sign $(-1)^{3+2}=-1$ of $c_{32}$ was dropped: the minor $-1$ was used instead of the cofactor $+1$. $3\cdot8-1=23$.
> - B: Each $2\times2$ determinant was computed as $bc-ad$ instead of $ad-bc$: $c_{22}=-8$, $c_{32}=-1$, so $-24-1=-25$.
> - D: The cofactors were added without the entries $a_{i2}$: $c_{22}+c_{32}=8+1=9$. Each cofactor must be multiplied by its entry.

### Q7 (slide 53)

$A$ is upper triangular with the rows $(2,1,0)$, $(0,1,3)$, $(0,0,4)$, so $\det A=8$. Which matrix is $A^{-1}=\operatorname{adj}A/\det A$?

- A) $\begin{bmatrix}\tfrac12&\tfrac12&\tfrac38\\0&1&\tfrac34\\0&0&\tfrac14\end{bmatrix}$
- B) $\begin{bmatrix}\tfrac12&0&0\\\tfrac12&1&0\\\tfrac38&\tfrac34&\tfrac14\end{bmatrix}$
- C) $\begin{bmatrix}\tfrac12&0&0\\-\tfrac12&1&0\\\tfrac38&-\tfrac34&\tfrac14\end{bmatrix}$
- D) $\begin{bmatrix}\tfrac12&-\tfrac12&\tfrac38\\0&1&-\tfrac34\\0&0&\tfrac14\end{bmatrix}$

> [!success]- Answer
> **D.** Cofactors $c_{ij}=(-1)^{i+j}\det M_{ij}$: $c_{11}=4$, $c_{21}=-4$, $c_{22}=8$, $c_{31}=3$, $c_{32}=-6$, $c_{33}=2$, the others are 0.
> $\operatorname{adj}A=[c_{ij}]^{\mathsf T}$ has the rows $(4,-4,3)$, $(0,8,-6)$, $(0,0,2)$. Divide by 8.
> As the Fact predicts, $A^{-1}$ is upper triangular with diagonal $1/a_{ii}$: $\tfrac12,1,\tfrac14$.
> - A: The signs $(-1)^{i+j}$ were dropped: minors were used instead of cofactors. Check: row 1 times column 2 of $A$ gives $\tfrac12+\tfrac12=1\neq0$.
> - B: Two slips: no signs $(-1)^{i+j}$ and no transpose. The result is not even upper triangular.
> - C: This is $[c_{ij}]/8$, without the transpose. The inverse of an upper triangular matrix must be upper triangular.

## 4. Similarity transformation and companion form (slides 54-55)

### Q8 (slide 54)

$A$ has the rows $(0,1)$, $(-2,-3)$. The new basis is $\mathbf{q}_1=(1,0)$, $\mathbf{q}_2=(1,-1)$, and $Q=[\mathbf{q}_1\ \ \mathbf{q}_2]$. Which matrix is $\hat A$ with $AQ=Q\hat A$?

- A) $\begin{bmatrix}-2&2\\0&-1\end{bmatrix}$
- B) $\begin{bmatrix}-2&0\\2&-1\end{bmatrix}$
- C) $\begin{bmatrix}0&-1\\-2&1\end{bmatrix}$
- D) $\begin{bmatrix}2&0\\-2&-1\end{bmatrix}$

> [!success]- Answer
> **B.** Column $i$ of $\hat A$ holds the coordinates of $A\mathbf{q}_i$ in the basis $\mathbf{q}_1,\mathbf{q}_2$.
> $A\mathbf{q}_1=(0,-2)=\alpha_1\mathbf{q}_1+\alpha_2\mathbf{q}_2=(\alpha_1+\alpha_2,-\alpha_2)$, so $\alpha_2=2$, $\alpha_1=-2$.
> $A\mathbf{q}_2=(-1,1)=-\mathbf{q}_2$, so column 2 is $(0,-1)$.
> Check: trace $-3$ and determinant $2$, the same as for $A$.
> - A: The coordinate vectors were written as rows instead of columns. This is $\hat A^{\mathsf T}$. Trace and determinant agree, so that check does not catch it: check $AQ=Q\hat A$.
> - C: This is $AQ$: the images $A\mathbf{q}_i$ in the natural basis, not written in the $\mathbf{q}$'s. Its trace is $1\neq-3$.
> - D: Sign slip in column 1: $\alpha_2=-2$, $\alpha_1=2$ gives $(2,-2)=2\mathbf{q}_1-2\mathbf{q}_2=(0,2)\neq A\mathbf{q}_1$. Its trace is $1\neq-3$.

### Q9 (slide 55)

$A$ has the rows $(1,2)$, $(3,4)$ and $\mathbf{b}=(1,0)$. With $Q=[\mathbf{b}\ \ A\mathbf{b}]$ and $A^2\mathbf{b}=\beta_1\mathbf{b}+\beta_2A\mathbf{b}$, the companion matrix is $B=\begin{bmatrix}0&\beta_1\\1&\beta_2\end{bmatrix}$. Which $B$, and which characteristic polynomial does $B$ have?

- A) $B=\begin{bmatrix}0&2\\1&5\end{bmatrix}$, polynomial $s^2-5s-2$
- B) $B=\begin{bmatrix}0&5\\1&2\end{bmatrix}$, polynomial $s^2-5s-2$
- C) $B=\begin{bmatrix}0&5\\1&2\end{bmatrix}$, polynomial $s^2+5s+2$
- D) $B=\begin{bmatrix}0&2\\1&5\end{bmatrix}$, polynomial $s^2+5s+2$

> [!success]- Answer
> **A.** $A\mathbf{b}=(1,3)$ and $A^2\mathbf{b}=A(1,3)=(7,15)$.
> $(\beta_1+\beta_2,\ 3\beta_2)=(7,15)$: $\beta_2=5$, $\beta_1=2$.
> The polynomial is $s^2-\beta_2s-\beta_1=s^2-5s-2$. Check with $A$: $s^2-(\operatorname{tr}A)s+\det A=s^2-5s-2$.
> - B: The polynomial is right, but $\beta_1=2$ and $\beta_2=5$ are swapped in $B$. The last column of $B$ is $(\beta_1,\beta_2)$.
> - C: $\beta_1$ and $\beta_2$ are swapped in $B$, and the signs of the polynomial are wrong. The polynomial of $B$ is $s^2-\beta_2s-\beta_1$.
> - D: $B$ is right, but the polynomial was written as $s^2+\beta_2s+\beta_1$. Then $\operatorname{tr}A=1+4=5$ would need $-5s$.

## 5. Eigenvalues and eigenvectors (slide 56)

### Q10 (slide 56)

$A$ has the rows $(1,2,0)$, $(4,3,0)$, $(1,0,2)$. Which option gives the eigenvalues of $A$ in increasing order and an eigenvector for $\lambda=-1$ with third entry 1?

- A) $-4,\ -1,\ 2$; eigenvector $(3,-3,1)$
- B) $-4,\ -1,\ 2$; eigenvector $(-3,3,1)$
- C) $-1,\ 2,\ 5$; eigenvector $(3,-3,1)$
- D) $-1,\ 2,\ 5$; eigenvector $(-3,3,1)$

> [!success]- Answer
> **D.** Expand $\det(\lambda I-A)$ along column 3: $\Delta=(\lambda-2)[(\lambda-1)(\lambda-3)-8]=(\lambda-2)(\lambda^2-4\lambda-5)=(\lambda-2)(\lambda-5)(\lambda+1)$.
> $\lambda=-1$: $A+I$ has the rows $(2,2,0)$, $(4,4,0)$, $(1,0,3)$. So $x_2=-x_1$ and $x_1=-3x_3$. With $x_3=1$: $(-3,3,1)$.
> Checks: $-1+2+5=6=\operatorname{tr}A$ and $(-1)\cdot2\cdot5=-10=\det A$.
> - A: Trace and determinant of the block were swapped, and the sign of $x_1$ in the eigenvector is wrong.
> - B: In the $2\times2$ block, trace and determinant were swapped: $\lambda^2+5\lambda+4$ instead of $\lambda^2-4\lambda-5$. The sum $-3$ does not match $\operatorname{tr}A=6$.
> - C: The eigenvalues are right, but row 3 of $A+I$, $x_1+3x_3=0$, gives $x_1=-3$, not $3$. $(A+I)(3,-3,1)=(0,0,6)\neq\mathbf{0}$.

## 6. Diagonalization, distinct eigenvalues (slides 57-58)

### Q11 (slide 57)

$A$ is $3\times3$ with eigenvalues $\lambda_1=1$, $\lambda_2=2$, $\lambda_3=4$ and eigenvectors $\mathbf{q}_1,\mathbf{q}_2,\mathbf{q}_3$. Apply $(A-\lambda_1I)(A-\lambda_3I)$ to $\alpha_1\mathbf{q}_1+\alpha_2\mathbf{q}_2+\alpha_3\mathbf{q}_3=\mathbf{0}$. What remains, and what happens if $\lambda_3=2$ instead?

- A) $2\alpha_2\mathbf{q}_2=\mathbf{0}$. If $\lambda_3=2$, the factor is 0, but $\mathbf{q}_2\neq\mathbf{0}$ still gives $\alpha_2=0$.
- B) $-2\alpha_2\mathbf{q}_2=\mathbf{0}$. If $\lambda_3=2$, the factor is 0, but $\mathbf{q}_2\neq\mathbf{0}$ still gives $\alpha_2=0$.
- C) $-2\alpha_2\mathbf{q}_2=\mathbf{0}$. If $\lambda_3=2$, the factor is 0 and says nothing about $\alpha_2$.
- D) $2\alpha_2\mathbf{q}_2=\mathbf{0}$. If $\lambda_3=2$, the factor is 0 and says nothing about $\alpha_2$.

> [!success]- Answer
> **C.** $(A-\lambda_jI)\mathbf{q}_i=(\lambda_i-\lambda_j)\mathbf{q}_i$. The $\mathbf{q}_1$ and $\mathbf{q}_3$ terms die.
> $\mathbf{q}_2$ term: $(\lambda_2-\lambda_1)(\lambda_2-\lambda_3)=(2-1)(2-4)=-2$. So $-2\alpha_2\mathbf{q}_2=\mathbf{0}$ and $\alpha_2=0$.
> With $\lambda_3=2$: $(2-1)(2-2)=0$, the equation is $\mathbf{0}=\mathbf{0}$. That is why Case 2 needs its own study.
> - A: The sign of the factor is wrong ($\lambda_2-\lambda_3=-2$), and a zero factor gives no information about $\alpha_2$.
> - B: The first part is right. But $0\cdot\alpha_2\mathbf{q}_2=\mathbf{0}$ holds for every $\alpha_2$, so it gives no information.
> - D: Sign slip: the factor $(A-\lambda_3I)$ was read as $\lambda_3-\lambda_2=2$ instead of $\lambda_2-\lambda_3=-2$. The second part is right.

### Q12 (slide 58)

$A$ has the rows $(0,1)$, $(-5,-2)$. Let $\mathbf{q}$ be the eigenvector with first entry 1 for the eigenvalue with positive imaginary part, and $Q_r=[\operatorname{Re}\mathbf{q}\ \ \operatorname{Im}\mathbf{q}]$. Which option gives the eigenvalues and $Q_r^{-1}AQ_r$?

- A) $\lambda=-1\pm2i$; $Q_r^{-1}AQ_r=\begin{bmatrix}-1&-2\\2&-1\end{bmatrix}$
- B) $\lambda=-1\pm2i$; $Q_r^{-1}AQ_r=\begin{bmatrix}-1&2\\-2&-1\end{bmatrix}$
- C) $\lambda=1\pm2i$; $Q_r^{-1}AQ_r=\begin{bmatrix}1&2\\-2&1\end{bmatrix}$
- D) $\lambda=1\pm2i$; $Q_r^{-1}AQ_r=\begin{bmatrix}1&-2\\2&1\end{bmatrix}$

> [!success]- Answer
> **B.** $\Delta=\lambda^2-(\operatorname{tr}A)\lambda+\det A=\lambda^2+2\lambda+5$, so $\lambda=-1\pm2i$.
> $\lambda=-1+2i$: row 1 gives $q_2=\lambda q_1$, so $\mathbf{q}=(1,-1+2i)$, $\operatorname{Re}\mathbf{q}=(1,-1)$, $\operatorname{Im}\mathbf{q}=(0,2)$.
> $\sigma=-1$, $\omega=2$: the modal form is $\begin{bmatrix}\sigma&\omega\\-\omega&\sigma\end{bmatrix}=\begin{bmatrix}-1&2\\-2&-1\end{bmatrix}$. Check: $AQ_r$ and $Q_r$ times this block both have the rows $(-1,2)$, $(-3,-4)$.
> - A: This is what the conjugate eigenvector $(1,-1-2i)$ gives ($\omega=-2$). The stem asks for the eigenvalue with positive imaginary part.
> - C: Sign slip in $\Delta$: $\lambda^2+(\operatorname{tr}A)\lambda+\det A=\lambda^2-2\lambda+5$. The real part must be $\operatorname{tr}A/2=-1$.
> - D: The trace sign is wrong ($\sigma=\operatorname{tr}A/2=-1$), and the block has the sign of $\omega$ of the conjugate eigenvector.

## 7. Diagonalization, repeated eigenvalues (slides 59-60)

### Q13 (slide 59)

$A$ has the rows $(3,0,2)$, $(0,2,0)$, $(1,0,4)$, with $\Delta(\lambda)=(\lambda-2)^2(\lambda-5)$. Give the geometric multiplicity of $\lambda=2$, say whether $A$ is diagonalizable, and give the eigenvector for $\lambda=5$ with first entry 1.

- A) Geometric multiplicity 1, not diagonalizable, eigenvector $(1,0,-1)$.
- B) Geometric multiplicity 2, diagonalizable, eigenvector $(1,0,-1)$.
- C) Geometric multiplicity 1, not diagonalizable, eigenvector $(1,0,1)$.
- D) Geometric multiplicity 2, diagonalizable, eigenvector $(1,0,1)$.

> [!success]- Answer
> **D.** $A-2I$ has the rows $(1,0,2)$, $(0,0,0)$, $(1,0,2)$. Rank 1, nullity $3-1=2$: geometric = algebraic = 2.
> $\lambda=5$ is simple, so its multiplicities are both 1. So $A$ is diagonalizable, with $\Lambda=\operatorname{diag}\{2,2,5\}$.
> $A-5I$ has the rows $(-2,0,2)$, $(0,-3,0)$, $(1,0,-1)$: $x_2=0$, $x_3=x_1$. So $(1,0,1)$.
> - A: The rank of $A-2I$ is 1 (two equal rows), so the nullity is 2. The sign of $x_3$ in the eigenvector is also wrong.
> - B: The first two parts are right, but row 3 of $A-5I$ gives $x_3=x_1$, not $-x_1$. $(A-5I)(1,0,-1)=(-4,0,2)\neq\mathbf{0}$.
> - C: $A-2I$ has two equal nonzero rows, so its rank is 1, not 2. The nullity is 2, which equals the algebraic multiplicity.

### Q14 (slide 60)

$A(k)$ has the rows $(2,k,0)$, $(0,2,0)$, $(1,0,5)$. Its characteristic polynomial is $(\lambda-2)^2(\lambda-5)$ for every real $k$. For which $k$ is $A(k)$ diagonalizable?

- A) Only for $k=0$.
- B) For no real $k$.
- C) For every $k\neq0$.
- D) For every real $k$.

> [!success]- Answer
> **A.** Only the double eigenvalue 2 can fail. $A(k)-2I$ has the rows $(0,k,0)$, $(0,0,0)$, $(1,0,3)$.
> $k=0$: rank 1, nullity 2 = algebraic multiplicity 2. Diagonalizable.
> $k\neq0$: rows $(0,k,0)$ and $(1,0,3)$ are independent, rank 2, nullity 1 < 2. Not diagonalizable.
> - B: A repeated eigenvalue does not forbid a diagonal form. For $k=0$ the nullity of $A-2I$ is 2, equal to the multiplicity.
> - C: This reverses the cases. For $k\neq0$, $A(k)-2I$ has rank 2 and only one eigenvector for $\lambda=2$.
> - D: The same $\Delta(\lambda)$ does not mean the same eigenvectors. For $k\neq0$ the nullity of $A(k)-2I$ is only 1.
