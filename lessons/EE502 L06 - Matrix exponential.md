---
course: EE 502 Linear System Theory
lecture: 6
title: Matrix exponential
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 78-80)
full_notes: lecture_notes/lecture_06/EE502_Lecture_06_Matrix_Exponential.pdf
---
# EE 502 · Lecture 6 · Matrix exponential

> [!summary] In short
> - Second definition of $f(A)$: plug $A$ into the power series of $f$. It agrees with the interpolating-polynomial definition of Lecture 5.
> - $e^{At}=\sum_{k=0}^\infty\frac{t^k}{k!}A^k$ converges for every square $A$.
> - Six properties (P1 to P6). The two used most: $\frac{d}{dt}e^{At}=Ae^{At}$ and $\mathcal{L}\{e^{At}\}=(sI-A)^{-1}$.
> - $e^{(A+B)t}=e^{At}e^{Bt}$ only if $AB=BA$.
> - Three ways to compute $e^{At}$: interpolating polynomial, Laplace, diagonalization or Jordan form.

## 1. Power series definition of f(A) (slides 78-79)
![[ee502_eee501alllecturenotesabo_p078.jpg]]
![[ee502_eee501alllecturenotesabo_p079.jpg]]

**Notes.** Slide 78 first repeats the general formula for a $k\times k$ Jordan block $J$ of $\lambda_1$: $f(J)$ has $f^{(j)}(\lambda_1)/j!$ on the $j$-th superdiagonal (see [[EE502 L05 - Functions of a matrix]]).

**Power series definition.** Let $f$ have a power series about $a\in\mathbb{C}$ with radius of convergence $\rho>0$:

$$f(\lambda)=\sum_{i=0}^{\infty}\beta_i(\lambda-a)^i,\quad|\lambda-a|<\rho\qquad\Longrightarrow\qquad f(A):=\sum_{i=0}^{\infty}\beta_i(A-aI)^i$$

The matrix series converges for all $A$ whose eigenvalues satisfy $|\lambda_i-a|<\rho$.

**Example 1 (the two definitions agree).** Take the Taylor series of $f$ about $\lambda_1$, with $\beta_i=f^{(i)}(\lambda_1)/i!$, and a Jordan block $J$ of size $k$. Let $N=J-\lambda_1I$ (ones just above the diagonal). Each power of $N$ moves the ones one diagonal up, and $N^i=0$ for $i\ge k$. So the infinite sum stops:

$$f(J)=\sum_{i=0}^{k-1}\frac{f^{(i)}(\lambda_1)}{i!}N^i$$

This is the same matrix as on slide 78.

**Example 2 (the exponential).** The Maclaurin series of $e^{\lambda t}$ gives

$$e^{At}=\sum_{k=0}^{\infty}\frac{t^k}{k!}A^k=I+tA+\frac{t^2}{2!}A^2+\frac{t^3}{3!}A^3+\cdots$$

It converges for every $A\in\mathbb{C}^{n\times n}$, because the exponential series converges for all $\lambda$.

> [!example] Three model matrices (ours)
> - Diagonal: $e^{\operatorname{diag}\{d_1,d_2\}t}=\operatorname{diag}\{e^{d_1t},e^{d_2t}\}$.
> - Nilpotent $N=\begin{bmatrix}0&1\\0&0\end{bmatrix}$: $N^2=0$, so $e^{Nt}=I+tN=\begin{bmatrix}1&t\\0&1\end{bmatrix}$.
> - Jordan block $J=\lambda_1I+N$: $e^{Jt}=e^{\lambda_1t}(I+tN)=\begin{bmatrix}e^{\lambda_1t}&te^{\lambda_1t}\\0&e^{\lambda_1t}\end{bmatrix}$.
> - Oscillator $A=\begin{bmatrix}0&\omega\\-\omega&0\end{bmatrix}$: $e^{At}=\begin{bmatrix}\cos\omega t&\sin\omega t\\-\sin\omega t&\cos\omega t\end{bmatrix}$.

> [!warning] Watch out
> - $e^{At}$ is not "$e$ to each entry". Zero entries do not become $e^0=1$.
> - A divergent series does not mean $f(A)$ is undefined. For $f(\lambda)=1/(1-\lambda)$ and $A=\operatorname{diag}(0.5,2)$ the series diverges, yet $f(A)=(I-A)^{-1}=\operatorname{diag}(2,-1)$ exists. The rule runs one way: eigenvalues inside the disc imply convergence.

## 2. Properties of the matrix exponential (slide 80)
![[ee502_eee501alllecturenotesabo_p080.jpg]]

**Notes.** For square $A,B$ and real $t,t_1,t_2$:

| | Property | Why |
|---|---|---|
| P1 | $e^{A0}=I_n$ | first term of the series |
| P2 | $e^{A(t_1+t_2)}=e^{At_1}e^{At_2}=e^{At_2}e^{At_1}$ | binomial formula and series multiplication |
| P3 | $[e^{At}]^{-1}=e^{-At}$ | P2 with $t_1=t$, $t_2=-t$ |
| P4 | $e^{(A+B)t}=e^{At}e^{Bt}$ provided $AB=BA$ | matrix version of P2 |
| P5 | $\dfrac{d}{dt}e^{At}=Ae^{At}=e^{At}A$ | differentiate the series term by term |
| P6 | $\mathcal{L}\{e^{At}\}=(sI-A)^{-1}$ | $\mathcal{L}\{t^k/k!\}=s^{-(k+1)}$ and $\sum_{k=0}^\infty A^ks^{-(k+1)}=(sI-A)^{-1}$ |

P3 says $e^{At}$ is always invertible. P5 says $\mathbf{x}(t)=e^{At}\mathbf{x}(0)$ solves $\dot{\mathbf{x}}=A\mathbf{x}$.

**Choosing a method for $e^{At}$.**
1. **Interpolating polynomial** (Lecture 5): $h(\lambda_i)=e^{\lambda_it}$ at each root, plus $h'(\lambda_i)=te^{\lambda_it}$ and so on for repeated roots. Then $e^{At}=h(A)$. Works for any Jordan structure.
2. **Laplace** (P6): invert $sI-A$, partial fractions, inverse transform entry by entry.
3. **Diagonalization / Jordan form**: $e^{At}=Qe^{Jt}Q^{-1}$.

The entries of $e^{At}$ are combinations of the modes $t^je^{\lambda_it}$ with $j<m_i$, where $m_i$ is the size of the largest Jordan block of $\lambda_i$.

> [!example] Mass-spring-damper (ours)
> $A=\begin{bmatrix}0&1\\-2&-3\end{bmatrix}$, eigenvalues $-1,-2$. By P6: $(sI-A)^{-1}=\dfrac{1}{(s+1)(s+2)}\begin{bmatrix}s+3&1\\-2&s\end{bmatrix}$, so
> $$e^{At}=\begin{bmatrix}2e^{-t}-e^{-2t}&e^{-t}-e^{-2t}\\-2e^{-t}+2e^{-2t}&-e^{-t}+2e^{-2t}\end{bmatrix}$$
> Checks: $t=0$ gives $I$, and the derivative at $t=0$ gives $A$.

> [!warning] Watch out
> - P4 needs $AB=BA$. Counterexample: $A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$, $B=\begin{bmatrix}0&0\\1&0\end{bmatrix}$. Then $e^{(A+B)t}=\begin{bmatrix}\cosh t&\sinh t\\ \sinh t&\cosh t\end{bmatrix}$, but $e^{At}e^{Bt}=\begin{bmatrix}1+t^2&t\\t&1\end{bmatrix}$.
> - Always check $e^{A0}=I$ and $\frac{d}{dt}e^{At}\big|_{t=0}=A$.
> - Every pole of an entry of $(sI-A)^{-1}$ is an eigenvalue of $A$, but not every eigenvalue appears in every entry.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| $f(A)$ by series | $\sum\beta_i(A-aI)^i$, converges if all $\lvert\lambda_i-a\rvert<\rho$ |
| Matrix exponential | $e^{At}=\sum_{k\ge0}t^kA^k/k!$ |
| Three forms | $e^{At}=h(A)=\mathcal{L}^{-1}\{(sI-A)^{-1}\}=Qe^{Jt}Q^{-1}$ |
| Semigroup | $e^{A(t_1+t_2)}=e^{At_1}e^{At_2}$ |
| Inverse | $(e^{At})^{-1}=e^{-At}$ |
| Derivative | $\frac{d}{dt}e^{At}=Ae^{At}=e^{At}A$ |
| Sum rule | $e^{(A+B)t}=e^{At}e^{Bt}$ only if $AB=BA$ |
| Jordan block | $e^{Jt}=e^{\lambda_1t}\bigl(I+tN+\frac{t^2}{2!}N^2+\cdots\bigr)$, $N=J-\lambda_1I$ |
| Zero-order-hold sampling | $A_d=e^{AT}$, $B_d=\int_0^Te^{A\sigma}d\sigma\,B$ |

## Check yourself
> [!question]- 1. Compute $e^{Jt}$ for $J=\begin{bmatrix}2&1\\0&2\end{bmatrix}$.
> $J=2I+N$, $N^2=0$: $e^{Jt}=e^{2t}(I+tN)=\begin{bmatrix}e^{2t}&te^{2t}\\0&e^{2t}\end{bmatrix}$. At $t=0$: $I$.

> [!question]- 2. Compute $e^{At}$ for $A=\begin{bmatrix}-1&0\\0&-3\end{bmatrix}$ and for $A=\begin{bmatrix}0&2\\-2&0\end{bmatrix}$.
> Diagonal: $\operatorname{diag}\{e^{-t},e^{-3t}\}$. Oscillator with $\omega=2$: $\begin{bmatrix}\cos2t&\sin2t\\-\sin2t&\cos2t\end{bmatrix}$.

> [!question]- 3. Compute $e^{Mt}$ for the shift $M=\begin{bmatrix}0&1&0\\0&0&1\\0&0&0\end{bmatrix}$.
> $M^2$ has a single one at $(1,3)$, $M^3=0$. $e^{Mt}=I+tM+\frac{t^2}{2}M^2=\begin{bmatrix}1&t&t^2/2\\0&1&t\\0&0&1\end{bmatrix}$.

> [!question]- 4. For $\ddot p+3\dot p+2p=0$ with $p(0)=0$, $\dot p(0)=1$, find $p(t)$.
> $\mathbf{x}(t)=e^{At}\begin{bmatrix}0\\1\end{bmatrix}$ is the second column of $e^{At}$ in the example above: $p(t)=e^{-t}-e^{-2t}$.

> [!question]- 5. Write $e^{-At}$ for the oscillator $A=\begin{bmatrix}0&\omega\\-\omega&0\end{bmatrix}$.
> P3: replace $t$ by $-t$. $e^{-At}=\begin{bmatrix}\cos\omega t&-\sin\omega t\\ \sin\omega t&\cos\omega t\end{bmatrix}$. The product with $e^{At}$ is $I$ because $\cos^2+\sin^2=1$.

> [!question]- 6. Discretize $\dot x=-2x+u$ with a zero-order hold and $T=0.5$.
> $A_d=e^{-2\cdot0.5}=e^{-1}$. $B_d=\int_0^{0.5}e^{-2\sigma}d\sigma=\frac{1-e^{-1}}{2}$. So $x[k+1]=e^{-1}x[k]+\frac{1-e^{-1}}{2}u[k]$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L05 - Functions of a matrix]]. Next: [[EE502 L07 - Jordan form]]
- Used by the midterm and by every later lecture on the solution of state equations.
- Full step-by-step notes (PDF): [EE502_Lecture_06_Matrix_Exponential.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_06/EE502_Lecture_06_Matrix_Exponential.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_06/EE502_Lecture_06_Matrix_Exponential.pdf`
- Original slides (PDF, pp. 78-80): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: none.
