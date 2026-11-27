---
course: EE 502 Linear System Theory
lesson: EE502 L05 - Functions of a matrix
type: quiz
questions: 12
---

# EE502 L05 - Functions of a matrix - quiz

Lesson note: [[EE502 L05 - Functions of a matrix]]. One question per check question of the lesson. Pick an option, then open the answer.

In this quiz all vectors are column vectors. $(a,b)$ is short for $[a\ \ b]^{\mathsf T}$. A matrix "with the rows" $(\dots)$ is written row by row. $\Delta(\lambda)=\det(\lambda I-A)$ is the characteristic polynomial and $\Psi(\lambda)$ the minimal polynomial.

## 1. Polynomials of a matrix (slide 69)

### Q1 (slide 69)

$A$ has the rows $(4,\ 1)$ and $(2,\ 3)$. The columns of $Q$ are the eigenvectors $(1,-2)$ and $(1,1)$, so $Q^{-1}AQ=\operatorname{diag}(2,5)$. Use the similarity rule $f(Q^{-1}AQ)=Q^{-1}f(A)Q$ to find $A^3$.

- A) $\begin{bmatrix}86&-39\\-78&47\end{bmatrix}$
- B) $\begin{bmatrix}86&39\\78&47\end{bmatrix}$
- C) $\begin{bmatrix}64&1\\8&27\end{bmatrix}$
- D) $\begin{bmatrix}47&-39\\-78&86\end{bmatrix}$

> [!success]- Answer
> **B.** From $\hat A^3=Q^{-1}A^3Q$ we get $A^3=Q\hat A^3Q^{-1}$ with $\hat A^3=\operatorname{diag}(8,125)$.
> $Q=\begin{bmatrix}1&1\\-2&1\end{bmatrix}$, $\det Q=3$, $Q^{-1}=\frac13\begin{bmatrix}1&-1\\2&1\end{bmatrix}$.
> $Q\hat A^3=\begin{bmatrix}8&125\\-16&125\end{bmatrix}$, and $A^3=\frac13\begin{bmatrix}258&117\\234&141\end{bmatrix}=\begin{bmatrix}86&39\\78&47\end{bmatrix}$.
> - A: This is $Q^{-1}\hat A^3Q$. The rule was solved in the wrong direction: $A^3=Q\hat A^3Q^{-1}$, not $Q^{-1}\hat A^3Q$.
> - C: This cubes every entry of $A$. $f(A)$ is not $f$ applied entrywise: the entries of $A^3$ come from matrix products.
> - D: This uses $\operatorname{diag}(125,8)$. The order of the eigenvalues must follow the order of the columns of $Q$: $(1,-2)$ belongs to 2, $(1,1)$ to 5.

## 2. Cayley-Hamilton theorem (slide 70)

### Q2 (slide 70)

$A$ has the rows $(1,\ 2)$ and $(3,\ 4)$. Use the Cayley-Hamilton theorem to write $A^3=\alpha A+\beta I$. Which $\alpha$ and $\beta$?

- A) $\alpha=27$ and $\beta=-10$
- B) $\alpha=23$ and $\beta=-10$
- C) $\alpha=27$ and $\beta=10$
- D) $\alpha=23$ and $\beta=10$

> [!success]- Answer
> **C.** $\Delta(\lambda)=(\lambda-1)(\lambda-4)-2\cdot3=\lambda^2-5\lambda-2$. Cayley-Hamilton: $A^2-5A-2I=0$, so $A^2=5A+2I$.
> Multiply by $A$: $A^3=5A^2+2A=5(5A+2I)+2A=27A+10I$.
> Test: $A^2=\begin{bmatrix}7&10\\15&22\end{bmatrix}=5A+2I$ holds, and $A^3=27A+10I=\begin{bmatrix}37&54\\81&118\end{bmatrix}$.
> - A: This comes from $A^2=-5A+2I$: the term $-5A$ was moved to the other side without a sign change. Then $A^3=-5A^2+2A=27A-10I$.
> - B: This comes from $A^2=5A-2I$: the constant $-2I$ was moved without a sign change. Then $A^3=5A^2-2A=23A-10I$.
> - D: $A^2=5A+2I$ is right, but after multiplying by $A$ the sign of $2A$ was lost: $5A^2-2A=25A+10I-2A=23A+10I$.

## 3. Minimal polynomial (slides 71-73)

### Q3 (slide 71)

The $4\times4$ matrix $A$ has $\lambda_0$ on the diagonal, a 1 at position $(1,2)$, and 0 everywhere else. Its characteristic polynomial is $\Delta(\lambda)=(\lambda-\lambda_0)^4$. What are the sizes of its Jordan blocks, and what is $\Psi(\lambda)$?

- A) Blocks of sizes 2, 1, 1, and $\Psi(\lambda)=(\lambda-\lambda_0)^2$.
- B) Blocks of sizes 2, 1, 1, and $\Psi(\lambda)=(\lambda-\lambda_0)^4$.
- C) Blocks of sizes 2 and 2, and $\Psi(\lambda)=(\lambda-\lambda_0)^2$.
- D) Blocks of sizes 2 and 2, and $\Psi(\lambda)=(\lambda-\lambda_0)^4$.

> [!success]- Answer
> **A.** The 1 at $(1,2)$ ties rows 1 and 2 into one block of size 2. Rows 3 and 4 have no 1 above the diagonal, so they are two blocks of size 1.
> $N=A-\lambda_0I$ has a single 1 at $(1,2)$, so $N\neq0$. In $N^2$ this 1 would need a nonzero entry in row 2 of $N$, but row 2 is zero. So $N^2=0$.
> $\Psi(\lambda)=(\lambda-\lambda_0)^2$: the exponent is the size of the largest block. $\Delta$ does not change, because the diagonal does not change.
> - B: The blocks are right, but this takes $\Psi=\Delta$. $N^2=0$ already, so a polynomial of degree 2 gives zero at $A$.
> - C: A block of size 2 needs a 1 above the diagonal inside it. Position $(3,4)$ holds 0, so rows 3 and 4 are separate blocks of size 1.
> - D: Two mistakes: rows 3 and 4 are not one block (entry $(3,4)$ is 0), and $\Psi$ is not $\Delta$, because $N^2=0$.

### Q4 (slide 72)

In the proof that $\Psi$ is unique, $\Phi=\Psi q+r$ with $\deg r<\deg\Psi$ and $r(A)=0$. The proof says that $r\not\equiv0$ would contradict the least degree of $\Psi$. But $r$ may not be monic, and the definition of $\Psi$ speaks about monic polynomials. Why is it still a contradiction?

- A) $r$ is the remainder of a division by the monic $\Psi$, so $r$ is itself monic and of lower degree.
- B) Divide $r$ by its leading coefficient: the result is monic, has lower degree than $\Psi$ and gives zero at $A$.
- C) No nonzero polynomial of degree below $n$ can give the zero matrix at an $n\times n$ matrix $A$.
- D) By Cayley-Hamilton every $p$ with $p(A)=0$ is a multiple of $\Delta$. As $\deg r<\deg\Delta$, $r\equiv0$.

> [!success]- Answer
> **B.** Let $c\neq0$ be the leading coefficient of $r$ and $\tilde r=r/c$. Then $\tilde r$ is monic and $\deg\tilde r=\deg r<\deg\Psi$.
> $\tilde r(A)=\frac1c\,r(A)=0$. So $\tilde r$ is a monic polynomial of lower degree than $\Psi$ with $\tilde r(A)=0$. This is impossible, so $r\equiv0$.
> - A: A remainder need not be monic. For example, dividing $\lambda^2$ by $\lambda^2-3\lambda+2$ leaves $3\lambda-2$, with leading coefficient 3.
> - C: This is false. $\Psi$ itself can have degree below $n$: for $A=\lambda_0I_n$, $\Psi=\lambda-\lambda_0$ has degree 1.
> - D: Cayley-Hamilton only says $\Delta(A)=0$. It does not say that $\Delta$ divides every $p$ with $p(A)=0$. For $A=I_2$, $p=\lambda-1$ gives $p(A)=0$, but $\Delta=(\lambda-1)^2$ does not divide it. The divisibility holds for $\Psi$, and that is what the proof wants to show.

### Q5 (slide 73)

A Jordan form $J_A$ has the eigenvalue $2$ with blocks of sizes 3 and 1, and the eigenvalue $-1$ with blocks of sizes 2 and 2. What are $\Delta(\lambda)$ and $\Psi(\lambda)$?

- A) $\Delta=(\lambda-2)^4(\lambda+1)^4$ and $\Psi=(\lambda-2)^3(\lambda+1)^2$.
- B) $\Delta=(\lambda-2)^4(\lambda+1)^4$ and $\Psi=(\lambda-2)^4(\lambda+1)^4$.
- C) $\Delta=(\lambda-2)^3(\lambda+1)^2$ and $\Psi=(\lambda-2)^4(\lambda+1)^4$.
- D) $\Delta=(\lambda-2)^3(\lambda+1)^2$ and $\Psi=(\lambda-2)^3(\lambda+1)^2$.

> [!success]- Answer
> **A.** $n=3+1+2+2=8$. The multiplicity $n_i$ is the sum of the block sizes of $\lambda_i$: $n_1=3+1=4$, $n_2=2+2=4$. So $\Delta=(\lambda-2)^4(\lambda+1)^4$.
> The index $m_i$ is the size of the largest block: $m_1=3$, $m_2=2$. So $\Psi=(\lambda-2)^3(\lambda+1)^2$, of degree 5.
> $(\lambda-2)^3$ is forced by the block of size 3, $(\lambda+1)^2$ by a block of size 2 of $-1$.
> - B: $\Delta$ is right, but this takes $\Psi=\Delta$. The exponents of $\Psi$ are the largest block sizes, not the multiplicities.
> - C: The two definitions are swapped. $\Delta$ must have degree $n=8$, and $\Psi$ divides $\Delta$, so $\Psi$ cannot have the larger exponents.
> - D: $\Delta$ was built from the largest blocks only. Then $\deg\Delta=5\neq n=8$. Every block counts for $\Delta$.

## 4. Indices and the interpolating polynomial (slide 74)

### Q6 (slide 74, indices)

$A$ is $3\times3$ with 2 on the diagonal and 1 everywhere else. Its characteristic polynomial is $(\lambda-1)^2(\lambda-4)$. What are $\Psi$ and the indices, and is $A$ diagonalizable?

- A) $\Psi=(\lambda-1)^2(\lambda-4)$, indices 2 and 1, not diagonalizable.
- B) $\Psi=(\lambda-1)(\lambda-4)$, indices 1 and 1, not diagonalizable.
- C) $\Psi=(\lambda-1)(\lambda-4)$, indices 1 and 1, diagonalizable.
- D) $\Psi=(\lambda-1)^2(\lambda-4)$, indices 2 and 1, diagonalizable.

> [!success]- Answer
> **C.** $\Psi$ divides $\Delta$ and has both eigenvalues as roots. Test the smaller candidate $(\lambda-1)(\lambda-4)$.
> Every row of $A-I$ is $(1,1,1)$. Every column of $A-4I$ sums to $-2+1+1=0$. So every entry of $(A-I)(A-4I)$ is a column sum of $A-4I$, and $(A-I)(A-4I)=0$.
> So $\Psi=(\lambda-1)(\lambda-4)$, $m_1=m_2=1$, and $A$ is diagonalizable.
> - A: This takes $\Psi=\Delta$ without testing the smaller candidate. $(A-I)(A-4I)=0$ already.
> - B: $\Psi$ and the indices are right, but a repeated eigenvalue does not mean "not diagonalizable". All indices are 1, so $A$ is diagonalizable.
> - D: $\Psi$ is wrong (it is not $\Delta$, see A), and the parts contradict each other: an index 2 would mean $A$ is not diagonalizable.

### Q7 (slide 74, interpolating polynomial)

$A$ has the rows $(0,\ 1)$ and $(-2,\ -3)$. For $f(\lambda)=e^{\lambda t}$ the interpolating polynomial is $h(\lambda)=h_0+h_1\lambda$, and $e^{At}=h_0I+h_1A$. Which $h_0$ and $h_1$?

- A) $h_0=e^{-2t}$ and $h_1=e^{-t}-e^{-2t}$
- B) $h_0=2e^{-t}-e^{-2t}$ and $h_1=e^{-2t}-e^{-t}$
- C) $h_0=e^{-2t}$ and $h_1=e^{-2t}-e^{-t}$
- D) $h_0=2e^{-t}-e^{-2t}$ and $h_1=e^{-t}-e^{-2t}$

> [!success]- Answer
> **D.** $\Delta(\lambda)=\lambda(\lambda+3)+2=(\lambda+1)(\lambda+2)$. Eigenvalues $-1$ and $-2$, both simple, so only value conditions.
> $h(-1)=e^{-t}$: $h_0-h_1=e^{-t}$. $h(-2)=e^{-2t}$: $h_0-2h_1=e^{-2t}$.
> First minus second: $h_1=e^{-t}-e^{-2t}$. Then $h_0=e^{-t}+h_1=2e^{-t}-e^{-2t}$.
> Test at $t=0$: $h_0=1$, $h_1=0$, so $e^{A\cdot0}=I$.
> - A: $h_1$ is right, but $h_0$ was taken as $e^{-t}-h_1$. From $h_0-h_1=e^{-t}$ it is $h_0=e^{-t}+h_1$.
> - B: $h$ was evaluated at $+1$ and $+2$: $h_0+h_1=e^{-t}$, $h_0+2h_1=e^{-2t}$. The conditions must use the eigenvalues $-1$ and $-2$ on both sides.
> - C: Second minus first gives $-h_1=e^{-2t}-e^{-t}$. The minus sign on $h_1$ was lost, and then $h_0=e^{-t}+h_1$ is wrong too.

## 5. Examples: A^100, e^{At}, f of a Jordan block (slides 75-77)

### Q8 (slide 75, remainder)

$A$ has the rows $(0,\ 1)$ and $(-2,\ 3)$, so $\Delta(\lambda)=\lambda^2-3\lambda+2$. For $f(\lambda)=\lambda^3$, the interpolating polynomial $h$ is the remainder of $f$ divided by $\Delta$. What is $h(\lambda)$?

- A) $h(\lambda)=7\lambda-6$
- B) $h(\lambda)=7\lambda+6$
- C) $h(\lambda)=\lambda+3$
- D) $h(\lambda)=11\lambda+6$

> [!success]- Answer
> **A.** $\lambda^3=(\lambda^2-3\lambda+2)\lambda+(3\lambda^2-2\lambda)$, and $3\lambda^2-2\lambda=3(\lambda^2-3\lambda+2)+(7\lambda-6)$.
> So $\lambda^3=\Delta(\lambda)(\lambda+3)+7\lambda-6$, and $h=7\lambda-6$.
> Check with Definition 1: the eigenvalues are 1 and 2, $h(1)=1=1^3$, $h(2)=8=2^3$. Then $A^3=7A-6I=\begin{bmatrix}-6&7\\-14&15\end{bmatrix}$.
> - B: This is the remainder for $\lambda^2+3\lambda+2$, a sign slip in $\Delta$. Check: $h(1)=13\neq1$.
> - C: This is the quotient $q$, not the remainder. $f=\Delta q+r$, and $h=r$.
> - D: This is the remainder for $\lambda^2-3\lambda-2$, a sign slip in the constant of $\Delta$. Check: $h(1)=17\neq1$.

### Q9 (slide 75, Example 1)

$A$ has the rows $(3,\ 1)$ and $(-1,\ 1)$. Compute $A^{10}$ with an interpolating polynomial $h(\lambda)=h_0+h_1\lambda$.

- A) $\begin{bmatrix}11264&5120\\-5120&1024\end{bmatrix}$
- B) $\begin{bmatrix}1024&0\\0&1024\end{bmatrix}$
- C) $\begin{bmatrix}11264&10240\\-10240&-9216\end{bmatrix}$
- D) $\begin{bmatrix}6144&5120\\-5120&-4096\end{bmatrix}$

> [!success]- Answer
> **D.** $\Delta(\lambda)=(\lambda-3)(\lambda-1)+1=(\lambda-2)^2$: one eigenvalue 2 with $n_1=2$, so a value and a derivative condition.
> $h(2)=2^{10}$: $h_0+2h_1=1024$. $h'(2)=f'(2)$: $h_1=10\cdot2^9=5120$. So $h_0=1024-10240=-9216$.
> $A^{10}=-9216\,I+5120\,A=\begin{bmatrix}-9216+15360&5120\\-5120&-9216+5120\end{bmatrix}=\begin{bmatrix}6144&5120\\-5120&-4096\end{bmatrix}$.
> - A: $h_1=5120$ is right, but $h_0$ was taken as $1024-h_1=-4096$. The factor 2 in $h_0+2h_1$ was lost.
> - B: This uses only the value condition, as if $\Psi=\lambda-2$ and $A=2I$. The derivative condition for the double eigenvalue is missing, and $A\neq2I$.
> - C: The derivative was taken as $10\cdot2^{10}=10240$ instead of $10\cdot2^9$. Then $h_0=1024-20480=-19456$.

### Q10 (slide 76)

For $A$ with the rows $(0,\ 0,\ -2)$, $(0,\ 1,\ 0)$, $(1,\ 0,\ 3)$ the slide finds $e^{At}=h_0I+h_1A+h_2A^2$ with

$$h_0=-2te^t+e^{2t},\qquad h_1=3te^t+2e^t-2e^{2t},\qquad h_2=-te^t-e^t+e^{2t}$$

At $t=0$ they give $(h_0,h_1,h_2)=(1,0,0)$, so $e^{A\cdot0}=I$. What are the derivatives $(\dot h_0,\dot h_1,\dot h_2)=\left(\frac{dh_0}{dt},\frac{dh_1}{dt},\frac{dh_2}{dt}\right)$ at $t=0$?

- A) $(\dot h_0,\dot h_1,\dot h_2)=(2,\ -2,\ 1)$
- B) $(\dot h_0,\dot h_1,\dot h_2)=(0,\ 1,\ 0)$
- C) $(\dot h_0,\dot h_1,\dot h_2)=(-1,\ 3,\ -1)$
- D) $(\dot h_0,\dot h_1,\dot h_2)=(1,\ 0,\ 0)$

> [!success]- Answer
> **B.** Use $\frac{d}{dt}(te^t)=e^t+te^t$ (product rule) and $\frac{d}{dt}e^{2t}=2e^{2t}$ (chain rule):
> $\dot h_0=-2e^t-2te^t+2e^{2t}$, $\dot h_1=3e^t+3te^t+2e^t-4e^{2t}$, $\dot h_2=-e^t-te^t-e^t+2e^{2t}$.
> At $t=0$: $\dot h_0=-2+2=0$, $\dot h_1=3+2-4=1$, $\dot h_2=-1-1+2=0$. So $\frac{d}{dt}e^{At}$ at $t=0$ is $0\cdot I+1\cdot A+0\cdot A^2=A$, as $\frac{d}{dt}e^{At}=Ae^{At}$ requires.
> - A: $\frac{d}{dt}(te^t)$ was taken as $te^t$, without the product rule. Then $\dot h_0=-2te^t+2e^{2t}$, $\dot h_1=3te^t+2e^t-4e^{2t}$, $\dot h_2=-te^t-e^t+2e^{2t}$, which give $(2,-2,1)$ at $t=0$.
> - C: $\frac{d}{dt}e^{2t}$ was taken as $e^{2t}$, without the factor 2 of the chain rule. Then $\dot h_0(0)=-2+1=-1$, $\dot h_1(0)=3+2-2=3$, $\dot h_2(0)=-1-1+1=-1$.
> - D: Both slips of A and C at once. The result equals the values $h_j(0)$, and it would give $\frac{d}{dt}e^{At}=I$ at $t=0$, not $A$.

### Q11 (slide 77, Remark)

$C$ is upper triangular with the rows $(1,\ 1,\ 0)$, $(0,\ 1,\ 0)$, $(0,\ 0,\ 2)$. It has $\Delta=(\lambda-1)^2(\lambda-2)$, as the matrix $A$ of Q10, so $e^{Ct}=h_0I+h_1C+h_2C^2$ with the same $h_0,h_1,h_2$ as in Q10: $h_0=-2te^t+e^{2t}$, $h_1=3te^t+2e^t-2e^{2t}$, $h_2=-te^t-e^t+e^{2t}$. Does $e^{Ct}$ contain a $te^t$ term, and what is $\Psi$ of $C$?

- A) No, entry $(1,2)$ of $e^{Ct}$ is $0$. $\Psi=(\lambda-1)(\lambda-2)$.
- B) Yes, entry $(1,2)$ of $e^{Ct}$ is $te^t$. $\Psi=(\lambda-1)(\lambda-2)$.
- C) No, entry $(1,2)$ of $e^{Ct}$ is $e^t$. $\Psi=(\lambda-1)^2(\lambda-2)$.
- D) Yes, entry $(1,2)$ of $e^{Ct}$ is $te^t$. $\Psi=(\lambda-1)^2(\lambda-2)$.

> [!success]- Answer
> **D.** $C^2=\begin{bmatrix}1&2&0\\0&1&0\\0&0&4\end{bmatrix}$, so entry $(1,2)$ of $h_0I+h_1C+h_2C^2$ is $h_1+2h_2=3te^t+2e^t-2e^{2t}-2te^t-2e^t+2e^{2t}=te^t$.
> In full, $e^{Ct}=\begin{bmatrix}e^t&te^t&0\\0&e^t&0\\0&0&e^{2t}\end{bmatrix}$.
> $(C-I)(C-2I)$ has the entry $-1$ at $(1,2)$, so it is not zero. So $\Psi=(\lambda-1)^2(\lambda-2)=\Delta$: $C$ has a Jordan block of size 2 for $\lambda=1$.
> - A: The same $\Delta$ gives the same $h$, not the same $f(C)$. The matrix that goes into $h$ is different, and $C$ is not diagonalizable.
> - B: $e^{Ct}$ is right, but $(\lambda-1)(\lambda-2)$ is not zero at $C$: $(C-I)(C-2I)\neq0$.
> - C: This applies $e^{(\cdot)t}$ to every entry of $C$: $e^{1\cdot t}=e^t$. $e^{Ct}$ is a matrix function, not an entrywise exponential.

### Q12 (slide 77, Example 3)

$J$ is the $3\times3$ Jordan block of $\lambda_1=2$ (2 on the diagonal, 1 on the superdiagonal). For $f(J)$ the formula puts $f^{(j)}(\lambda_1)/j!$ on the $j$-th superdiagonal. What is the first row of $J^5$, and what is entry $(1,3)$ of $e^{Jt}$?

- A) First row of $J^5$: $(32,\ 80,\ 160)$. Entry $(1,3)$ of $e^{Jt}$: $t^2e^{2t}$.
- B) First row of $J^5$: $(32,\ 80,\ 80)$. Entry $(1,3)$ of $e^{Jt}$: $t^2e^{2t}$.
- C) First row of $J^5$: $(32,\ 80,\ 80)$. Entry $(1,3)$ of $e^{Jt}$: $\tfrac12t^2e^{2t}$.
- D) First row of $J^5$: $(32,\ 80,\ 160)$. Entry $(1,3)$ of $e^{Jt}$: $\tfrac12t^2e^{2t}$.

> [!success]- Answer
> **C.** $J^5$: $f=\lambda^5$, $f'=5\lambda^4$, $f''=20\lambda^3$. At 2: $f=32$, $f'=80$, $\frac12f''=\frac12\cdot160=80$. First row $(32,80,80)$.
> $e^{Jt}$: $f=e^{\lambda t}$, $f''=t^2e^{\lambda t}$ (derivatives with respect to $\lambda$). Entry $(1,3)$ is $\frac12f''(2)=\frac12t^2e^{2t}$.
> - A: The factor $1/2!$ was dropped in both: $f''(2)=160$ and $t^2e^{2t}$ were put on the second superdiagonal.
> - B: $J^5$ is right, but the $1/2!$ was dropped in $e^{Jt}$.
> - D: $e^{Jt}$ is right, but the $1/2!$ was dropped in $J^5$: entry $(1,3)$ is $f''(2)/2=80$, not $160$.
