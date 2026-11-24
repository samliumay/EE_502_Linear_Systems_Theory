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
> [!question]- 1. Orthogonally diagonalize $M=\begin{bmatrix}5&2\\2&2\end{bmatrix}$.
> $\Delta=\lambda^2-7\lambda+6=(\lambda-6)(\lambda-1)$. $\lambda_1=6$: $\mathbf{q}_1=\tfrac{1}{\sqrt5}(2,1)^{\mathsf T}$. $\lambda_2=1$: $\mathbf{q}_2=\tfrac{1}{\sqrt5}(1,-2)^{\mathsf T}$. $\mathbf{q}_1^{\mathsf T}\mathbf{q}_2=0$, and $6\mathbf{q}_1\mathbf{q}_1^{\mathsf T}+\mathbf{q}_2\mathbf{q}_2^{\mathsf T}=M$.

> [!question]- 2. For which $a$ is $\begin{bmatrix}2&1&0\\1&a&1\\0&1&2\end{bmatrix}$ positive definite?
> $D_1=2$, $D_2=2a-1$, $D_3=2(2a-1)-2=4a-4$. All positive iff $a>1$.

> [!question]- 3. Is $\begin{bmatrix}2&-2\\-2&2\end{bmatrix}$ positive definite, semi-definite or neither?
> Eigenvalues $0$ and $4$: semi-definite, not definite. The form is $2(x_1-x_2)^2$, which is $0$ at $(1,1)$.

> [!question]- 4. Show that $N^{\mathsf T}N>0$ when $N\in\mathbb{R}^{m\times n}$ has full column rank.
> $N^{\mathsf T}N$ is symmetric. Independent columns mean $N\mathbf{x}=\mathbf{0}$ only for $\mathbf{x}=\mathbf{0}$. So for $\mathbf{x}\ne\mathbf{0}$: $\mathbf{x}^{\mathsf T}N^{\mathsf T}N\mathbf{x}=\lVert N\mathbf{x}\rVert^2>0$.

> [!question]- 5. Singular values of $A=\begin{bmatrix}1&1\\0&1\end{bmatrix}$, and its $\kappa$.
> $A^{\mathsf T}A=\begin{bmatrix}1&1\\1&2\end{bmatrix}$, $\lambda=\tfrac{3\pm\sqrt5}{2}$. $\sigma_1=\tfrac{1+\sqrt5}{2}\approx 1.618$, $\sigma_2=\tfrac{\sqrt5-1}{2}\approx 0.618$, product $1=\lvert\det A\rvert$. $\kappa=\sigma_1/\sigma_2=\tfrac{3+\sqrt5}{2}\approx 2.618$.

> [!question]- 6. Singular values of an orthogonal matrix, and of $\operatorname{diag}(-3,2)$?
> Orthogonal: $Q^{\mathsf T}Q=I$, so all $\sigma=1$. $\operatorname{diag}(-3,2)$: $A^{\mathsf T}A=\operatorname{diag}(9,4)$, so $\sigma=3,2$.

## Links
- Course index: [[EE502 Home]]
- Previous: Lecture 7 (Jordan form). Next: [[EE502 L09 - LTI state equation solution]]
- Used later in: [[EE502 L12 - Stability]] (Lyapunov functions), [[EE502 L13 - Controllability]] and [[EE502 L14 - Observability]] (Gramians)
- Full step-by-step notes (PDF): [EE502_Lecture_08_PosDef_SVD.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_08/EE502_Lecture_08_PosDef_SVD.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_08/EE502_Lecture_08_PosDef_SVD.pdf`
- Original slides (PDF, pp. 81-88): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
