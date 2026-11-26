---
course: EE 502 Linear System Theory
lecture: 8
title: Positive definiteness and SVD
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 81-88)
full_notes: lecture_notes/lecture_08/EE502_Lecture_08_PosDef_SVD.pdf
---
# EE 502 · Lecture 8 · Positive definiteness and SVD

> [!summary] In short
> - A real symmetric matrix has real eigenvalues and an orthonormal set of eigenvectors: $M=Q\Lambda Q^{\mathsf T}$ with $Q^{-1}=Q^{\mathsf T}$.
> - $M>0$ (positive definite) means $\mathbf{x}^{\mathsf T}M\mathbf{x}>0$ for every $\mathbf{x}\ne\mathbf{0}$. Three equivalent tests: eigenvalues $>0$, leading principal minors $>0$, $M=N^{\mathsf T}N$ with $N$ nonsingular.
> - Every $H\in\mathbb{R}^{m\times n}$ factors as $H=RSQ^{\mathsf T}$ (SVD). The singular values are $\sigma_j=\sqrt{\lambda_j(H^{\mathsf T}H)}\ge 0$.
> - Condition number $\kappa=\sigma_1/\sigma_n\ge 1$: how much a relative error in $\mathbf{b}$ can grow in the solution of $A\mathbf{x}=\mathbf{b}$.
> - The slides have three slips (semi-definite minors test, "ascending" order, $\sigma_n=\lVert A^{-1}\rVert_2$). See the warnings.

Slide numbers below are pages of the 220-page ABO file. Midterm material, not in Quiz 3.

## 1. Symmetric matrices (slides 81-82)
![[ee502_eee501alllecturenotesabo_p081.jpg]]
![[ee502_eee501alllecturenotesabo_p082.jpg]]

**Notes.** $M$ is symmetric when $M=M^{\mathsf T}$. Notation: $\mathbf{v}^*$ is the conjugate transpose of $\mathbf{v}$, and $\mathbf{v}^*\mathbf{v}=\lvert\mathbf{v}\rvert^2$.

- **Fact 1.** Eigenvalues are real, eigenvectors can be chosen real, and $M$ is diagonalizable.
  - Real: from $M\mathbf{v}=\lambda\mathbf{v}$, $\mathbf{v}^*M\mathbf{v}=\lambda\lvert\mathbf{v}\rvert^2$. The number $\mathbf{v}^*M\mathbf{v}$ equals its own conjugate (because $M^*=M$), so it is real, and so is $\lambda$.
  - Diagonalizable: a grade-2 generalized eigenvector $\mathbf{v}$ would give $\mathbf{w}=(M-\lambda I)\mathbf{v}\ne\mathbf{0}$ with $\mathbf{w}^*\mathbf{w}=\mathbf{v}^*(M-\lambda I)^2\mathbf{v}=0$. Contradiction.
- **Fact 2 (spectral theorem).** There is a real orthogonal $Q$ ($Q^{\mathsf T}Q=I$) with
$$M=Q\,\operatorname{diag}\{\lambda_1,\dots,\lambda_n\}\,Q^{\mathsf T}=\sum_{j=1}^{n}\lambda_j\,\mathbf{q}_j\mathbf{q}_j^{\mathsf T}.$$
  Eigenvectors of distinct eigenvalues are perpendicular: $(\lambda_j-\lambda_i)\mathbf{v}_j^{\mathsf T}\mathbf{v}_i=0$. Inside one eigenspace use Gram-Schmidt.

> [!example] $M=\begin{bmatrix}2&1\\1&2\end{bmatrix}$
> $\Delta(\lambda)=\lambda^2-4\lambda+3$, so $\lambda=3,1$. Unit eigenvectors $\mathbf{q}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$, $\mathbf{q}_2=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$, and $\mathbf{q}_1^{\mathsf T}\mathbf{q}_2=0$. So $Q=\tfrac{1}{\sqrt2}\begin{bmatrix}1&1\\1&-1\end{bmatrix}$, $\Lambda=\operatorname{diag}(3,1)$.

> [!question]- Check (slide 81): The real matrix $A$ with the rows $(0,1)$ and $(-1,0)$ has the eigenvalues $\pm j$. Which step of the proof of Fact 1 (i) fails for this $A$?
> The proof uses $(\mathbf{v}^*M\mathbf{v})^*=\mathbf{v}^*M^{\mathsf T}\mathbf{v}=\mathbf{v}^*M\mathbf{v}$. The last equality needs $M^{\mathsf T}=M$.
> Here $A^{\mathsf T}=-A$, so $(\mathbf{v}^*A\mathbf{v})^*=-\mathbf{v}^*A\mathbf{v}$. A number that equals minus its own conjugate is purely imaginary, not real.
> So $\lambda=\mathbf{v}^*A\mathbf{v}/\lvert\mathbf{v}\rvert^2$ is purely imaginary. Check: $\Delta(\lambda)=\lambda^2+1$, $\lambda=\pm j$.

> [!question]- Check (slide 82): Orthogonally diagonalize $M$ with the rows $(2,1,1)$, $(1,2,1)$ and $(1,1,2)$. Where do you need Gram-Schmidt?
> Every row sums to $4$, so $\mathbf{v}_1=(1,1,1)^{\mathsf T}$ is an eigenvector with $\lambda_1=4$. Unit vector: $\mathbf{q}_1=\tfrac{1}{\sqrt3}(1,1,1)^{\mathsf T}$.
> $M-I$ has all entries $1$ (rank 1), so $\lambda=1$ is a double eigenvalue. Its eigenspace is the plane $x_1+x_2+x_3=0$. Trace check: $4+1+1=6$.
> Two independent vectors in the plane: $\mathbf{v}_2=(1,-1,0)^{\mathsf T}$, $\mathbf{v}_3=(1,0,-1)^{\mathsf T}$. They are both perpendicular to $\mathbf{q}_1$ (distinct eigenvalues), but $\mathbf{v}_2^{\mathsf T}\mathbf{v}_3=1\ne 0$. Gram-Schmidt is needed inside this eigenspace.
> $\mathbf{q}_2=\tfrac{1}{\sqrt2}(1,-1,0)^{\mathsf T}$. Then $\mathbf{v}_3-(\mathbf{q}_2^{\mathsf T}\mathbf{v}_3)\mathbf{q}_2=(1,0,-1)^{\mathsf T}-\tfrac12(1,-1,0)^{\mathsf T}=(\tfrac12,\tfrac12,-1)^{\mathsf T}$, so $\mathbf{q}_3=\tfrac{1}{\sqrt6}(1,1,-2)^{\mathsf T}$.
> $Q=[\mathbf{q}_1\ \mathbf{q}_2\ \mathbf{q}_3]$, $Q^{\mathsf T}Q=I$ and $Q^{\mathsf T}MQ=\operatorname{diag}(4,1,1)$.

## 2. Positive definite matrices (slides 83-84)
![[ee502_eee501alllecturenotesabo_p083.jpg]]
![[ee502_eee501alllecturenotesabo_p084.jpg]]

**Notes.** For symmetric $M$: positive definite ($M>0$) if $\mathbf{x}^{\mathsf T}M\mathbf{x}>0$ for all $\mathbf{x}\ne\mathbf{0}$; positive semi-definite ($M\ge 0$) if $\mathbf{x}^{\mathsf T}M\mathbf{x}\ge 0$ for all $\mathbf{x}$. "$M>0$" does not mean positive entries.

**Fact 3.** For symmetric $M$, $M>0$ is equivalent to each of:
1. every eigenvalue is positive;
2. every leading principal minor $D_k$ (determinant of the top-left $k\times k$ block) is positive (Sylvester's criterion);
3. $M=N^{\mathsf T}N$ for a square nonsingular $N$.

Proof chain to know: $M>0\Rightarrow$ (1) by taking $\mathbf{x}=Q\mathbf{e}_j$, which gives $\mathbf{x}^{\mathsf T}M\mathbf{x}=\lambda_j$. (1) $\Rightarrow$ (3) with $N=DQ^{\mathsf T}$, $D=\operatorname{diag}\{\sqrt{\lambda_j}\}$. (3) $\Rightarrow M>0$ because $\mathbf{x}^{\mathsf T}N^{\mathsf T}N\mathbf{x}=\lVert N\mathbf{x}\rVert^2>0$.

> [!example] Slide example: $M=\begin{bmatrix}1&-1\\-1&a\end{bmatrix}$
> $\mathbf{x}^{\mathsf T}M\mathbf{x}=x_1^2-2x_1x_2+ax_2^2=(x_1-x_2)^2+(a-1)x_2^2$.
> So $M>0$ iff $a>1$, and $M\ge 0$ iff $a\ge 1$.
> Same answer from the minors: $D_1=1$, $D_2=a-1$.

Also useful: if $M>0$ then $\lambda_{\min}\lVert\mathbf{x}\rVert^2\le\mathbf{x}^{\mathsf T}M\mathbf{x}\le\lambda_{\max}\lVert\mathbf{x}\rVert^2$, $\det M>0$ and $M^{-1}>0$.

> [!warning] Slide error: the semi-definite minors test
> The slide says "$M\ge 0$ iff every leading minor is nonnegative". False: $\begin{bmatrix}0&0\\0&-1\end{bmatrix}$ has $D_1=D_2=0$ but the form is $-1$ at $(0,1)$. For $M\ge 0$ check **all** principal minors (same rows and columns chosen), or the eigenvalues.

> [!warning] Watch out
> The tests need a symmetric $M$. $\begin{bmatrix}1&4\\0&1\end{bmatrix}$ has eigenvalues $1,1$ but its form is $-2$ at $(1,-1)$. Positive entries are not enough either: $\begin{bmatrix}1&2\\2&1\end{bmatrix}$ has eigenvalues $3,-1$.

> [!info] Quadratic forms and the symmetric part (beyond the slides)
> The scalar $\mathbf{x}^{\mathsf T}M\mathbf{x}=\sum_{i,j}m_{ij}x_ix_j$ is called a quadratic form. The product $x_ix_j$ ($i\ne j$) gets the coefficient $m_{ij}+m_{ji}$. Only this sum matters, not how it is split.
> So every square $M$ gives the same form as its symmetric part $M_s=\tfrac12(M+M^{\mathsf T})$: $\mathbf{x}^{\mathsf T}M\mathbf{x}=\mathbf{x}^{\mathsf T}M_s\mathbf{x}$. The rest, $K=\tfrac12(M-M^{\mathsf T})$, has $K^{\mathsf T}=-K$ and $\mathbf{x}^{\mathsf T}K\mathbf{x}=0$ for every $\mathbf{x}$.
> This is why the definition asks for a symmetric $M$: nothing is lost, and the eigenvalue and minor tests are valid only for the symmetric matrix.

> [!info] Principal minors and leading principal minors (beyond the slides)
> A principal minor is the determinant of the block that keeps the same set of rows and columns, for example rows and columns $\{2,3\}$. A leading principal minor keeps the first $k$ rows and columns: $D_1,D_2,\dots,D_n$.
> A $3\times 3$ matrix has $3$ leading principal minors but $7$ principal minors: the three diagonal entries, three $2\times 2$ blocks ($\{1,2\}$, $\{1,3\}$, $\{2,3\}$) and $\det M$.
> Test for $M>0$: the $n$ leading ones are enough. Test for $M\ge 0$: all principal minors must be $\ge 0$.

> [!question]- Check (slide 83, a): $M$ with the rows $(2,3)$ and $(-1,1)$ is not symmetric. Find the symmetric matrix with the same quadratic form. Is the form positive for every $\mathbf{x}\ne\mathbf{0}$?
> $\mathbf{x}^{\mathsf T}M\mathbf{x}=2x_1^2+(3-1)x_1x_2+x_2^2=2x_1^2+2x_1x_2+x_2^2$.
> Symmetric part: $M_s=\tfrac12(M+M^{\mathsf T})$ has the rows $(2,1)$ and $(1,1)$. It gives the same form.
> Completing the square: $2x_1^2+2x_1x_2+x_2^2=(x_1+x_2)^2+x_1^2$. This is zero only if $x_1=0$ and $x_1+x_2=0$, so only at $\mathbf{x}=\mathbf{0}$. The form is positive, and $M_s>0$ ($D_1=2$, $D_2=2-1=1$).
> Note: the eigenvalues of $M$ itself are $\tfrac{3\pm j\sqrt{11}}{2}$, complex. The tests must be applied to $M_s$, whose eigenvalues are $\tfrac{3\pm\sqrt5}{2}>0$.

> [!question]- Check (slide 83, b): Complete the square for $M$ with the rows $(1,3)$ and $(3,a)$. For which $a$ is $M>0$, and for which $a$ is $M\ge 0$? Give a nonzero $\mathbf{x}$ with zero form in the boundary case.
> $\mathbf{x}^{\mathsf T}M\mathbf{x}=x_1^2+6x_1x_2+ax_2^2=(x_1+3x_2)^2+(a-9)x_2^2$.
> $M>0$ iff $a>9$: both squares are then nonnegative and vanish together only at $\mathbf{x}=\mathbf{0}$.
> $M\ge 0$ iff $a\ge 9$. For $a<9$ take $\mathbf{x}=(3,-1)^{\mathsf T}$: the form is $a-9<0$.
> Boundary $a=9$: $\mathbf{x}=(3,-1)^{\mathsf T}$ gives $(3-3)^2+0=0$. Same result from the minors: $D_1=1$, $D_2=a-9$.

> [!question]- Check (slide 84, a): Show in three ways that $M$ with the rows $(2,-1,0)$, $(-1,2,-1)$ and $(0,-1,2)$ is positive definite: leading principal minors, eigenvalues, sum of squares.
> Minors: $D_1=2$, $D_2=4-1=3$, $D_3=2(4-1)-(-1)(-2-0)=6-2=4$. All positive.
> Eigenvalues: $\det(M-\lambda I)=(2-\lambda)\big[(2-\lambda)^2-1\big]-(2-\lambda)=(2-\lambda)\big[(2-\lambda)^2-2\big]$. So $\lambda=2,\ 2+\sqrt2\approx 3.414,\ 2-\sqrt2\approx 0.586$. All positive. Product $2\cdot(4-2)=4=D_3$.
> Squares: $\mathbf{x}^{\mathsf T}M\mathbf{x}=2x_1^2-2x_1x_2+2x_2^2-2x_2x_3+2x_3^2=x_1^2+(x_1-x_2)^2+(x_2-x_3)^2+x_3^2$.
> This is zero only if $x_1=0$, $x_3=0$ and $x_1=x_2$, so only at $\mathbf{x}=\mathbf{0}$.

> [!question]- Check (slide 84, b): $M$ with the rows $(1,1,1)$, $(1,1,1)$ and $(1,1,0)$ has the leading principal minors $1,0,0$. Is $M\ge 0$?
> No. $D_1=1$, $D_2=1-1=0$, $D_3=0$ (two equal rows). The leading minors are all nonnegative, but they do not decide semi-definiteness.
> Check all principal minors. Rows and columns $\{2,3\}$: $1\cdot 0-1\cdot 1=-1<0$. So $M$ is not positive semi-definite.
> A vector that shows it: $\mathbf{x}=(0,1,-1)^{\mathsf T}$ has $x_1=0$, so $\mathbf{x}^{\mathsf T}M\mathbf{x}=x_2^2+2x_2x_3=1-2=-1$.
> Eigenvalues: $\lambda(\lambda^2-2\lambda-2)=0$, so $\lambda=0,\ 1+\sqrt3\approx 2.732,\ 1-\sqrt3\approx -0.732$. One is negative: $M$ is indefinite.

> [!question]- Check (slide 84, c): Use the recipe $N=DQ^{\mathsf T}$ of the proof to factor $M$ with the rows $(2,1)$ and $(1,2)$ as $M=N^{\mathsf T}N$. Is $N$ nonsingular?
> From the example in section 1: $\lambda=3,1$ and $Q=\tfrac{1}{\sqrt2}[(1,1)^{\mathsf T}\ (1,-1)^{\mathsf T}]$. $D=\operatorname{diag}(\sqrt3,1)$.
> $N=DQ^{\mathsf T}$ has the rows $\big(\sqrt{3/2},\sqrt{3/2}\big)$ and $\big(\tfrac{1}{\sqrt2},-\tfrac{1}{\sqrt2}\big)$.
> Check $N^{\mathsf T}N$: entry $(1,1)$ is $\tfrac32+\tfrac12=2$, entry $(1,2)$ is $\tfrac32-\tfrac12=1$, entry $(2,2)$ is $\tfrac32+\tfrac12=2$. This is $M$.
> $\det N=\det D\cdot\det Q^{\mathsf T}=\sqrt3\cdot(-1)=-\sqrt3\ne 0$, so $N$ is nonsingular. This agrees with $M>0$.

## 3. Singular values and the SVD (slides 85-87)
![[ee502_eee501alllecturenotesabo_p085.jpg]]
![[ee502_eee501alllecturenotesabo_p086.jpg]]
![[ee502_eee501alllecturenotesabo_p087.jpg]]

**Notes.** For $H\in\mathbb{R}^{m\times n}$, $H^{\mathsf T}H$ is symmetric and positive semi-definite. With $r=\operatorname{rank}H$ and eigenvalues $\lambda_1\ge\dots\ge\lambda_r>0$ of $H^{\mathsf T}H$, the singular values are $\sigma_j=\sqrt{\lambda_j}$, followed by zeros. There are $\min\{m,n\}$ of them in total.

**Theorem (SVD).** $H=RSQ^{\mathsf T}$ with $R\in\mathbb{R}^{m\times m}$ and $Q\in\mathbb{R}^{n\times n}$ orthogonal, and $S\in\mathbb{R}^{m\times n}$ holding the singular values on its diagonal. Equivalently $H\mathbf{q}_j=\sigma_j\mathbf{r}_j$: rotate ($Q^{\mathsf T}$), stretch ($S$), rotate ($R$).

The proof is the recipe:
1. Diagonalize $H^{\mathsf T}H$: $Q^{\mathsf T}H^{\mathsf T}HQ=\begin{bmatrix}\Lambda&0\\0&0\end{bmatrix}$, $\Lambda=D^2$, $D=\operatorname{diag}\{\sigma_1,\dots,\sigma_r\}$. Split $Q=[Q_1\ Q_2]$.
2. $Q_2^{\mathsf T}H^{\mathsf T}HQ_2=0$ gives $HQ_2=0$ (columns of $Q_2$ span the null space of $H$).
3. $R_1=HQ_1D^{-1}$ has orthonormal columns. Complete it to an orthogonal $R=[R_1\ R_2]$.
4. Then $R^{\mathsf T}HQ=\begin{bmatrix}D&0\\0&0\end{bmatrix}=S$.

> [!example] Slide example: $H=\begin{bmatrix}-4&-1&2\\2&1/2&-1\end{bmatrix}$ (rank 1)
> $H^{\mathsf T}H=\begin{bmatrix}20&5&-10\\5&5/4&-5/2\\-10&-5/2&5\end{bmatrix}$ has eigenvalues $\{105/4,0,0\}$.
> Singular values: $\sigma_1=\sqrt{105}/2\approx 5.1235$, $\sigma_2=0$.
> $Q_1=(4,1,-2)^{\mathsf T}/\sqrt{21}$, $R_1=HQ_1/\sigma_1=(-2,1)^{\mathsf T}/\sqrt5\approx(-0.8944,0.4472)^{\mathsf T}$.
> Check: $\sigma_1R_1Q_1^{\mathsf T}=H$. MATLAB: `[R,S,Q]=svd(H)`.

The SVD is not unique: signs of a pair $(\mathbf{q}_j,\mathbf{r}_j)$ can flip, and $Q_2$, $R_2$ can be any orthonormal bases of their subspaces.

> [!warning] Slide slip: order of the singular values
> The slide says "in ascending order". The standard convention (MATLAB `svd`, the condition number) is descending: $\sigma_1$ is the largest.

> [!info] Counting the singular values (beyond the slides)
> $H^{\mathsf T}H$ is $n\times n$ and has $n$ eigenvalues: $r$ positive ones and $n-r$ zeros. $H$ has only $\min\{m,n\}$ singular values, because $S$ is $m\times n$ and its diagonal has $\min\{m,n\}$ places.
> So the list of singular values has $r$ positive numbers and $\min\{m,n\}-r=\min\{m-r,n-r\}$ zeros. This is the "# of zeros" on slide 85.
> Also $\operatorname{rank}H=\operatorname{rank}H^{\mathsf T}H=r$ = number of nonzero singular values. Reason: $H^{\mathsf T}H\mathbf{x}=\mathbf{0}$ gives $\mathbf{x}^{\mathsf T}H^{\mathsf T}H\mathbf{x}=\lVert H\mathbf{x}\rVert^2=0$, so $H$ and $H^{\mathsf T}H$ have the same null space.

> [!question]- Check (slide 85): $H$ has the rows $(1,0,1)$ and $(0,1,1)$. Find the eigenvalues of $H^{\mathsf T}H$, the singular values of $H$, the rank, and the number of zero singular values.
> $H^{\mathsf T}H$ has the rows $(1,0,1)$, $(0,1,1)$ and $(1,1,2)$.
> $\Delta(\lambda)=\lambda^3-4\lambda^2+3\lambda=\lambda(\lambda-1)(\lambda-3)$. Eigenvalues $3,1,0$.
> Singular values: $H$ is $2\times 3$, so there are $\min\{2,3\}=2$ of them: $\sigma_1=\sqrt3\approx 1.732$, $\sigma_2=1$.
> Rank: two nonzero singular values, so $r=2$. Zero singular values: $\min\{m-r,n-r\}=\min\{0,1\}=0$. The eigenvalue $0$ of $H^{\mathsf T}H$ does not give a singular value. It only says that $H$ has a null space of dimension $n-r=1$.

> [!question]- Check (slide 86): Follow the four steps of the proof for $A$ with the rows $(3,0)$ and $(4,5)$. Find $Q$, $S$, $R$ and verify $A=RSQ^{\mathsf T}$.
> Step 1. $A^{\mathsf T}A$ has the rows $(25,20)$ and $(20,25)$. $\Delta(\lambda)=\lambda^2-50\lambda+225=(\lambda-45)(\lambda-5)$. So $\sigma_1=\sqrt{45}=3\sqrt5\approx 6.708$, $\sigma_2=\sqrt5\approx 2.236$.
> Eigenvectors: $\mathbf{q}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$ for $45$, $\mathbf{q}_2=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$ for $5$.
> Step 2. $r=2=n$, so there is no $Q_2$ (the null space is $\{\mathbf{0}\}$).
> Step 3. $\mathbf{r}_1=A\mathbf{q}_1/\sigma_1=\tfrac{1}{\sqrt2}(3,9)^{\mathsf T}/(3\sqrt5)=\tfrac{1}{\sqrt{10}}(1,3)^{\mathsf T}$. $\mathbf{r}_2=A\mathbf{q}_2/\sigma_2=\tfrac{1}{\sqrt2}(3,-1)^{\mathsf T}/\sqrt5=\tfrac{1}{\sqrt{10}}(3,-1)^{\mathsf T}$. They are orthonormal: $\mathbf{r}_1^{\mathsf T}\mathbf{r}_2=(3-3)/10=0$.
> Step 4. $Q=[\mathbf{q}_1\ \mathbf{q}_2]$, $R=[\mathbf{r}_1\ \mathbf{r}_2]$, $S=\operatorname{diag}(3\sqrt5,\sqrt5)$. Verify with $A=\sigma_1\mathbf{r}_1\mathbf{q}_1^{\mathsf T}+\sigma_2\mathbf{r}_2\mathbf{q}_2^{\mathsf T}$:
> $$A=\tfrac{3\sqrt5}{\sqrt{20}}\begin{bmatrix}1&1\\3&3\end{bmatrix}+\tfrac{\sqrt5}{\sqrt{20}}\begin{bmatrix}3&-3\\-1&1\end{bmatrix}=\begin{bmatrix}1.5&1.5\\4.5&4.5\end{bmatrix}+\begin{bmatrix}1.5&-1.5\\-0.5&0.5\end{bmatrix}=\begin{bmatrix}3&0\\4&5\end{bmatrix}.$$

> [!question]- Check (slide 87): $H$ with the rows $(1,2)$ and $(2,4)$ has rank 1, like the slide example. Find its SVD. Why can the second column of $R$ not come from the formula $R_1=HQ_1D^{-1}$?
> $H^{\mathsf T}H$ has the rows $(5,10)$ and $(10,20)$: trace $25$, determinant $0$, so the eigenvalues are $25$ and $0$. $\sigma_1=5$, $\sigma_2=0$.
> $Q_1=\mathbf{q}_1=\tfrac{1}{\sqrt5}(1,2)^{\mathsf T}$. $Q_2=\mathbf{q}_2=\tfrac{1}{\sqrt5}(2,-1)^{\mathsf T}$, and $H\mathbf{q}_2=\mathbf{0}$ as the proof says.
> $R_1=H\mathbf{q}_1/\sigma_1=\tfrac{1}{\sqrt5}(5,10)^{\mathsf T}/5=\tfrac{1}{\sqrt5}(1,2)^{\mathsf T}$.
> The formula divides by $\sigma_j$, and $\sigma_2=0$ ($H\mathbf{q}_2=\mathbf{0}$ gives no direction). So $R_2$ is chosen freely as a unit vector perpendicular to $R_1$: $R_2=\tfrac{1}{\sqrt5}(2,-1)^{\mathsf T}$.
> $R=\tfrac{1}{\sqrt5}[(1,2)^{\mathsf T}\ (2,-1)^{\mathsf T}]$, $S=\operatorname{diag}(5,0)$, $Q=R$ here. Check: $RSQ^{\mathsf T}=5\,\mathbf{r}_1\mathbf{q}_1^{\mathsf T}=\tfrac55\begin{bmatrix}1&2\\2&4\end{bmatrix}=H$.

## 4. Condition number (slide 88)
![[ee502_eee501alllecturenotesabo_p088.jpg]]

**Notes.** The matrix 2-norm is the largest stretch: $\lVert A\rVert_2=\sup_{\lVert\mathbf{x}\rVert_2=1}\lVert A\mathbf{x}\rVert_2$. For nonsingular $A\in\mathbb{R}^{n\times n}$:
$$\sigma_1=\lVert A\rVert_2,\qquad \sigma_n=\frac{1}{\lVert A^{-1}\rVert_2},\qquad \kappa=\frac{\sigma_1}{\sigma_n}=\lVert A\rVert_2\,\lVert A^{-1}\rVert_2\ \ge 1 .$$
$\kappa=\infty$ if $A$ is singular. If $A\mathbf{x}=\mathbf{b}$ and $A(\mathbf{x}+\delta\mathbf{x})=\mathbf{b}+\delta\mathbf{b}$, then
$$\frac{\lVert\delta\mathbf{x}\rVert}{\lVert\mathbf{x}\rVert}\le\kappa\,\frac{\lVert\delta\mathbf{b}\rVert}{\lVert\mathbf{b}\rVert}.$$
Remark 2 of the slide: the columns of $Q$ are eigenvectors of $H^{\mathsf T}H$, the columns of $R$ are eigenvectors of $HH^{\mathsf T}$. Both share the nonzero eigenvalues $\sigma_j^2$.

> [!example] Ill-conditioned system (our notes)
> $A=\begin{bmatrix}1&1\\1&1.01\end{bmatrix}$: $\sigma_1\approx 2.005$, $\sigma_2\approx 0.0049875$, $\kappa\approx 402$.
> $\mathbf{b}=(2,2.01)$ gives $\mathbf{x}=(1,1)$. $\mathbf{b}=(2,2.02)$ gives $\mathbf{x}=(0,2)$. A 0.35% change in the data moves the solution by 100%.

> [!warning] Slide typos
> - The slide writes $\sigma_n=\lVert A^{-1}\rVert_2$. Correct: $\sigma_n=1/\lVert A^{-1}\rVert_2$.
> - The slide writes $H=RSQ$ in Remark 2. The transpose is intended: $H=RSQ^{\mathsf T}$.
> - $\kappa$ uses singular values, not eigenvalues. They agree only for symmetric matrices ($\sigma_j=\lvert\lambda_j\rvert$).

> [!info] Why the 2-norm is the largest singular value (beyond the slides)
> The slide states $\sigma_1=\lVert A\rVert_2$ without a derivation. For any $\mathbf{x}$: $\lVert A\mathbf{x}\rVert^2=\mathbf{x}^{\mathsf T}A^{\mathsf T}A\mathbf{x}$. The matrix $A^{\mathsf T}A$ is symmetric with largest eigenvalue $\sigma_1^2$, so by the bound in section 2, $\mathbf{x}^{\mathsf T}A^{\mathsf T}A\mathbf{x}\le\sigma_1^2\lVert\mathbf{x}\rVert^2$.
> So $\lVert A\mathbf{x}\rVert\le\sigma_1\lVert\mathbf{x}\rVert$, with equality for $\mathbf{x}=\mathbf{q}_1$ (then $A\mathbf{q}_1=\sigma_1\mathbf{r}_1$). The largest stretch is $\sigma_1$.
> Inverse: $A=RSQ^{\mathsf T}$ gives $A^{-1}=QS^{-1}R^{\mathsf T}$. This is an SVD of $A^{-1}$ with the singular values $1/\sigma_j$. The largest of them is $1/\sigma_n$, so $\lVert A^{-1}\rVert_2=1/\sigma_n$.
> Remark 2 in one line: $H^{\mathsf T}H=QS^{\mathsf T}R^{\mathsf T}RSQ^{\mathsf T}=Q(S^{\mathsf T}S)Q^{\mathsf T}$ and $HH^{\mathsf T}=R(SS^{\mathsf T})R^{\mathsf T}$. Both $S^{\mathsf T}S$ ($n\times n$) and $SS^{\mathsf T}$ ($m\times m$) are diagonal with the entries $\sigma_j^2$, followed by zeros.

> [!question]- Check (slide 88, a): $A$ with the rows $(3,0)$ and $(4,5)$ has the singular values $3\sqrt5$ and $\sqrt5$. Give $\lVert A\rVert_2$, $\lVert A^{-1}\rVert_2$ and $\kappa$. A student computes $\kappa=5/3$ from the eigenvalues. What is wrong?
> $\lVert A\rVert_2=\sigma_1=3\sqrt5\approx 6.708$. $\lVert A^{-1}\rVert_2=1/\sigma_2=1/\sqrt5\approx 0.447$.
> $\kappa=\sigma_1/\sigma_2=3\sqrt5/\sqrt5=3$.
> $A$ is triangular with the eigenvalues $3$ and $5$, but it is not symmetric, so $\sigma_j\ne\lvert\lambda_j\rvert$. The ratio $5/3\approx 1.67$ is not the condition number. Only the product agrees: $\sigma_1\sigma_2=15=\lvert\det A\rvert=3\cdot 5$.

> [!question]- Check (slide 88, b): For $H$ with the rows $(1,0,1)$ and $(0,1,1)$, the matrix $H^{\mathsf T}H$ has the eigenvalues $3,1,0$. Without a new characteristic polynomial, what are the eigenvalues of $HH^{\mathsf T}$? Then find the columns of $R$.
> $HH^{\mathsf T}=RSS^{\mathsf T}R^{\mathsf T}$ is $2\times 2$ and shares the nonzero eigenvalues $\sigma_j^2$ with $H^{\mathsf T}H$. So its eigenvalues are $3$ and $1$. The extra $0$ belongs only to the larger matrix $H^{\mathsf T}H$.
> Check: $HH^{\mathsf T}$ has the rows $(2,1)$ and $(1,2)$, trace $4=3+1$, determinant $3=3\cdot 1$.
> Columns of $R$ = unit eigenvectors of $HH^{\mathsf T}$: $\mathbf{r}_1=\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$ for $3$, $\mathbf{r}_2=\tfrac{1}{\sqrt2}(1,-1)^{\mathsf T}$ for $1$ (each up to a sign that must match $\mathbf{q}_j$).
> Same $\mathbf{r}_1$ from the recipe: $\mathbf{q}_1=\tfrac{1}{\sqrt6}(1,1,2)^{\mathsf T}$, $H\mathbf{q}_1=\tfrac{1}{\sqrt6}(3,3)^{\mathsf T}$, divided by $\sigma_1=\sqrt3$: $\tfrac{1}{\sqrt2}(1,1)^{\mathsf T}$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Symmetric | $M=M^{\mathsf T}$; real $\lambda$; $M=Q\Lambda Q^{\mathsf T}$, $Q$ orthogonal |
| Orthogonal $Q$ | $Q^{\mathsf T}Q=I$, $Q^{-1}=Q^{\mathsf T}$, $\lVert Q\mathbf{x}\rVert=\lVert\mathbf{x}\rVert$ |
| $M>0$ | $\mathbf{x}^{\mathsf T}M\mathbf{x}>0$ for $\mathbf{x}\ne\mathbf{0}$ $\iff$ all $\lambda_j>0$ $\iff$ leading minors $>0$ $\iff$ $M=N^{\mathsf T}N$, $N$ nonsingular |
| $M\ge 0$ | all $\lambda_j\ge 0$ $\iff$ all principal minors $\ge 0$ $\iff$ $M=N^{\mathsf T}N$, any $N$ |
| Singular values | $\sigma_j=\sqrt{\lambda_j(H^{\mathsf T}H)}$, descending, $\min\{m,n\}$ of them |
| SVD | $H=RSQ^{\mathsf T}$, $H\mathbf{q}_j=\sigma_j\mathbf{r}_j$, $R_1=HQ_1D^{-1}$ |
| 2-norm | $\lVert A\rVert_2=\sigma_1$, $\lVert A^{-1}\rVert_2=1/\sigma_n$ |
| Condition number | $\kappa=\sigma_1/\sigma_n$; relative error amplification $\le\kappa$ |

## Check yourself
> [!question]- 1. Orthogonally diagonalize $M$ with the rows $(5,2)$ and $(2,2)$.
> $\Delta=\lambda^2-7\lambda+6=(\lambda-6)(\lambda-1)$. $\lambda_1=6$: $\mathbf{q}_1=\tfrac{1}{\sqrt5}(2,1)^{\mathsf T}$. $\lambda_2=1$: $\mathbf{q}_2=\tfrac{1}{\sqrt5}(1,-2)^{\mathsf T}$. $\mathbf{q}_1^{\mathsf T}\mathbf{q}_2=0$, and $6\mathbf{q}_1\mathbf{q}_1^{\mathsf T}+\mathbf{q}_2\mathbf{q}_2^{\mathsf T}=M$.

> [!question]- 2. For which $a$ is the matrix with the rows $(2,1,0)$, $(1,a,1)$ and $(0,1,2)$ positive definite?
> $D_1=2$, $D_2=2a-1$, $D_3=2(2a-1)-2=4a-4$. All positive iff $a>1$.

> [!question]- 3. Is the matrix with the rows $(2,-2)$ and $(-2,2)$ positive definite, semi-definite or neither?
> Eigenvalues $0$ and $4$: semi-definite, not definite. The form is $2(x_1-x_2)^2$, which is $0$ at $(1,1)$.

> [!question]- 4. Show that $N^{\mathsf T}N>0$ when $N\in\mathbb{R}^{m\times n}$ has full column rank.
> $N^{\mathsf T}N$ is symmetric. Independent columns mean $N\mathbf{x}=\mathbf{0}$ only for $\mathbf{x}=\mathbf{0}$. So for $\mathbf{x}\ne\mathbf{0}$: $\mathbf{x}^{\mathsf T}N^{\mathsf T}N\mathbf{x}=\lVert N\mathbf{x}\rVert^2>0$.

> [!question]- 5. Singular values of $A$ with the rows $(1,1)$ and $(0,1)$, and its $\kappa$.
> $A^{\mathsf T}A=\begin{bmatrix}1&1\\1&2\end{bmatrix}$, $\lambda=\tfrac{3\pm\sqrt5}{2}$. $\sigma_1=\tfrac{1+\sqrt5}{2}\approx 1.618$, $\sigma_2=\tfrac{\sqrt5-1}{2}\approx 0.618$, product $1=\lvert\det A\rvert$. $\kappa=\sigma_1/\sigma_2=\tfrac{3+\sqrt5}{2}\approx 2.618$.

> [!question]- 6. Singular values of an orthogonal matrix, and of $\operatorname{diag}(-3,2)$?
> Orthogonal: $Q^{\mathsf T}Q=I$, so all $\sigma=1$. $\operatorname{diag}(-3,2)$: $A^{\mathsf T}A=\operatorname{diag}(9,4)$, so $\sigma=3,2$.

## Links
- Course index: [[EE502 Home]]
- Previous: Lecture 7 (Jordan form). Next: [[EE502 L09 - LTI state equation solution]]
- Used later in: [[EE502 L12 - Stability]] (Lyapunov functions), [[EE502 L13 - Controllability]] and [[EE502 L14 - Observability]] (Gramians)
- Full step-by-step notes (PDF): [EE502_Lecture_08_PosDef_SVD.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_08/EE502_Lecture_08_PosDef_SVD.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_08/EE502_Lecture_08_PosDef_SVD.pdf`
- Original slides (PDF, pp. 81-88): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
