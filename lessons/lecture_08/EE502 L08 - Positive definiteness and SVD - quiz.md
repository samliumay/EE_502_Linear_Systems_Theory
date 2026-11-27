---
course: EE 502 Linear System Theory
lesson: EE502 L08 - Positive definiteness and SVD
type: quiz
questions: 12
---

# EE502 L08 - Positive definiteness and SVD - quiz

Lesson note: [[EE502 L08 - Positive definiteness and SVD]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. $M>0$ means positive definite and $M\ge 0$ positive semi-definite. $D_k$ is the $k$-th leading principal minor (determinant of the top-left $k\times k$ block). The SVD is $H=RSQ^{\mathsf T}$ with orthogonal $R$, $Q$, columns $\mathbf{r}_j$, $\mathbf{q}_j$, and $H\mathbf{q}_j=\sigma_j\mathbf{r}_j$.

## 1. Symmetric matrices (slides 81-82)

### Q1 (slide 81)

Fact 1 says a real symmetric $M$ has real eigenvalues. The proof takes $M\mathbf{v}=\lambda\mathbf{v}$ (with $\mathbf{v}$ possibly complex), writes $\mathbf{v}^*M\mathbf{v}=\lambda\lvert\mathbf{v}\rvert^2$ and shows that $\mathbf{v}^*M\mathbf{v}$ is real. The real matrix $A$ with the rows $(0,1)$ and $(-1,0)$ has the eigenvalues $\pm j$. Which step of the proof fails for this $A$?

- A) The step $\mathbf{v}^*\mathbf{v}=\lvert\mathbf{v}\rvert^2$ fails: for a complex $\mathbf{v}$ this number is not real.
- B) The step $A\mathbf{v}=\lambda\mathbf{v}$ fails: $A$ is not diagonalizable, so it has no eigenvector for $\lambda=\pm j$.
- C) The step $(\mathbf{v}^*A\mathbf{v})^*=\mathbf{v}^*A\mathbf{v}$ fails: it needs $A^{\mathsf T}=A$, but here $A^{\mathsf T}=-A$.
- D) The first step fails: the proof needs a real eigenvector $\mathbf{v}$, and this $A$ has no real eigenvector at all.

> [!success]- Answer
> **C.** $(\mathbf{v}^*A\mathbf{v})^*=\mathbf{v}^*A^{\mathsf T}\mathbf{v}$ for a real $A$. Only $A^{\mathsf T}=A$ turns this into $\mathbf{v}^*A\mathbf{v}$.
> Here $A^{\mathsf T}=-A$, so $(\mathbf{v}^*A\mathbf{v})^*=-\mathbf{v}^*A\mathbf{v}$. A number equal to minus its own conjugate is purely imaginary.
> So $\lambda=\mathbf{v}^*A\mathbf{v}/\lvert\mathbf{v}\rvert^2$ is purely imaginary. Check: $\Delta(\lambda)=\lambda^2+1$, $\lambda=\pm j$.
> - A: $\mathbf{v}^*\mathbf{v}=\sum_i\lvert v_i\rvert^2$ is real and positive for every $\mathbf{v}\ne\mathbf{0}$, complex or not.
> - B: The eigenvalues $\pm j$ are distinct, so $A$ is diagonalizable over $\mathbb{C}$ and has complex eigenvectors.
> - D: The proof allows a complex $\mathbf{v}$ (that is why it uses $\mathbf{v}^*$). A real eigenvector is a conclusion of Fact 1, not an assumption.

### Q2 (slide 82)

$M$ has the rows $(2,1,1)$, $(1,2,1)$ and $(1,1,2)$. You want $M=Q\Lambda Q^{\mathsf T}$ with an orthogonal $Q$. What are the eigenvalues of $M$, and where is Gram-Schmidt needed?

- A) Eigenvalues $3,0,0$. Gram-Schmidt inside the eigenspace of the double eigenvalue.
- B) Eigenvalues $4,1,1$. Gram-Schmidt between the simple eigenvalue's eigenvector and the double one's.
- C) Eigenvalues $3,0,0$. Gram-Schmidt between the simple eigenvalue's eigenvector and the double one's.
- D) Eigenvalues $4,1,1$. Gram-Schmidt inside the eigenspace of the double eigenvalue.

> [!success]- Answer
> **D.** Every row sums to $4$, so $(1,1,1)^{\mathsf T}$ is an eigenvector with $\lambda_1=4$.
> $M-I$ has all entries $1$ (rank 1), so $\lambda=1$ is a double eigenvalue with the eigenspace $x_1+x_2+x_3=0$. Trace check: $4+1+1=6$.
> Eigenvectors of distinct eigenvalues of a symmetric matrix are already perpendicular. Inside the plane, $\mathbf{v}_2=(1,-1,0)^{\mathsf T}$ and $\mathbf{v}_3=(1,0,-1)^{\mathsf T}$ have $\mathbf{v}_2^{\mathsf T}\mathbf{v}_3=1\ne0$: Gram-Schmidt is needed there. It gives $\mathbf{q}_3=\tfrac{1}{\sqrt6}(1,1,-2)^{\mathsf T}$.
> - A: $3,0,0$ are the eigenvalues of $M-I$. The shift by $1$ was forgotten.
> - B: For a symmetric $M$, eigenvectors of different eigenvalues are perpendicular by themselves: $(\lambda_j-\lambda_i)\mathbf{v}_j^{\mathsf T}\mathbf{v}_i=0$.
> - C: Both slips: eigenvalues of $M-I$, and Gram-Schmidt put where it is not needed.

## 2. Positive definite matrices (slides 83-84)

### Q3 (slide 83, a)

$M$ with the rows $(2,3)$ and $(-1,1)$ is not symmetric. Which symmetric matrix has the same quadratic form $\mathbf{x}^{\mathsf T}M\mathbf{x}$, and is the form positive for every $\mathbf{x}\ne\mathbf{0}$?

- A) The rows $(2,1)$ and $(1,1)$. The form is positive for every $\mathbf{x}\ne\mathbf{0}$.
- B) The rows $(2,2)$ and $(2,1)$. The form is positive for every $\mathbf{x}\ne\mathbf{0}$.
- C) The rows $(2,1)$ and $(1,1)$. The form is not positive for every $\mathbf{x}\ne\mathbf{0}$.
- D) The rows $(2,2)$ and $(2,1)$. The form is not positive for every $\mathbf{x}\ne\mathbf{0}$.

> [!success]- Answer
> **A.** $\mathbf{x}^{\mathsf T}M\mathbf{x}=2x_1^2+(3-1)x_1x_2+x_2^2=2x_1^2+2x_1x_2+x_2^2$.
> $M_s=\tfrac12(M+M^{\mathsf T})$ has the rows $(2,1)$ and $(1,1)$ and gives the same form.
> $2x_1^2+2x_1x_2+x_2^2=(x_1+x_2)^2+x_1^2$, zero only at $\mathbf{x}=\mathbf{0}$. Also $D_1=2$, $D_2=1$: $M_s>0$.
> - B: The cross coefficient $m_{12}+m_{21}=2$ was put in each off-diagonal entry instead of half of it (form $2x_1^2+4x_1x_2+x_2^2$). Then only $D_1=2>0$ was checked. $D_2=-2$.
> - C: The verdict came from $M$ itself: its eigenvalues $\tfrac{3\pm j\sqrt{11}}{2}$ are complex. The tests apply only to $M_s$, with eigenvalues $\tfrac{3\pm\sqrt5}{2}>0$.
> - D: The cross coefficient $2$ was not halved. That matrix has $D_2=2-4=-2$, but its form is not the form of $M$.

### Q4 (slide 83, b)

$M$ has the rows $(1,3)$ and $(3,a)$. Complete the square in $\mathbf{x}^{\mathsf T}M\mathbf{x}$. For which $a$ is $M>0$, for which $a$ is $M\ge0$, and which nonzero $\mathbf{x}$ gives a zero form in the boundary case?

- A) $M>0$ iff $a>9$, $M\ge0$ iff $a\ge9$. At $a=9$: $\mathbf{x}=(3,-1)^{\mathsf T}$.
- B) $M>0$ iff $a>9$, $M\ge0$ iff $a\ge9$. At $a=9$: $\mathbf{x}=(1,-3)^{\mathsf T}$.
- C) $M>0$ iff $a>3$, $M\ge0$ iff $a\ge3$. At $a=3$: $\mathbf{x}=(3,-1)^{\mathsf T}$.
- D) $M>0$ iff $a>3$, $M\ge0$ iff $a\ge3$. At $a=3$: $\mathbf{x}=(1,-3)^{\mathsf T}$.

> [!success]- Answer
> **A.** $\mathbf{x}^{\mathsf T}M\mathbf{x}=x_1^2+6x_1x_2+ax_2^2=(x_1+3x_2)^2+(a-9)x_2^2$.
> $a>9$: both terms are $\ge0$ and vanish together only at $\mathbf{x}=\mathbf{0}$. $a\ge9$: the form is never negative. Minors: $D_1=1$, $D_2=a-9$.
> At $a=9$ the form is $(x_1+3x_2)^2$, zero when $x_1=-3x_2$, for example $\mathbf{x}=(3,-1)^{\mathsf T}$.
> - B: The components were swapped when solving $x_1+3x_2=0$. At $a=9$, $\mathbf{x}=(1,-3)^{\mathsf T}$ gives $(1-9)^2=64$.
> - C: The square was completed with $3$ instead of $3^2=9$: $(a-3)x_2^2$. At $a=3$, $(3,-1)^{\mathsf T}$ gives $9-18+3=-6$.
> - D: Both slips.

### Q5 (slide 84, a)

$M$ has the rows $(2,-1,0)$, $(-1,2,-1)$ and $(0,-1,2)$. What are its leading principal minors $D_1,D_2,D_3$ and its eigenvalues?

- A) $D_k=2,3,6$. Eigenvalues $1,2,3$.
- B) $D_k=2,3,4$. Eigenvalues $1,2,3$.
- C) $D_k=2,3,4$. Eigenvalues $2,\ 2+\sqrt2,\ 2-\sqrt2$.
- D) $D_k=2,3,6$. Eigenvalues $2,\ 2+\sqrt2,\ 2-\sqrt2$.

> [!success]- Answer
> **C.** $D_1=2$, $D_2=4-1=3$, $D_3=2(4-1)-(-1)(-2-0)=6-2=4$.
> $\det(M-\lambda I)=(2-\lambda)\big[(2-\lambda)^2-1\big]-(2-\lambda)=(2-\lambda)\big[(2-\lambda)^2-2\big]$, so $\lambda=2,\ 2\pm\sqrt2$.
> Check: product $2\cdot(4-2)=4=D_3$. All minors and all eigenvalues are positive: $M>0$. Sum of squares: $x_1^2+(x_1-x_2)^2+(x_2-x_3)^2+x_3^2$.
> - A: The second cofactor term was dropped in both expansions: $D_3=2\cdot3=6$, and $(2-\lambda)\big[(2-\lambda)^2-1\big]$ gives $1,2,3$.
> - B: Right minors, but the term $-(2-\lambda)$ was dropped in $\det(M-\lambda I)$. Product $6\ne D_3=4$.
> - D: Right eigenvalues, but $D_3$ without its second cofactor term. The product of the eigenvalues is $4$, not $6$.

### Q6 (slide 84, b)

$M$ has the rows $(1,1,1)$, $(1,1,1)$ and $(1,1,0)$. Its leading principal minors are $1,0,0$. Is $M\ge0$, and why?

- A) Yes. All leading principal minors $1,0,0$ are $\ge0$, and that test decides $M\ge0$.
- B) No. $D_3=\det M=0$, so $M$ has a zero eigenvalue, and that rules out $M\ge0$.
- C) No. The principal minor with rows and columns $\{2,3\}$ is $1\cdot0-1\cdot1=-1<0$.
- D) Yes. All $1\times1$ principal minors (the diagonal $1,1,0$) are $\ge0$, so $M\ge0$.

> [!success]- Answer
> **C.** For $M\ge0$ all principal minors must be $\ge0$. Rows and columns $\{2,3\}$ give $-1$ (so does $\{1,3\}$).
> A vector that shows it: $\mathbf{x}=(0,1,-1)^{\mathsf T}$ gives $x_2^2+2x_2x_3=1-2=-1$.
> Eigenvalues: $0,\ 1+\sqrt3,\ 1-\sqrt3\approx-0.732$. $M$ is indefinite.
> - A: This is the slide's slip. Leading minors decide only $M>0$. For $M\ge0$ they are not enough.
> - B: A zero eigenvalue is allowed for $M\ge0$. It only rules out $M>0$. The conclusion is right, the reason is not.
> - D: Only part of the principal minors was checked. The $2\times2$ ones fail.

### Q7 (slide 84, c)

$M$ has the rows $(2,1)$ and $(1,2)$. The proof's recipe: $M=Q\Lambda Q^{\mathsf T}$ with $\Lambda=\operatorname{diag}(\lambda_1,\lambda_2)$, $\lambda_1\ge\lambda_2$, $Q$ orthogonal with unit eigenvectors as columns (first entry positive), $D=\operatorname{diag}(\sqrt{\lambda_1},\sqrt{\lambda_2})$ and $N=DQ^{\mathsf T}$, so that $M=N^{\mathsf T}N$. What is $N$?

- A) The rows $\big(\tfrac{\sqrt6}{2},\tfrac{\sqrt2}{2}\big)$ and $\big(\tfrac{\sqrt6}{2},-\tfrac{\sqrt2}{2}\big)$.
- B) The rows $\big(\tfrac{\sqrt6}{2},\tfrac{\sqrt6}{2}\big)$ and $\big(\tfrac{\sqrt2}{2},-\tfrac{\sqrt2}{2}\big)$.
- C) The rows $\big(\tfrac{3\sqrt2}{2},\tfrac{\sqrt2}{2}\big)$ and $\big(\tfrac{3\sqrt2}{2},-\tfrac{\sqrt2}{2}\big)$.
- D) The rows $\big(\tfrac{3\sqrt2}{2},\tfrac{3\sqrt2}{2}\big)$ and $\big(\tfrac{\sqrt2}{2},-\tfrac{\sqrt2}{2}\big)$.

> [!success]- Answer
> **B.** $\lambda=3,1$, $\mathbf{q}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$, $\mathbf{q}_2=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$, $D=\operatorname{diag}(\sqrt3,1)$.
> $N=DQ^{\mathsf T}$: row 1 is $\sqrt3\,\mathbf{q}_1^{\mathsf T}=\big(\sqrt{3/2},\sqrt{3/2}\big)=\big(\tfrac{\sqrt6}{2},\tfrac{\sqrt6}{2}\big)$, row 2 is $\mathbf{q}_2^{\mathsf T}$.
> Check: $N^{\mathsf T}N$ has the entries $\tfrac32+\tfrac12=2$ and $\tfrac32-\tfrac12=1$, so it is $M$. $\det N=-\sqrt3\ne0$: $N$ is nonsingular, as $M>0$ requires.
> - A: The product was taken as $QD$. Then $N^{\mathsf T}N=DQ^{\mathsf T}QD=D^2=\operatorname{diag}(3,1)\ne M$.
> - C: Order $QD$ and $D=\Lambda$ (square root forgotten). $N^{\mathsf T}N=\operatorname{diag}(9,1)$.
> - D: The square root was forgotten: $D=\operatorname{diag}(3,1)$. $N^{\mathsf T}N$ has the rows $(5,4)$ and $(4,5)$.

## 3. Singular values and the SVD (slides 85-87)

### Q8 (slide 85)

$H$ has the rows $(1,0,1)$ and $(0,1,1)$. $H^{\mathsf T}H$ has the eigenvalues $3,1,0$. What are the singular values of $H$ (in decreasing order), and how many of them are zero?

- A) $\sqrt3,\ 1,\ 0$. One singular value is zero.
- B) $3,\ 1$. No singular value is zero.
- C) $3,\ 1,\ 0$. One singular value is zero.
- D) $\sqrt3,\ 1$. No singular value is zero.

> [!success]- Answer
> **D.** $\sigma_j=\sqrt{\lambda_j(H^{\mathsf T}H)}$. $H$ is $2\times3$, so it has $\min\{2,3\}=2$ singular values: $\sqrt3\approx1.732$ and $1$.
> Both are nonzero, so $\operatorname{rank}H=2$, and the number of zero singular values is $\min\{m,n\}-r=0$.
> The eigenvalue $0$ of $H^{\mathsf T}H$ only says that $H$ has a null space of dimension $n-r=1$.
> - A: $n=3$ singular values were counted instead of $\min\{m,n\}=2$.
> - B: The square root was forgotten: the eigenvalues of $H^{\mathsf T}H$ were taken as singular values.
> - C: Both slips: no square root, and $n$ instead of $\min\{m,n\}$ values.

### Q9 (slide 86)

$A$ has the rows $(3,0)$ and $(4,5)$. Take its SVD $A=RSQ^{\mathsf T}$ with the singular values in decreasing order, the first entry of each $\mathbf{q}_j$ positive, and $\mathbf{r}_j=A\mathbf{q}_j/\sigma_j$. What are $S$ and the first column $\mathbf{r}_1$ of $R$?

- A) $S=\operatorname{diag}(45,5)$ and $\mathbf{r}_1=\tfrac{1}{\sqrt{10}}(1,3)^{\mathsf T}$.
- B) $S=\operatorname{diag}(3\sqrt5,\sqrt5)$ and $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$.
- C) $S=\operatorname{diag}(45,5)$ and $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$.
- D) $S=\operatorname{diag}(3\sqrt5,\sqrt5)$ and $\mathbf{r}_1=\tfrac{1}{\sqrt{10}}(1,3)^{\mathsf T}$.

> [!success]- Answer
> **D.** $A^{\mathsf T}A$ has the rows $(25,20)$ and $(20,25)$. $\Delta(\lambda)=(\lambda-45)(\lambda-5)$, so $\sigma_1=\sqrt{45}=3\sqrt5$, $\sigma_2=\sqrt5$.
> $\mathbf{q}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$. $A\mathbf{q}_1=\tfrac{1}{\sqrt2}(3,9)^{\mathsf T}$, divided by $3\sqrt5$: $\mathbf{r}_1=\tfrac{1}{\sqrt{10}}(1,3)^{\mathsf T}$.
> Also $\mathbf{q}_2=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$, $\mathbf{r}_2=\tfrac{1}{\sqrt{10}}(3,-1)^{\mathsf T}$, and $\sigma_1\mathbf{r}_1\mathbf{q}_1^{\mathsf T}+\sigma_2\mathbf{r}_2\mathbf{q}_2^{\mathsf T}=A$.
> - A: The square root was forgotten: the eigenvalues of $A^{\mathsf T}A$ were put into $S$.
> - B: $R$ and $Q$ were swapped: $\mathbf{q}_1$ (eigenvector of $A^{\mathsf T}A$) was used as $\mathbf{r}_1$.
> - C: Both slips.

### Q10 (slide 87)

$H$ has the rows $(1,2)$ and $(2,4)$ (rank 1). Its singular values are $5$ and $0$, $\mathbf{q}_1=\tfrac{1}{\sqrt5}(1,2)^{\mathsf T}$, $\mathbf{q}_2=\tfrac{1}{\sqrt5}(2,-1)^{\mathsf T}$, and $\mathbf{r}_1=H\mathbf{q}_1/\sigma_1=\tfrac{1}{\sqrt5}(1,2)^{\mathsf T}$. Why can $\mathbf{r}_2$ not come from the formula $\mathbf{r}_j=H\mathbf{q}_j/\sigma_j$, and how is it found?

- A) The formula gives $\mathbf{r}_2=H\mathbf{q}_2/\sigma_2=\mathbf{0}$. So the second column of $R$ is the zero vector.
- B) $H\mathbf{q}_2=\mathbf{0}$ and $\sigma_2=0$: the formula is $0/0$. Take a unit $\mathbf{r}_2$ with $\mathbf{r}_2\perp\mathbf{r}_1$.
- C) $\operatorname{rank}H=1$, so $R$ has only one column, and there is no $\mathbf{r}_2$ to find at all.
- D) $H\mathbf{q}_2$ is parallel to $\mathbf{r}_1$, so the formula repeats $\mathbf{r}_1$. Take $\mathbf{r}_2=-\mathbf{r}_1$.

> [!success]- Answer
> **B.** $H\mathbf{q}_2=\tfrac{1}{\sqrt5}(2-2,\ 4-4)^{\mathsf T}=\mathbf{0}$, and the formula divides by $\sigma_2=0$. It gives no direction.
> $R$ must be a $2\times2$ orthogonal matrix, so $\mathbf{r}_2$ is chosen as a unit vector perpendicular to $\mathbf{r}_1$: $\mathbf{r}_2=\tfrac{1}{\sqrt5}(2,-1)^{\mathsf T}$ (or its negative).
> Then $S=\operatorname{diag}(5,0)$ and $RSQ^{\mathsf T}=5\,\mathbf{r}_1\mathbf{q}_1^{\mathsf T}=H$.
> - A: A zero column makes $R$ singular, not orthogonal. $0/0$ is not $\mathbf{0}$.
> - C: In the full SVD $R$ is $m\times m=2\times2$. Only the thin form keeps one column.
> - D: $H\mathbf{q}_2=\mathbf{0}$, not a multiple of $\mathbf{r}_1$. Also $-\mathbf{r}_1$ is not perpendicular to $\mathbf{r}_1$.

## 4. Condition number (slide 88)

### Q11 (slide 88, a)

$A$ has the rows $(3,0)$ and $(4,5)$. Its condition number is $\kappa=\lVert A\rVert_2\,\lVert A^{-1}\rVert_2$ (matrix 2-norms). What is $\kappa$?

- A) $\kappa=5/3$
- B) $\kappa=3$
- C) $\kappa=10/3$
- D) $\kappa=9$

> [!success]- Answer
> **B.** $A^{\mathsf T}A$ has the eigenvalues $45$ and $5$, so $\sigma_1=3\sqrt5$ and $\sigma_2=\sqrt5$.
> $\lVert A\rVert_2=\sigma_1=3\sqrt5\approx6.708$ and $\lVert A^{-1}\rVert_2=1/\sigma_2=1/\sqrt5\approx0.447$. So $\kappa=\sigma_1/\sigma_2=3$.
> - A: The ratio of the eigenvalues $5$ and $3$ of $A$. $A$ is not symmetric, so $\sigma_j\ne\lvert\lambda_j\rvert$. Only the product agrees: $\sigma_1\sigma_2=15=\lvert\det A\rvert$.
> - C: Frobenius norms instead of 2-norms: $\lVert A\rVert_F=\sqrt{50}$, $\lVert A^{-1}\rVert_F=\sqrt{50}/15$, product $50/15=10/3$.
> - D: The square root was forgotten: $\lambda_1/\lambda_2$ of $A^{\mathsf T}A$ is $45/5=9=\kappa^2$.

### Q12 (slide 88, b)

$H$ has the rows $(1,0,1)$ and $(0,1,1)$. $H^{\mathsf T}H$ has the eigenvalues $3,1,0$. Without a new characteristic polynomial: what are the eigenvalues of $HH^{\mathsf T}$, and what is $\mathbf{r}_1$, the first column of $R$ in $H=RSQ^{\mathsf T}$ (singular values in decreasing order, first entry of $\mathbf{r}_1$ positive)?

- A) Eigenvalues $3,1$. $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$.
- B) Eigenvalues $3,1,0$. $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$.
- C) Eigenvalues $3,1$. $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$.
- D) Eigenvalues $3,1,0$. $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$.

> [!success]- Answer
> **A.** $HH^{\mathsf T}=R(SS^{\mathsf T})R^{\mathsf T}$ is $2\times2$ and shares the nonzero eigenvalues $\sigma_j^2$ with $H^{\mathsf T}H$: $3$ and $1$.
> Check: $HH^{\mathsf T}$ has the rows $(2,1)$ and $(1,2)$, trace $4=3+1$, determinant $3$.
> $\mathbf{r}_1$ is the unit eigenvector of $HH^{\mathsf T}$ for the largest eigenvalue $3=\sigma_1^2$: $\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$. The recipe agrees: $H\mathbf{q}_1/\sigma_1$ with $\mathbf{q}_1=\tfrac{1}{\sqrt6}(1,1,2)^{\mathsf T}$.
> - B: Both slips: the extra $0$, and the order taken as ascending.
> - C: The singular values were taken in ascending order (as the slide says), so $\mathbf{r}_1$ was matched with the eigenvalue $1$.
> - D: The extra $0$ belongs only to the $3\times3$ matrix $H^{\mathsf T}H$. A $2\times2$ matrix has two eigenvalues.
