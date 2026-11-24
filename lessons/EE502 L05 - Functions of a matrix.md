---
course: EE 502 Linear System Theory
lecture: 5
title: Functions of a matrix
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 68-77)
full_notes: lecture_notes/lecture_05/EE502_Lecture_05_Matrix_Functions.pdf
---
# EE 502 · Lecture 5 · Functions of a matrix

> [!summary] In short
> - A polynomial of a matrix: replace $\lambda^k$ by $A^k$ and the constant by a multiple of $I$.
> - Cayley-Hamilton: $\Delta(A)=0$. So every $f(A)$ is a combination of $I,A,\dots,A^{n-1}$.
> - The minimal polynomial $\Psi$ is the monic polynomial of least degree with $\Psi(A)=0$. Its exponents are the sizes of the largest Jordan blocks.
> - $A$ is diagonalizable exactly when all exponents of $\Psi$ are 1.
> - $f(A):=h(A)$, where the polynomial $h$ matches $f$ and its derivatives at the eigenvalues.

> [!info] Order of the lectures
> The syllabus teaches matrix functions (slides 68-80) before the Jordan form (slides 61-67). This lecture uses Jordan blocks in a few places. They are explained in [[EE502 L07 - Jordan form]].

## 1. Polynomials of a matrix (slide 69)
![[ee502_eee501alllecturenotesabo_p069.jpg]]

**Notes.** For $A\in\mathbb{R}^{n\times n}$, $A^0=I_n$ and $A^k=A\cdots A$ ($k$ factors). For $f(\lambda)=f_n\lambda^n+\cdots+f_1\lambda+f_0$:

$$f(A)=f_nA^n+\cdots+f_1A+f_0I_n$$

Two structural rules:

- **Block-diagonal.** $A=\begin{bmatrix}A_1&0\\0&A_2\end{bmatrix}$ with square blocks gives $f(A)=\begin{bmatrix}f(A_1)&0\\0&f(A_2)\end{bmatrix}$.
- **Similar.** $\hat A=Q^{-1}AQ$ gives $\hat A^k=Q^{-1}A^kQ$, so $f(\hat A)=Q^{-1}f(A)Q$.

> [!warning] Watch out
> $f(A)$ is not "apply $f$ to every entry". For $A=\begin{bmatrix}1&2\\0&3\end{bmatrix}$, $A^2=\begin{bmatrix}1&8\\0&9\end{bmatrix}$, not $\begin{bmatrix}1&4\\0&9\end{bmatrix}$.

## 2. Cayley-Hamilton theorem (slide 70)
![[ee502_eee501alllecturenotesabo_p070.jpg]]

**Notes.** If $\Delta(\lambda)=\det(\lambda I-A)=\lambda^n+a_1\lambda^{n-1}+\cdots+a_n$, then

$$\Delta(A)=A^n+a_1A^{n-1}+\cdots+a_{n-1}A+a_nI_n=0$$

Consequences:

1. In factored form, with distinct roots $\lambda_i$ of multiplicities $n_i$: $\prod_{i=1}^k(A-\lambda_iI)^{n_i}=0$.
2. $A^n=-(a_1A^{n-1}+\cdots+a_nI_n)$, so every power $A^{n+j}$ is a combination of $I_n,A,\dots,A^{n-1}$.
3. So any polynomial of $A$, of any degree, is a combination of $I_n,A,\dots,A^{n-1}$.

> [!example] $A^2$ and $A^{-1}$ without multiplying (ours)
> $A=\begin{bmatrix}2&1\\1&2\end{bmatrix}$: $\Delta=\lambda^2-4\lambda+3$. So $A^2=4A-3I=\begin{bmatrix}5&4\\4&5\end{bmatrix}$, and from $A(A-4I)=-3I$: $A^{-1}=\frac13(4I-A)=\frac13\begin{bmatrix}2&-1\\-1&2\end{bmatrix}$.

## 3. Minimal polynomial (slides 71-73)
![[ee502_eee501alllecturenotesabo_p071.jpg]]
![[ee502_eee501alllecturenotesabo_p072.jpg]]
![[ee502_eee501alllecturenotesabo_p073.jpg]]

**Notes.** **Definition.** A monic polynomial $\Psi(\lambda)$ of least degree with $\Psi(A)=0$ is the **minimal polynomial** of $A$. (Monic: leading coefficient 1.)

**Slide example.** A Jordan form with $\Delta(\lambda)=(\lambda-\lambda_0)^4$, two Jordan blocks of sizes 3 and 1:

$$A=\begin{bmatrix}\lambda_0&1&0&0\\0&\lambda_0&1&0\\0&0&\lambda_0&0\\0&0&0&\lambda_0\end{bmatrix}$$

$N=A-\lambda_0I$ has ones at positions $(1,2)$ and $(2,3)$. $N^2$ has a single one at $(1,3)$. $N^3=0$. So $\Psi(\lambda)=(\lambda-\lambda_0)^3$, of lower degree than $\Delta$.

**Fact 1.** $\Psi$ is unique and divides $\Delta$. Proof idea: Euclidean division $\Phi=\Psi q+r$ with $\deg r<\deg\Psi$. Since $\Phi(A)=\Psi(A)=0$, also $r(A)=0$, which forces $r\equiv0$ because $\Psi$ has least degree.

**Fact 2.** Let $m_i$ be the size of the largest Jordan block of $\lambda_i$ in the Jordan form $J_A$. Then

$$\Psi(\lambda)=\prod_{i=1}^k(\lambda-\lambda_i)^{m_i}$$

Reason: $\Psi(A)=0$ iff $\Psi(J_A)=0$ iff $\Psi$ vanishes on every Jordan block, and for a block $J$ of size $s$ the smallest power with $(J-\lambda_iI)^k=0$ is $k=s$.

> [!warning] Watch out
> - Slide 72 concludes "$\Phi$ divides $\Psi$" after the first division. With $r\equiv0$, $\Phi=\Psi q$, so it is $\Psi$ that divides $\Phi$. The argument is symmetric, so the result stands.
> - $\Psi$ divides $\Delta$, but a factor of $\Delta$ does not automatically give zero at $A$. Test it: $(\lambda-\lambda_0)^2$ fails in the example above.

## 4. Indices and the interpolating polynomial (slide 74)
![[ee502_eee501alllecturenotesabo_p074.jpg]]

**Notes.**

$$\Delta(\lambda)=\prod_{i=1}^k(\lambda-\lambda_i)^{n_i},\qquad \Psi(\lambda)=\prod_{i=1}^k(\lambda-\lambda_i)^{m_i},\qquad 1\le m_i\le n_i$$

The $m_i$ are the **indices** of $A$. **Fact.** $A$ is diagonalizable if and only if all $m_i=1$.

**Definition 1.** Let $f(\lambda)$ be $n-1$ times differentiable. The **interpolating polynomial** of $f$ for $A$ is the polynomial $h(\lambda)$ of degree at most $n-1$ with

$$f^{(l)}(\lambda_i)=h^{(l)}(\lambda_i),\qquad i=1,\dots,k,\quad l=0,1,\dots,n_i-1$$

**Definition 2.** $f(A):=h(A)$.

**Recipe.**
1. Find $\Delta$, its roots $\lambda_i$ and multiplicities $n_i$.
2. Write $h(\lambda)=h_0+h_1\lambda+\cdots+h_{n-1}\lambda^{n-1}$.
3. For each $\lambda_i$ match $f,f',\dots,f^{(n_i-1)}$ with $h,h',\dots$: $n$ linear equations.
4. Solve, then $f(A)=h_0I+h_1A+\cdots+h_{n-1}A^{n-1}$.

> [!warning] Watch out
> - The slide says "degree $n$" and "$l=1,\dots,n_i-1$". Correct: degree at most $n-1$, and $l$ starts at 0 (the values themselves must match). That gives $n$ conditions for $n$ unknowns.
> - For $f(\lambda)=e^{\lambda t}$ differentiate with respect to $\lambda$. $t$ is a constant: $f'(\lambda)=te^{\lambda t}$.
> - A repeated root of $\Delta$ does not mean "not diagonalizable" (example: $\lambda_0I_n$).

## 5. Examples: A^100, e^{At}, f of a Jordan block (slides 75-77)
![[ee502_eee501alllecturenotesabo_p075.jpg]]
![[ee502_eee501alllecturenotesabo_p076.jpg]]
![[ee502_eee501alllecturenotesabo_p077.jpg]]

**Notes.** If $f$ is itself a polynomial, divide: $f=\Delta q+r$. Then $h=r$, the remainder.

**Example 1.** $A^{100}$ for $A=\begin{bmatrix}0&1\\-1&-2\end{bmatrix}$. $\Delta=(\lambda+1)^2$, $f=\lambda^{100}$, $h=h_0+h_1\lambda$.
- $h(-1)=f(-1)$: $h_0-h_1=1$.
- $h'(-1)=f'(-1)$: $h_1=100(-1)^{99}=-100$.

So $h=-99-100\lambda$ and

$$A^{100}=-99I-100A=\begin{bmatrix}-99&-100\\100&101\end{bmatrix}$$

**Example 2.** $e^{At}$ for $A=\begin{bmatrix}0&0&-2\\0&1&0\\1&0&3\end{bmatrix}$, $\Delta=(\lambda-1)^2(\lambda-2)$, $f=e^{\lambda t}$, $h=h_0+h_1\lambda+h_2\lambda^2$.

$$\begin{aligned}h_0+h_1+h_2&=e^t\\ h_1+2h_2&=te^t\\ h_0+2h_1+4h_2&=e^{2t}\end{aligned}\quad\Longrightarrow\quad\begin{aligned}h_0&=-2te^t+e^{2t}\\ h_1&=3te^t+2e^t-2e^{2t}\\ h_2&=-te^t-e^t+e^{2t}\end{aligned}$$

$$e^{At}=h_0I+h_1A+h_2A^2=\begin{bmatrix}2e^t-e^{2t}&0&2e^t-2e^{2t}\\0&e^t&0\\-e^t+e^{2t}&0&-e^t+2e^{2t}\end{bmatrix}$$

No $te^t$ term survives, because this $A$ is diagonalizable ($\Psi=(\lambda-1)(\lambda-2)$).

**Remark.** $B=\begin{bmatrix}0&2&-2\\0&1&0\\1&-1&3\end{bmatrix}$ has the same $\Delta$, so the same $h$. But $h(B)\neq h(A)$: $B$ has a Jordan block for $\lambda=1$, so $e^{Bt}$ keeps a $te^t$ term.

**Example 3.** $f(J)$ for a size-3 Jordan block $J$ of $\lambda_1$. Write $h(\lambda)=\beta_0+\beta_1(\lambda-\lambda_1)+\beta_2(\lambda-\lambda_1)^2$. The conditions give $\beta_0=f(\lambda_1)$, $\beta_1=f'(\lambda_1)$, $\beta_2=\frac12f''(\lambda_1)$:

$$f(J)=\begin{bmatrix}f(\lambda_1)&f'(\lambda_1)&\frac12f''(\lambda_1)\\0&f(\lambda_1)&f'(\lambda_1)\\0&0&f(\lambda_1)\end{bmatrix}$$

General rule for a $k\times k$ Jordan block: $f^{(j)}(\lambda_1)/j!$ on the $j$-th superdiagonal.

> [!warning] Watch out
> On slide 77 the left side of the display in Example 3 is written $e^{Jt}$. It is $f(J)$ for a general $f$, and $e^{Jt}$ only for $f(\lambda)=e^{\lambda t}$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Polynomial of a matrix | $f(A)=f_nA^n+\cdots+f_1A+f_0I$ |
| Similarity rule | $f(Q^{-1}AQ)=Q^{-1}f(A)Q$ |
| Cayley-Hamilton | $\Delta(A)=0$, every $f(A)$ is a combination of $I,A,\dots,A^{n-1}$ |
| Minimal polynomial | $\Psi=\prod(\lambda-\lambda_i)^{m_i}$, $m_i$ = size of the largest Jordan block, $\Psi$ divides $\Delta$ |
| Index | $m_i$, with $1\le m_i\le n_i$. Diagonalizable iff all $m_i=1$ |
| Interpolating polynomial | $h^{(l)}(\lambda_i)=f^{(l)}(\lambda_i)$, $l=0,\dots,n_i-1$, $\deg h\le n-1$ |
| Function of a matrix | $f(A):=h(A)$ |
| Jordan block | $f(J)$ has $f^{(j)}(\lambda_1)/j!$ on the $j$-th superdiagonal |

## Check yourself
> [!question]- 1. For $A=\begin{bmatrix}1&1\\0&2\end{bmatrix}$ and $f(\lambda)=\lambda^2+1$, compute $f(A)$.
> $A^2=\begin{bmatrix}1&3\\0&4\end{bmatrix}$, $f(A)=A^2+I=\begin{bmatrix}2&3\\0&5\end{bmatrix}$. Diagonal check: $f(1)=2$, $f(2)=5$.

> [!question]- 2. A matrix has $\Delta(\lambda)=\lambda^2+1$. What is $A^4$?
> $\lambda^4=(\lambda^2+1)(\lambda^2-1)+1$, and $\Delta(A)=0$, so $A^4=I$.

> [!question]- 3. Find $\Psi$ for $\operatorname{diag}(2,2,5)$ and for $M=\begin{bmatrix}2&1&0\\0&2&0\\0&0&5\end{bmatrix}$. Which is diagonalizable?
> Both have $\Delta=(\lambda-2)^2(\lambda-5)$. For the diagonal matrix $(D-2I)(D-5I)=0$, so $\Psi=(\lambda-2)(\lambda-5)$: diagonalizable. For $M$, $(M-2I)(M-5I)\neq0$, so $\Psi=(\lambda-2)^2(\lambda-5)$: index 2, not diagonalizable.

> [!question]- 4. A $5\times5$ matrix has the single eigenvalue 0 with Jordan blocks of sizes 2, 2, 1. $\Delta$ and $\Psi$?
> $\Delta=\lambda^5$. Largest block has size 2, so $\Psi=\lambda^2$.

> [!question]- 5. Compute $e^{At}$ for $A=\begin{bmatrix}1&1\\0&1\end{bmatrix}$ with the interpolating polynomial.
> $\Delta=(\lambda-1)^2$, $h=h_0+h_1\lambda$. $h_0+h_1=e^t$, $h_1=te^t$. $e^{At}=h_0I+h_1A=e^t\begin{bmatrix}1&t\\0&1\end{bmatrix}$.

> [!question]- 6. Redo slide Example 2 with $\Psi=(\lambda-1)(\lambda-2)$: $h=h_0+h_1\lambda$. Same $e^{At}$?
> $h_0+h_1=e^t$, $h_0+2h_1=e^{2t}$: $h_1=e^{2t}-e^t$, $h_0=2e^t-e^{2t}$. $h_0I+h_1A$ gives the same matrix, for example entry $(3,3)$: $h_0+3h_1=-e^t+2e^{2t}$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L04 - Equations, eigenvalues, diagonalization]]. Next: [[EE502 L06 - Matrix exponential]]. Jordan blocks: [[EE502 L07 - Jordan form]]
- Used by the midterm. The Quiz 2 revision pack for slides 36-79 (rank, eigen, $f(A)$, Cayley-Hamilton) is kept for Quiz 3 and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_05_Matrix_Functions.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_05/EE502_Lecture_05_Matrix_Functions.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_05/EE502_Lecture_05_Matrix_Functions.pdf`
- Original slides (PDF, pp. 68-77): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: 68 (section title).
