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

> [!question]- Check (slide 78, Jordan block formula): Use the formula for $f(J)$ with $f(\lambda)=1/\lambda$ to find the inverse of the $3\times3$ Jordan block $J$ with $\lambda_1=2$.
> $f(\lambda)=\lambda^{-1}$, $f'(\lambda)=-\lambda^{-2}$, $f''(\lambda)=2\lambda^{-3}$.
> At $\lambda_1=2$: $f=\tfrac12$, $f'=-\tfrac14$, $\dfrac{f''}{2!}=\dfrac{2/8}{2}=\tfrac18$.
> The formula puts $f$ on the diagonal, $f'$ on the first superdiagonal and $f''/2!$ on the second:
> $$J^{-1}=\begin{bmatrix}\tfrac12&-\tfrac14&\tfrac18\\0&\tfrac12&-\tfrac14\\0&0&\tfrac12\end{bmatrix}$$
> Test with the first row of $J\,J^{-1}$: $[2\cdot\tfrac12,\ \ 2\cdot(-\tfrac14)+\tfrac12,\ \ 2\cdot\tfrac18-\tfrac14]=[1\ \ 0\ \ 0]$.

> [!question]- Check (slide 78, convergence): The series $\ln(1+\lambda)=\lambda-\frac{\lambda^2}{2}+\frac{\lambda^3}{3}-\cdots$ has $a=0$ and $\rho=1$. Does the slide guarantee convergence of the matrix series for $A$ with rows $(0.5,\ 100)$ and $(0,\ -0.5)$? And for $B$ with rows $(0,\ -2)$ and $(2,\ 0)$?
> $A=\begin{bmatrix}0.5&100\\0&-0.5\end{bmatrix}$, $B=\begin{bmatrix}0&-2\\2&0\end{bmatrix}$.
> Only the eigenvalues count, not the size of the entries.
> $A$ is triangular, so its eigenvalues are $0.5$ and $-0.5$. Both satisfy $\lvert\lambda_i-0\rvert=0.5<1$. The series converges, even with the entry 100.
> $B$ has $\Delta(\lambda)=\lambda^2+4$, eigenvalues $\pm2j$ with $\lvert\lambda_i\rvert=2>1$. The condition fails, so the slide gives no guarantee. Here the series in fact diverges.

> [!question]- Check (slide 79, series stops): Compute $e^{At}$ from the series for the $3\times3$ matrix $A$ with rows $(0,2,1)$, $(0,0,3)$, $(0,0,0)$.
> $A=\begin{bmatrix}0&2&1\\0&0&3\\0&0&0\end{bmatrix}$, $A^2=\begin{bmatrix}0&0&6\\0&0&0\\0&0&0\end{bmatrix}$ (only entry: $2\cdot3=6$) and $A^3=0$. So the series stops after three terms:
> $$e^{At}=I+tA+\frac{t^2}{2}A^2=\begin{bmatrix}1&2t&t+3t^2\\0&1&3t\\0&0&1\end{bmatrix}$$
> The $(1,3)$ entry is $t\cdot1+\frac{t^2}{2}\cdot6=t+3t^2$. The entries are polynomials in $t$, with no exponential, because the only eigenvalue is 0.

> [!question]- Check (slide 79, series does not stop): For $A$ with rows $(1,1)$ and $(0,0)$ show that $A^2=A$ and use this to sum the series of $e^{At}$.
> $A^2=\begin{bmatrix}1\cdot1+1\cdot0&1\cdot1+1\cdot0\\0&0\end{bmatrix}=\begin{bmatrix}1&1\\0&0\end{bmatrix}=A$. So $A^k=A$ for every $k\ge1$.
> $$e^{At}=I+\Bigl(t+\frac{t^2}{2!}+\frac{t^3}{3!}+\cdots\Bigr)A=I+(e^t-1)A=\begin{bmatrix}e^t&e^t-1\\0&1\end{bmatrix}$$
> The bracket is the series of $e^t$ without its first term 1. Test: $t=0$ gives $I$.

> [!question]- Check (slide 79, repeated eigenvalue): $A$ with rows $(1,1)$ and $(-1,3)$ has the double eigenvalue 2. Use $N=A-2I$ and the idea of Example 1 to find $e^{At}$. Which new kind of term appears?
> $A=\begin{bmatrix}1&1\\-1&3\end{bmatrix}$, $\Delta(\lambda)=\lambda^2-4\lambda+4=(\lambda-2)^2$. $N=A-2I=\begin{bmatrix}-1&1\\-1&1\end{bmatrix}$ and $N^2=0$.
> $A=2I+N$, and $2I$ commutes with $N$, so $e^{At}=e^{2t}e^{Nt}$. The series of $e^{Nt}$ stops: $e^{Nt}=I+tN$.
> $$e^{At}=e^{2t}(I+tN)=e^{2t}\begin{bmatrix}1-t&t\\-t&1+t\end{bmatrix}$$
> New term: $te^{2t}$. It appears because $A$ has only one eigenvector for $\lambda=2$ (one Jordan block of size 2).

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

> [!info] The skipped steps of P5 and P6, and the polynomial route (beyond the slides)
> **P5.** Differentiate $\frac{t^k}{k!}A^k$: the result is $\frac{t^{k-1}}{(k-1)!}A^k=A\cdot\frac{t^{k-1}}{(k-1)!}A^{k-1}$. The sum over $k\ge1$ is $A$ times the series of $e^{At}$. The factor $A$ can also be taken out on the right, so $Ae^{At}=e^{At}A$.
> 
> **P6.** $\sum_{k\ge0}A^ks^{-(k+1)}=\frac1s\bigl(I+\frac As+\frac{A^2}{s^2}+\cdots\bigr)$ is a geometric series in $A/s$. Its sum is $\frac1s\bigl(I-\frac As\bigr)^{-1}=(sI-A)^{-1}$. The series converges when $\lvert s\rvert$ is larger than every $\lvert\lambda_i\rvert$.
> 
> **Polynomial route (Cayley-Hamilton).** $\Delta(A)=0$, so $A^n$ and every higher power is a combination of $I,A,\dots,A^{n-1}$. The whole series then folds into
> $$e^{At}=\beta_0(t)I+\beta_1(t)A+\cdots+\beta_{n-1}(t)A^{n-1}$$
> The same equation holds with $A$ replaced by each eigenvalue: $e^{\lambda_it}=\beta_0+\beta_1\lambda_i+\cdots+\beta_{n-1}\lambda_i^{n-1}$. For a repeated eigenvalue also differentiate with respect to $\lambda$: $te^{\lambda_it}=\beta_1+2\beta_2\lambda_i+\cdots$. This gives $n$ equations for the $n$ unknowns $\beta_j(t)$. It is method 1 above: $h(\lambda)=\beta_0+\beta_1\lambda+\cdots$ is the interpolating polynomial.

> [!question]- Check (slide 80, P1 and P5): Two upper triangular candidates $\Phi_1(t)$, $\Phi_2(t)$ have the diagonal $e^{-t}$, $e^{-3t}$. The $(1,2)$ entry is $t$ in $\Phi_1$ and $e^{-t}-e^{-3t}$ in $\Phi_2$. Which one is a matrix exponential $e^{At}$, and of which $A$?
> $\Phi_1(t)=\begin{bmatrix}e^{-t}&t\\0&e^{-3t}\end{bmatrix}$, $\Phi_2(t)=\begin{bmatrix}e^{-t}&e^{-t}-e^{-3t}\\0&e^{-3t}\end{bmatrix}$.
> P1: both give $I$ at $t=0$. P5 at $t=0$ says $A=\frac{d}{dt}e^{At}\big|_{t=0}$.
> $\Phi_1$: $A$ would be $\dot\Phi_1(0)=\begin{bmatrix}-1&1\\0&-3\end{bmatrix}$. Test P5 in entry $(1,2)$: $\dot\Phi_1$ has $1$, but $A\Phi_1$ has $-t+e^{-3t}$. Not equal for $t\neq0$. $\Phi_1$ is not a matrix exponential.
> $\Phi_2$: $A=\dot\Phi_2(0)=\begin{bmatrix}-1&-1+3\\0&-3\end{bmatrix}=\begin{bmatrix}-1&2\\0&-3\end{bmatrix}$. Entry $(1,2)$ of $\dot\Phi_2$: $-e^{-t}+3e^{-3t}$. Entry $(1,2)$ of $A\Phi_2$: $-(e^{-t}-e^{-3t})+2e^{-3t}=-e^{-t}+3e^{-3t}$. Equal. The diagonal entries also match. So $\Phi_2=e^{At}$.

> [!question]- Check (slide 80, P3): For $A$ with rows $(1,1)$ and $(-1,3)$, $e^{At}$ is $e^{2t}$ times the matrix with rows $(1-t,\ t)$ and $(-t,\ 1+t)$. Write $[e^{At}]^{-1}$ without inverting a matrix, then test it.
> $e^{At}=e^{2t}\begin{bmatrix}1-t&t\\-t&1+t\end{bmatrix}$.
> P3: replace $t$ by $-t$.
> $$[e^{At}]^{-1}=e^{-At}=e^{-2t}\begin{bmatrix}1+t&-t\\t&1-t\end{bmatrix}$$
> Test: $e^{2t}e^{-2t}=1$, and $\begin{bmatrix}1-t&t\\-t&1+t\end{bmatrix}\begin{bmatrix}1+t&-t\\t&1-t\end{bmatrix}=\begin{bmatrix}1-t^2+t^2&-t+t^2+t-t^2\\-t-t^2+t+t^2&t^2+1-t^2\end{bmatrix}=I$.

> [!question]- Check (slide 80, P4): Take $A$ with rows $(1,0)$, $(0,0)$ and $B$ with rows $(0,1)$, $(0,0)$. Show $AB\neq BA$, then compare $e^{At}e^{Bt}$, $e^{Bt}e^{At}$ and $e^{(A+B)t}$.
> $A=\begin{bmatrix}1&0\\0&0\end{bmatrix}$, $B=\begin{bmatrix}0&1\\0&0\end{bmatrix}$.
> $AB=\begin{bmatrix}0&1\\0&0\end{bmatrix}=B$, but $BA=\begin{bmatrix}0&0\\0&0\end{bmatrix}$. They do not commute.
> $e^{At}=\begin{bmatrix}e^t&0\\0&1\end{bmatrix}$ (diagonal). $e^{Bt}=I+tB=\begin{bmatrix}1&t\\0&1\end{bmatrix}$ ($B^2=0$).
> $e^{At}e^{Bt}=\begin{bmatrix}e^t&te^t\\0&1\end{bmatrix}$, $\quad e^{Bt}e^{At}=\begin{bmatrix}e^t&t\\0&1\end{bmatrix}$.
> $A+B=\begin{bmatrix}1&1\\0&0\end{bmatrix}$ satisfies $(A+B)^2=A+B$, so $e^{(A+B)t}=I+(e^t-1)(A+B)=\begin{bmatrix}e^t&e^t-1\\0&1\end{bmatrix}$.
> The three $(1,2)$ entries are $te^t$, $t$ and $e^t-1$. All different for $t\neq0$, so P4 fails without $AB=BA$.

> [!question]- Check (slide 80, P6 Laplace route): Compute $e^{At}$ with P6 for $A$ with rows $(1,2)$ and $(3,2)$.
> $A=\begin{bmatrix}1&2\\3&2\end{bmatrix}$, $sI-A=\begin{bmatrix}s-1&-2\\-3&s-2\end{bmatrix}$, $\det=(s-1)(s-2)-6=s^2-3s-4=(s-4)(s+1)$.
> $$(sI-A)^{-1}=\frac{1}{(s-4)(s+1)}\begin{bmatrix}s-2&2\\3&s-1\end{bmatrix}$$
> Partial fractions (cover-up at $s=4$ and $s=-1$):
> $\dfrac{s-2}{(s-4)(s+1)}=\dfrac{2/5}{s-4}+\dfrac{3/5}{s+1}$, $\quad\dfrac{2}{(s-4)(s+1)}=\dfrac{2/5}{s-4}-\dfrac{2/5}{s+1}$,
> $\dfrac{3}{(s-4)(s+1)}=\dfrac{3/5}{s-4}-\dfrac{3/5}{s+1}$, $\quad\dfrac{s-1}{(s-4)(s+1)}=\dfrac{3/5}{s-4}+\dfrac{2/5}{s+1}$.
> Inverse transform entry by entry:
> $$e^{At}=\frac15\begin{bmatrix}2e^{4t}+3e^{-t}&2e^{4t}-2e^{-t}\\3e^{4t}-3e^{-t}&3e^{4t}+2e^{-t}\end{bmatrix}$$
> Test: $t=0$ gives $\frac15\begin{bmatrix}5&0\\0&5\end{bmatrix}=I$.

> [!question]- Check (slide 80, the other two routes): For the same $A$ (rows $(1,2)$ and $(3,2)$) compute $e^{At}$ by diagonalization and by the polynomial route. Show that both agree with the Laplace result.
> Eigenvalues: $4$ and $-1$.
> **Diagonalization.** $(A-4I)\mathbf{q}=\mathbf{0}$: $-3q_1+2q_2=0$, $\mathbf{q}_1=(2,3)$. $(A+I)\mathbf{q}=\mathbf{0}$: $2q_1+2q_2=0$, $\mathbf{q}_2=(1,-1)$.
> $Q=\begin{bmatrix}2&1\\3&-1\end{bmatrix}$, $\det Q=-5$, $Q^{-1}=\frac15\begin{bmatrix}1&1\\3&-2\end{bmatrix}$.
> $$e^{At}=Q\begin{bmatrix}e^{4t}&0\\0&e^{-t}\end{bmatrix}Q^{-1}=\frac15\begin{bmatrix}2e^{4t}&e^{-t}\\3e^{4t}&-e^{-t}\end{bmatrix}\begin{bmatrix}1&1\\3&-2\end{bmatrix}=\frac15\begin{bmatrix}2e^{4t}+3e^{-t}&2e^{4t}-2e^{-t}\\3e^{4t}-3e^{-t}&3e^{4t}+2e^{-t}\end{bmatrix}$$
> **Polynomial route.** $e^{At}=\beta_0I+\beta_1A$ with $\beta_0+4\beta_1=e^{4t}$ and $\beta_0-\beta_1=e^{-t}$.
> Subtract: $5\beta_1=e^{4t}-e^{-t}$, so $\beta_1=\frac{e^{4t}-e^{-t}}{5}$ and $\beta_0=e^{-t}+\beta_1=\frac{e^{4t}+4e^{-t}}{5}$.
> Entry $(1,1)$: $\beta_0+\beta_1=\frac{2e^{4t}+3e^{-t}}{5}$. Entry $(1,2)$: $2\beta_1=\frac{2e^{4t}-2e^{-t}}{5}$. Entry $(2,1)$: $3\beta_1$. Entry $(2,2)$: $\beta_0+2\beta_1=\frac{3e^{4t}+2e^{-t}}{5}$.
> All three routes give the same matrix.

> [!question]- Check (slide 80, P6 with a double pole): Use P6 for $A$ with rows $(1,1)$ and $(-1,3)$. Where does the term $te^{2t}$ come from in the Laplace route?
> $A=\begin{bmatrix}1&1\\-1&3\end{bmatrix}$, $sI-A=\begin{bmatrix}s-1&-1\\1&s-3\end{bmatrix}$, $\det=(s-1)(s-3)+1=s^2-4s+4=(s-2)^2$.
> $$(sI-A)^{-1}=\frac{1}{(s-2)^2}\begin{bmatrix}s-3&1\\-1&s-1\end{bmatrix}$$
> $\dfrac{s-3}{(s-2)^2}=\dfrac{1}{s-2}-\dfrac{1}{(s-2)^2}$ and $\dfrac{s-1}{(s-2)^2}=\dfrac{1}{s-2}+\dfrac{1}{(s-2)^2}$.
> $\mathcal{L}^{-1}\bigl\{\frac{1}{s-2}\bigr\}=e^{2t}$ and $\mathcal{L}^{-1}\bigl\{\frac{1}{(s-2)^2}\bigr\}=te^{2t}$. So
> $$e^{At}=\begin{bmatrix}e^{2t}-te^{2t}&te^{2t}\\-te^{2t}&e^{2t}+te^{2t}\end{bmatrix}$$
> The double pole at $s=2$ gives $te^{2t}$. Same result as with the series (slide 79).

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
> [!question]- 1. Compute $e^{Jt}$ for $J$ with the rows $(2,1)$ and $(0,2)$.
> $J=2I+N$, $N^2=0$: $e^{Jt}=e^{2t}(I+tN)=\begin{bmatrix}e^{2t}&te^{2t}\\0&e^{2t}\end{bmatrix}$. At $t=0$: $I$.

> [!question]- 2. Compute $e^{At}$ for $A$ with the rows $(-1,0)$ and $(0,-3)$, and for $A$ with the rows $(0,2)$ and $(-2,0)$.
> Diagonal: $\operatorname{diag}\{e^{-t},e^{-3t}\}$. Oscillator with $\omega=2$: $\begin{bmatrix}\cos2t&\sin2t\\-\sin2t&\cos2t\end{bmatrix}$.

> [!question]- 3. Compute $e^{Mt}$ for the shift $M$ with the rows $(0,1,0)$, $(0,0,1)$ and $(0,0,0)$.
> $M^2$ has a single one at $(1,3)$, $M^3=0$. $e^{Mt}=I+tM+\frac{t^2}{2}M^2=\begin{bmatrix}1&t&t^2/2\\0&1&t\\0&0&1\end{bmatrix}$.

> [!question]- 4. For $\ddot p+3\dot p+2p=0$ with $p(0)=0$, $\dot p(0)=1$, find $p(t)$.
> $\mathbf{x}(t)=e^{At}\begin{bmatrix}0\\1\end{bmatrix}$ is the second column of $e^{At}$ in the example above: $p(t)=e^{-t}-e^{-2t}$.

> [!question]- 5. Write $e^{-At}$ for the oscillator $A$ with the rows $(0,\omega)$ and $(-\omega,0)$.
> P3: replace $t$ by $-t$. $e^{-At}=\begin{bmatrix}\cos\omega t&-\sin\omega t\\ \sin\omega t&\cos\omega t\end{bmatrix}$. The product with $e^{At}$ is $I$ because $\cos^2+\sin^2=1$.

> [!question]- 6. Discretize $\dot x=-2x+u$ with a zero-order hold and $T=0.5$.
> $A_d=e^{-2\cdot0.5}=e^{-1}$. $B_d=\int_0^{0.5}e^{-2\sigma}d\sigma=\frac{1-e^{-1}}{2}$. So $x[k+1]=e^{-1}x[k]+\frac{1-e^{-1}}{2}u[k]$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L05 - Functions of a matrix]]. Next: [[EE502 L07 - Jordan form]]
- Used by the midterm and by every later lecture on the solution of state equations.
- Full step-by-step notes (PDF): [EE502_Lecture_06_Matrix_Exponential.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_06/EE502_Lecture_06_Matrix_Exponential.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_06/EE502_Lecture_06_Matrix_Exponential.pdf`
- Original slides (PDF, pp. 78-80): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L06 - Matrix exponential - quiz]]

Slides not embedded: none.
