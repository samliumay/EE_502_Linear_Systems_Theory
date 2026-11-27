---
course: EE 502 Linear System Theory
lesson: EE502 L06 - Matrix exponential
type: quiz
questions: 11
---

# EE502 L06 - Matrix exponential - quiz

Lesson note: [[EE502 L06 - Matrix exponential]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz a matrix "with the rows" $(\dots)$ is written row by row. $e^{At}=\sum_{k\ge0}\frac{t^k}{k!}A^k$ is the matrix exponential and $\mathcal{L}$ the Laplace transform.

## 1. Power series definition of f(A) (slides 78-79)

### Q1 (slide 78, Jordan block formula)

$J$ is the $3\times3$ Jordan block with the rows $(2,1,0)$, $(0,2,1)$, $(0,0,2)$. Use the formula for a function of a Jordan block with $f(\lambda)=1/\lambda$ to find $J^{-1}$.

- A) $\begin{bmatrix}\tfrac12&-\tfrac14&\tfrac18\\0&\tfrac12&-\tfrac14\\0&0&\tfrac12\end{bmatrix}$
- B) $\begin{bmatrix}\tfrac12&-\tfrac14&\tfrac14\\0&\tfrac12&-\tfrac14\\0&0&\tfrac12\end{bmatrix}$
- C) $\begin{bmatrix}\tfrac12&\tfrac14&\tfrac18\\0&\tfrac12&\tfrac14\\0&0&\tfrac12\end{bmatrix}$
- D) $\begin{bmatrix}\tfrac12&\tfrac14&\tfrac14\\0&\tfrac12&\tfrac14\\0&0&\tfrac12\end{bmatrix}$

> [!success]- Answer
> **A.** $f(J)$ has $f(\lambda_1)$ on the diagonal, $f'(\lambda_1)$ on the first superdiagonal and $f''(\lambda_1)/2!$ on the second.
> $f=\lambda^{-1}$, $f'=-\lambda^{-2}$, $f''=2\lambda^{-3}$. At $\lambda_1=2$: $f=\tfrac12$, $f'=-\tfrac14$, $f''/2!=\tfrac{2/8}{2}=\tfrac18$.
> Test, first row of $JJ^{-1}$: $[1,\ -\tfrac12+\tfrac12,\ \tfrac14-\tfrac14]=[1\ \ 0\ \ 0]$.
> - B: The corner is $f''(2)=\tfrac14$: the factor $1/2!$ was forgotten.
> - C: The sign of $f'=-\lambda^{-2}$ was lost on the first superdiagonal.
> - D: Both slips together: the sign of $f'$ lost and the $1/2!$ forgotten.

### Q2 (slide 78, convergence)

$\ln(1+\lambda)=\lambda-\frac{\lambda^2}{2}+\frac{\lambda^3}{3}-\cdots$ is a power series about $a=0$ with radius $\rho=1$. $A$ has the rows $(0.5,\ 100)$ and $(0,\ -0.5)$. $B$ has the rows $(0,\ -2)$ and $(2,\ 0)$. Does the convergence condition of the slide guarantee that the matrix series converges for $A$? For $B$?

- A) For $A$: yes. For $B$: yes.
- B) For $A$: yes. For $B$: no.
- C) For $A$: no. For $B$: no.
- D) For $A$: no. For $B$: yes.

> [!success]- Answer
> **B.** The condition is on the eigenvalues only: every $\lvert\lambda_i-a\rvert<\rho$.
> $A$ is triangular, eigenvalues $0.5$ and $-0.5$, both with $\lvert\lambda_i\rvert=0.5<1$. Guaranteed, even with the entry 100.
> $B$: $\Delta(\lambda)=\lambda^2+4$, eigenvalues $\pm2j$, $\lvert\lambda_i\rvert=2>1$. No guarantee (here the series in fact diverges).
> - A: This tests the diagonal entries ($0.5,-0.5$ and $0,0$) instead of the eigenvalues. For $B$ they are not the eigenvalues.
> - C: This tests the size of the entries (100 and 2 are larger than 1). The entries do not matter, only the eigenvalues.
> - D: For $A$ the entry 100 was used; for $B$ only the real part 0 of $\pm2j$. The condition uses the full modulus $\lvert\lambda_i\rvert$.

### Q3 (slide 79, series stops)

$A$ is the $3\times3$ matrix with the rows $(0,2,1)$, $(0,0,3)$, $(0,0,0)$. Compute $e^{At}$ from the power series. What is its $(1,3)$ entry?

- A) $t+6t^2$
- B) $t+3t^2$
- C) $t$
- D) $e^{t}$

> [!success]- Answer
> **B.** $A^2$ has the single entry $2\cdot3=6$ at $(1,3)$, and $A^3=0$. So the series stops: $e^{At}=I+tA+\frac{t^2}{2!}A^2$.
> Entry $(1,3)$: $0+t\cdot1+\frac{t^2}{2}\cdot6=t+3t^2$.
> - A: The $1/2!$ in front of $t^2A^2$ was forgotten.
> - C: The series was stopped after $I+tA$. $A^2\neq0$, so the term $\frac{t^2}{2}A^2$ is still there.
> - D: This is $e$ to the entry $1$ times $t$: $e^{At}$ taken entrywise. The matrix exponential is not computed entry by entry.

### Q4 (slide 79, series does not stop)

$A$ has the rows $(1,1)$ and $(0,0)$. Then $A^2=A$. Sum the power series and write $e^{At}=I+g(t)A$. What is $g(t)$?

- A) $g(t)=e^{t}$
- B) $g(t)=t$
- C) $g(t)=e^{t}-1$
- D) $g(t)=\dfrac{t}{1-t}$ for $\lvert t\rvert<1$

> [!success]- Answer
> **C.** $A^2=A$ gives $A^k=A$ for every $k\ge1$. The $k=0$ term is $I$.
> $e^{At}=I+\Bigl(t+\frac{t^2}{2!}+\frac{t^3}{3!}+\cdots\Bigr)A=I+(e^t-1)A$, because the bracket is the series of $e^t$ without its first term 1.
> Test: $t=0$ gives $I$.
> - A: The first term 1 was left in the bracket. But the $k=0$ term is $I$, already written separately, so $e^t$ counts it twice.
> - B: Only the $k=1$ term was kept, as if $A^2=0$. Here $A^2=A\neq0$, so the series does not stop.
> - D: The $1/k!$ was forgotten: $t+t^2+t^3+\cdots=\frac{t}{1-t}$ is a geometric series.

### Q5 (slide 79, repeated eigenvalue)

$A$ has the rows $(1,1)$ and $(-1,3)$ and the double eigenvalue 2. Let $N=A-2I$, so $A=2I+N$ and $N^2=0$. Find $e^{At}$.

- A) $\begin{bmatrix}e^{2t}-t&t\\-t&e^{2t}+t\end{bmatrix}$
- B) $\begin{bmatrix}(1+t)e^{2t}&-te^{2t}\\te^{2t}&(1-t)e^{2t}\end{bmatrix}$
- C) $\begin{bmatrix}e^{2t}&0\\0&e^{2t}\end{bmatrix}$
- D) $\begin{bmatrix}(1-t)e^{2t}&te^{2t}\\-te^{2t}&(1+t)e^{2t}\end{bmatrix}$

> [!success]- Answer
> **D.** $N=\begin{bmatrix}-1&1\\-1&1\end{bmatrix}$, $N^2=0$. $2I$ commutes with $N$, so $e^{At}=e^{2t}e^{Nt}$, and the series of $e^{Nt}$ stops: $e^{Nt}=I+tN$.
> $e^{At}=e^{2t}(I+tN)=e^{2t}\begin{bmatrix}1-t&t\\-t&1+t\end{bmatrix}$. The new term is $te^{2t}$.
> - A: This is $e^{2t}I+tN$: the sum $2I+N$ in the exponent was turned into a sum of exponentials. The rule is a product, $e^{2t}e^{Nt}$.
> - B: This uses $N=2I-A$, the wrong sign. It gives $e^{2t}(I-tN)$.
> - C: The $te^{2t}$ term was forgotten, as if $A$ were $2I$. $A$ has one Jordan block of size 2, so $te^{2t}$ must appear.

## 2. Properties of the matrix exponential (slide 80)

### Q6 (slide 80, P1 and P5)

Two candidates have the same diagonal $e^{-t}$, $e^{-3t}$ and a zero $(2,1)$ entry. The $(1,2)$ entry is $t$ in $\Phi_1(t)$ and $e^{-t}-e^{-3t}$ in $\Phi_2(t)$. Let $M_1$, $M_2$, $M_3$ be the matrices with the rows $(-1,\ 1),(0,\ -3)$, then $(-1,\ 2),(0,\ -3)$, then $(-1,\ -4),(0,\ -3)$. Which candidate is a matrix exponential $e^{At}$, and for which $A$?

- A) Only $\Phi_1$, with $A=M_1$.
- B) Both, with $A=M_1$ and $A=M_2$.
- C) Only $\Phi_2$, with $A=M_2$.
- D) Only $\Phi_2$, with $A=M_3$.

> [!success]- Answer
> **C.** Both give $I$ at $t=0$ (P1). P5 says $A=\dot\Phi(0)$, and then $\dot\Phi(t)=A\Phi(t)$ must hold for every $t$.
> $\Phi_2$: entry $(1,2)$ of $\dot\Phi_2$ is $-e^{-t}+3e^{-3t}$, which is $2$ at $t=0$, so $A=M_2$. Entry $(1,2)$ of $M_2\Phi_2$: $-(e^{-t}-e^{-3t})+2e^{-3t}=-e^{-t}+3e^{-3t}$. Equal.
> $\Phi_1$: $\dot\Phi_1(0)=M_1$. Entry $(1,2)$: $\dot\Phi_1$ has $1$, but $M_1\Phi_1$ has $-t+e^{-3t}$. Not equal for $t\neq0$.
> - A: $\Phi_1$ passes P1 and gives an $A$ at $t=0$, but P5 fails for $t\neq0$.
> - B: P5 was tested only at $t=0$. That test always gives some matrix; it must also hold for $t\neq0$.
> - D: The derivative of $-e^{-3t}$ was taken as $-3e^{-3t}$: then $-1-3=-4$. The right derivative is $+3e^{-3t}$.

### Q7 (slide 80, P3)

$A$ has the rows $(3,4)$ and $(-1,-1)$. Its matrix exponential is $e^{At}=e^{t}\begin{bmatrix}1+2t&4t\\-t&1-2t\end{bmatrix}$. Without inverting a matrix, write $[e^{At}]^{-1}=e^{-t}\tilde M(t)$. What is $\tilde M(t)$?

- A) $\begin{bmatrix}1+2t&4t\\-t&1-2t\end{bmatrix}$
- B) $\begin{bmatrix}1-2t&t\\-4t&1+2t\end{bmatrix}$
- C) $\begin{bmatrix}1-2t&-4t\\t&1+2t\end{bmatrix}$
- D) $\begin{bmatrix}1+2t&-t\\4t&1-2t\end{bmatrix}$

> [!success]- Answer
> **C.** P3: $[e^{At}]^{-1}=e^{-At}$, so replace $t$ by $-t$ everywhere: $e^{-t}\begin{bmatrix}1-2t&-4t\\t&1+2t\end{bmatrix}$.
> Test: $(1+2t)(1-2t)+4t\cdot t=1$ and $(1+2t)(-4t)+4t(1+2t)=0$; the other two entries of the product also give $0$ and $1$.
> - A: $t$ was replaced by $-t$ only in the scalar $e^{t}$, not inside the matrix.
> - B: This is $e^{-A^{\mathsf T}t}$, the transpose of the right answer. The inverse of $e^{At}$ is $e^{-At}$, with no transpose.
> - D: This is the transpose of the matrix part, as if the inverse were the transpose. That holds only for a rotation, such as the oscillator.

### Q8 (slide 80, P4)

$A$ has the rows $(1,0)$, $(0,0)$ and $B$ has the rows $(0,1)$, $(0,0)$, so $AB\neq BA$. Look at the $(1,2)$ entries of $e^{At}e^{Bt}$, of $e^{Bt}e^{At}$ and of $e^{(A+B)t}$, in this order.

- A) $t$, $\ te^{t}$, $\ e^{t}-1$
- B) $te^{t}$, $\ t$, $\ e^{t}-1$
- C) $te^{t}$, $\ t$, $\ te^{t}$
- D) $t$, $\ te^{t}$, $\ t$

> [!success]- Answer
> **B.** $e^{At}=\begin{bmatrix}e^t&0\\0&1\end{bmatrix}$ ($A$ diagonal) and $e^{Bt}=I+tB=\begin{bmatrix}1&t\\0&1\end{bmatrix}$ ($B^2=0$).
> $e^{At}e^{Bt}=\begin{bmatrix}e^t&te^t\\0&1\end{bmatrix}$ and $e^{Bt}e^{At}=\begin{bmatrix}e^t&t\\0&1\end{bmatrix}$.
> $(A+B)^2=A+B$, so $e^{(A+B)t}=I+(e^t-1)(A+B)$, with $(1,2)$ entry $e^t-1$. All three differ for $t\neq0$: P4 needs $AB=BA$.
> - A: The two products were swapped: $e^{At}e^{Bt}$ multiplies row 1 of $e^{At}$, $(e^t,0)$, with column 2 of $e^{Bt}$, $(t,1)$, which gives $te^t$.
> - C: P4 was used without $AB=BA$: $e^{(A+B)t}=e^{At}e^{Bt}$ is false here.
> - D: The products were swapped, and then P4 was used without $AB=BA$: $e^{(A+B)t}$ was set equal to the (wrong) value of $e^{At}e^{Bt}$. Both steps are wrong.

### Q9 (slide 80, P6 Laplace route)

$A$ has the rows $(1,2)$ and $(3,2)$. Use P6, $\mathcal{L}\{e^{At}\}=(sI-A)^{-1}$, with partial fractions to find $e^{At}$.

- A) $\frac15\begin{bmatrix}3e^{t}+2e^{-4t}&2e^{-4t}-2e^{t}\\3e^{-4t}-3e^{t}&2e^{t}+3e^{-4t}\end{bmatrix}$
- B) $\begin{bmatrix}e^{t}&e^{2t}\\e^{3t}&e^{2t}\end{bmatrix}$
- C) $\frac15\begin{bmatrix}3e^{4t}+2e^{-t}&2e^{4t}-2e^{-t}\\3e^{4t}-3e^{-t}&2e^{4t}+3e^{-t}\end{bmatrix}$
- D) $\frac15\begin{bmatrix}2e^{4t}+3e^{-t}&2e^{4t}-2e^{-t}\\3e^{4t}-3e^{-t}&3e^{4t}+2e^{-t}\end{bmatrix}$

> [!success]- Answer
> **D.** $\det(sI-A)=(s-1)(s-2)-6=(s-4)(s+1)$ and $(sI-A)^{-1}=\frac{1}{(s-4)(s+1)}\begin{bmatrix}s-2&2\\3&s-1\end{bmatrix}$.
> Cover-up: $\frac{s-2}{(s-4)(s+1)}=\frac{2/5}{s-4}+\frac{3/5}{s+1}$, $\frac{2}{(s-4)(s+1)}=\frac{2/5}{s-4}-\frac{2/5}{s+1}$, $\frac{3}{(s-4)(s+1)}=\frac{3/5}{s-4}-\frac{3/5}{s+1}$, $\frac{s-1}{(s-4)(s+1)}=\frac{3/5}{s-4}+\frac{2/5}{s+1}$.
> Inverse transform entry by entry gives D. Test: $t=0$ gives $I$.
> - A: This uses $(sI+A)^{-1}$. Its inverse transform is $e^{-At}$, with the modes $e^{-4t}$ and $e^{t}$.
> - B: This is $e^{At}$ taken entrywise ($e$ to each entry times $t$). It is not $I$ at $t=0$.
> - C: The diagonal of the adjugate was not swapped: $s-1$ was put at $(1,1)$ and $s-2$ at $(2,2)$.

### Q10 (slide 80, the other two routes)

$A$ has the rows $(1,2)$ and $(3,2)$. By the polynomial route (Cayley-Hamilton), $e^{At}=\beta_0(t)I+\beta_1(t)A$, and the same equation holds with $A$ replaced by each eigenvalue of $A$. What is $\beta_1(t)$?

- A) $\beta_1(t)=\frac15\bigl(e^{4t}-e^{-t}\bigr)$
- B) $\beta_1(t)=\frac15\bigl(e^{4t}+4e^{-t}\bigr)$
- C) $\beta_1(t)=\frac13\bigl(e^{4t}-e^{-t}\bigr)$
- D) $\beta_1(t)=\frac15\bigl(e^{-t}-e^{4t}\bigr)$

> [!success]- Answer
> **A.** $\Delta(\lambda)=\lambda^2-3\lambda-4=(\lambda-4)(\lambda+1)$, eigenvalues $4$ and $-1$.
> $\beta_0+4\beta_1=e^{4t}$ and $\beta_0-\beta_1=e^{-t}$. Subtract: $5\beta_1=e^{4t}-e^{-t}$.
> Then $\beta_0=e^{-t}+\beta_1=\frac15(e^{4t}+4e^{-t})$. Test: entry $(1,2)$ of $\beta_0I+\beta_1A$ is $2\beta_1$, the same as by diagonalization.
> - B: This is $\beta_0$, not $\beta_1$: the two unknowns were swapped.
> - C: The eigenvalue $-1$ was used as $+1$: $\beta_0+\beta_1=e^{-t}$ gives $3\beta_1=e^{4t}-e^{-t}$.
> - D: The equations were subtracted in the other order, $-5\beta_1=e^{-t}-e^{4t}$, and the minus sign of $-5\beta_1$ was dropped.

### Q11 (slide 80, P6 with a double pole)

$A$ has the rows $(0,1)$ and $(-4,-4)$. Its characteristic polynomial is $(\lambda+2)^2$. Use P6, $\mathcal{L}\{e^{At}\}=(sI-A)^{-1}$, to find the $(1,1)$ entry of $e^{At}$.

- A) $(1+2t)e^{-2t}$
- B) $3e^{-2t}$
- C) $(1-2t)e^{-2t}$
- D) $(1+2t)e^{2t}$

> [!success]- Answer
> **A.** $(sI-A)^{-1}=\frac{1}{(s+2)^2}\begin{bmatrix}s+4&1\\-4&s\end{bmatrix}$. Entry $(1,1)$: $\frac{s+4}{(s+2)^2}=\frac{1}{s+2}+\frac{2}{(s+2)^2}$.
> $\mathcal{L}^{-1}\{\frac{1}{s+2}\}=e^{-2t}$ and $\mathcal{L}^{-1}\{\frac{1}{(s+2)^2}\}=te^{-2t}$. So the entry is $e^{-2t}+2te^{-2t}$.
> The double pole at $s=-2$ is the source of the term $te^{-2t}$.
> - B: $\frac{2}{(s+2)^2}$ was inverted as $2e^{-2t}$: the $t$ factor of the double pole was forgotten.
> - C: The diagonal of the adjugate was not swapped: $\frac{s}{(s+2)^2}=\frac{1}{s+2}-\frac{2}{(s+2)^2}$ is the $(2,2)$ entry.
> - D: The pole $s=-2$ was read as $e^{2t}$. A pole at $s=p$ gives $e^{pt}$.
