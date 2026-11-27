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

> [!question]- Check (slide 69): $A$ has the rows $(4,\ 1)$ and $(2,\ 3)$. The columns of $Q$ are its eigenvectors $(1,-2)$ and $(1,1)$, so $Q^{-1}AQ=\operatorname{diag}(2,5)$. Use the similarity rule to compute $A^3$ without multiplying $A$ by itself.
> The rule says $\hat A^3=Q^{-1}A^3Q$. Solve for $A^3$: $A^3=Q\hat A^3Q^{-1}$.
> A diagonal matrix is block-diagonal with $1\times1$ blocks, so $\hat A^3=\operatorname{diag}(2^3,5^3)=\operatorname{diag}(8,125)$.
> $$Q=\begin{bmatrix}1&1\\-2&1\end{bmatrix},\qquad \det Q=1\cdot1-1\cdot(-2)=3,\qquad Q^{-1}=\frac13\begin{bmatrix}1&-1\\2&1\end{bmatrix}$$
> $$Q\hat A^3=\begin{bmatrix}8&125\\-16&125\end{bmatrix},\qquad A^3=\frac13\begin{bmatrix}8+250&-8+125\\-16+250&16+125\end{bmatrix}=\frac13\begin{bmatrix}258&117\\234&141\end{bmatrix}=\begin{bmatrix}86&39\\78&47\end{bmatrix}$$
> This is $f(A)=Qf(\Lambda)Q^{-1}$ with $f(\lambda)=\lambda^3$. It works for every polynomial $f$ when $A$ is diagonalizable.

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

> [!question]- Check (slide 70): $A$ has the rows $(1,\ 2)$ and $(3,\ 4)$. Verify the Cayley-Hamilton theorem for this $A$. Then write $A^3$ as $\alpha A+\beta I$ and give the matrix.
> $\Delta(\lambda)=(\lambda-1)(\lambda-4)-2\cdot3=\lambda^2-5\lambda-2$.
> $$A^2=\begin{bmatrix}1+6&2+8\\3+12&6+16\end{bmatrix}=\begin{bmatrix}7&10\\15&22\end{bmatrix}$$
> $$\Delta(A)=A^2-5A-2I=\begin{bmatrix}7-5-2&10-10\\15-15&22-20-2\end{bmatrix}=\begin{bmatrix}0&0\\0&0\end{bmatrix}$$
> So $A^2=5A+2I$. Multiply by $A$ and use this again:
> $A^3=5A^2+2A=5(5A+2I)+2A=27A+10I$.
> $$A^3=\begin{bmatrix}27+10&54\\81&108+10\end{bmatrix}=\begin{bmatrix}37&54\\81&118\end{bmatrix}$$
> The same step repeated gives every higher power as a combination of $A$ and $I$ (here $n=2$).

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

> [!question]- Check (slide 71): In the slide's $4\times4$ matrix, replace the 1 at position $(2,3)$ by 0. What are the Jordan blocks now, and what is $\Psi(\lambda)$? Is $\Delta(\lambda)$ different?
> The diagonal does not change, so $\Delta(\lambda)=(\lambda-\lambda_0)^4$ stays the same.
> Only the 1 at $(1,2)$ is left. It ties rows 1 and 2 into one block of size 2. Rows 3 and 4 are blocks of size 1. Block sizes: 2, 1, 1.
> $N=A-\lambda_0I$ has a single 1 at $(1,2)$. $N\neq0$, so $(\lambda-\lambda_0)$ is not enough.
> $N^2$: entry $(i,j)$ is $\sum_k N_{ik}N_{kj}$. The only nonzero factor is $N_{12}$, and it needs $N_{2j}\neq0$, but row 2 of $N$ is zero. So $N^2=0$.
> $\Psi(\lambda)=(\lambda-\lambda_0)^2$. The exponent is the size of the largest block.

> [!question]- Check (slide 72): The proof says that $r(A)=0$ with $r\not\equiv0$ "would contradict" the least degree. But $r$ may not be monic, and the definition speaks about monic polynomials. Why is it still a contradiction?
> Let $c\neq0$ be the leading coefficient of $r$. Then $\tilde r(\lambda)=r(\lambda)/c$ is monic.
> $\tilde r(A)=\frac1c r(A)=0$, and $\deg\tilde r=\deg r<\deg\Psi$.
> So $\tilde r$ is a monic polynomial of lower degree than $\Psi$ that gives zero at $A$. This is impossible, because $\Psi$ has the least degree. So $r\equiv0$.

> [!question]- Check (slide 73): A Jordan form $J_A$ has the eigenvalue $2$ with blocks of sizes 3 and 1, and the eigenvalue $-1$ with blocks of sizes 2 and 2. Give $n$, $\Delta(\lambda)$ and $\Psi(\lambda)$. Which factor of $\Psi$ is forced by which block?
> $n$ is the sum of all block sizes: $3+1+2+2=8$.
> The multiplicity $n_i$ is the sum of the block sizes of $\lambda_i$: $n_1=4$, $n_2=4$. So $\Delta(\lambda)=(\lambda-2)^4(\lambda+1)^4$.
> The index $m_i$ is the largest block size: $m_1=3$, $m_2=2$. So $\Psi(\lambda)=(\lambda-2)^3(\lambda+1)^2$, of degree 5.
> $(\lambda-2)^3$ is forced by the size-3 block: for it $(J-2I)^2\neq0$ and $(J-2I)^3=0$. $(\lambda+1)^2$ is forced by a size-2 block of $-1$. The smaller blocks are then zero automatically.

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

> [!info] Why the Fact holds, and why $h$ exists (beyond the slides)
> - **Fact.** $m_i$ is the size of the largest Jordan block of $\lambda_i$. All $m_i=1$ means every Jordan block has size 1. Then $J_A$ is a diagonal matrix, and $J_A=Q^{-1}AQ$ says that $A$ is diagonalizable. The other direction: if $A$ is diagonalizable, its Jordan form is diagonal, so all blocks have size 1.
> - **Counting.** $h(\lambda)=h_0+h_1\lambda+\cdots+h_{n-1}\lambda^{n-1}$ has $n$ unknown coefficients. Eigenvalue $\lambda_i$ gives $n_i$ conditions ($l=0,\dots,n_i-1$). In total $n_1+\cdots+n_k=n$ conditions. The equations are linear in the $h_j$ and always have exactly one solution, so $h$ is unique.
> - **Distinct eigenvalues.** Then all $n_i=1$ and no derivative is needed: only $h(\lambda_i)=f(\lambda_i)$ for $i=1,\dots,n$.
> - **Spectrum.** The set of eigenvalues of $A$ is called the spectrum of $A$. "$h$ equals $f$ on the spectrum of $A$" (Chen) means the conditions of Definition 1.

> [!question]- Check (slide 74, indices): $A$ is $3\times3$ with 2 on the diagonal and 1 everywhere else. Its characteristic polynomial is $(\lambda-1)^2(\lambda-4)$. Find $\Psi$, the indices, and say whether $A$ is diagonalizable.
> $\Psi$ divides $\Delta$ and has every eigenvalue as a root ($m_i\ge1$). Two candidates: $(\lambda-1)(\lambda-4)$ and $(\lambda-1)^2(\lambda-4)$. Test the smaller one.
> $$A-I=\begin{bmatrix}1&1&1\\1&1&1\\1&1&1\end{bmatrix},\qquad A-4I=\begin{bmatrix}-2&1&1\\1&-2&1\\1&1&-2\end{bmatrix}$$
> Every column of $A-4I$ sums to $-2+1+1=0$. Every row of $A-I$ is $(1,1,1)$, so every entry of the product is a column sum of $A-4I$: $(A-I)(A-4I)=0$.
> So $\Psi(\lambda)=(\lambda-1)(\lambda-4)$. The indices are $m_1=1$, $m_2=1$, and $A$ is diagonalizable. The eigenvalue 1 is repeated ($n_1=2$), but its index is 1.

> [!question]- Check (slide 74, interpolating polynomial): $A$ has the rows $(0,\ 1)$ and $(-2,\ -3)$. Set up and solve the conditions of Definition 1 for $f(\lambda)=e^{\lambda t}$, then give $e^{At}$.
> $\Delta(\lambda)=\lambda(\lambda+3)+2=\lambda^2+3\lambda+2=(\lambda+1)(\lambda+2)$. Eigenvalues $-1$ and $-2$, both with $n_i=1$. So only $l=0$: two value conditions, no derivative.
> $h(\lambda)=h_0+h_1\lambda$:
> $$h_0-h_1=e^{-t},\qquad h_0-2h_1=e^{-2t}$$
> Subtract the second from the first: $h_1=e^{-t}-e^{-2t}$. Then $h_0=e^{-t}+h_1=2e^{-t}-e^{-2t}$.
> $$e^{At}=h_0I+h_1A=\begin{bmatrix}h_0&h_1\\-2h_1&h_0-3h_1\end{bmatrix}=\begin{bmatrix}2e^{-t}-e^{-2t}&e^{-t}-e^{-2t}\\-2e^{-t}+2e^{-2t}&-e^{-t}+2e^{-2t}\end{bmatrix}$$
> Test: at $t=0$ the result is $I$.

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

> [!info] Proof of "$h$ is the remainder" (beyond the slides)
> Slide 75 says "(Prove this!)". Let $f$ be a polynomial and $f(\lambda)=\Delta(\lambda)q(\lambda)+r(\lambda)$ with $\deg r\le n-1$.
> 1. $\lambda_i$ is a root of $\Delta$ of multiplicity $n_i$, so $\Delta(\lambda)=(\lambda-\lambda_i)^{n_i}g(\lambda)$. Every derivative of $\Delta$ up to order $n_i-1$ still has a factor $(\lambda-\lambda_i)$, so $\Delta^{(j)}(\lambda_i)=0$ for $j=0,\dots,n_i-1$.
> 2. Differentiate $f=\Delta q+r$ $l$ times with the product rule. Every term that comes from $\Delta q$ contains some $\Delta^{(j)}$ with $j\le l$. For $l\le n_i-1$ all these terms are zero at $\lambda_i$. So $f^{(l)}(\lambda_i)=r^{(l)}(\lambda_i)$.
> 3. So $r$ has degree at most $n-1$ and meets all conditions of Definition 1. The interpolating polynomial is unique, so $h=r$.
> 
> This also shows that Definition 2 agrees with the direct definition of slide 69 when $f$ is a polynomial: $f(A)=\Delta(A)q(A)+r(A)=r(A)=h(A)$, because $\Delta(A)=0$ (Cayley-Hamilton).

> [!question]- Check (slide 75, remainder): $A$ has the rows $(0,\ 1)$ and $(-2,\ 3)$, so $\Delta(\lambda)=\lambda^2-3\lambda+2$. Find $h$ for $f(\lambda)=\lambda^3$ by Euclidean division. Then confirm it with the conditions of Definition 1, and give $A^3$.
> Division: $\lambda^3=(\lambda^2-3\lambda+2)\lambda+(3\lambda^2-2\lambda)$, and $3\lambda^2-2\lambda=3(\lambda^2-3\lambda+2)+(7\lambda-6)$.
> So $\lambda^3=\Delta(\lambda)(\lambda+3)+7\lambda-6$: $q=\lambda+3$, $r=7\lambda-6$, $h(\lambda)=7\lambda-6$.
> Definition 1: $\Delta=(\lambda-1)(\lambda-2)$, distinct eigenvalues 1 and 2. $h(1)=7-6=1=1^3$ and $h(2)=14-6=8=2^3$. Both conditions hold.
> $$A^3=7A-6I=\begin{bmatrix}-6&7\\-14&21-6\end{bmatrix}=\begin{bmatrix}-6&7\\-14&15\end{bmatrix}$$

> [!question]- Check (slide 75, Example 1): $A$ has the rows $(3,\ 1)$ and $(-1,\ 1)$. Compute $A^{10}$ with the method of Example 1.
> $\Delta(\lambda)=(\lambda-3)(\lambda-1)+1=\lambda^2-4\lambda+4=(\lambda-2)^2$. One eigenvalue $2$ with $n_1=2$, so one value condition and one derivative condition.
> $f(\lambda)=\lambda^{10}$, $f'(\lambda)=10\lambda^9$, $h(\lambda)=h_0+h_1\lambda$, $h'(\lambda)=h_1$.
> - $h(2)=f(2)$: $h_0+2h_1=2^{10}=1024$.
> - $h'(2)=f'(2)$: $h_1=10\cdot2^9=5120$.
> 
> $h_0=1024-2\cdot5120=-9216$.
> $$A^{10}=-9216\,I+5120\,A=\begin{bmatrix}-9216+15360&5120\\-5120&-9216+5120\end{bmatrix}=\begin{bmatrix}6144&5120\\-5120&-4096\end{bmatrix}$$
> Without the derivative condition there would be one equation for two unknowns.

> [!question]- Check (slide 76): Put $t=0$ into the slide's solution $h_0,h_1,h_2$. What do you get, and why must it be so? Then do the same for the derivatives $dh_j/dt$ at $t=0$.
> At $t=0$: $h_0=-0+1=1$, $h_1=0+2-2=0$, $h_2=-0-1+1=0$.
> So $e^{A\cdot0}=1\cdot I+0\cdot A+0\cdot A^2=I$. It must be so: for $t=0$, $f(\lambda)=e^{0}=1$ is the constant polynomial 1, and $f(A)=I$.
> Derivatives: $\dot h_0=-2e^t-2te^t+2e^{2t}$, $\dot h_1=3e^t+3te^t+2e^t-4e^{2t}$, $\dot h_2=-e^t-te^t-e^t+2e^{2t}$.
> At $t=0$: $\dot h_0=-2+2=0$, $\dot h_1=3+2-4=1$, $\dot h_2=-1-1+2=0$.
> So $\frac{d}{dt}e^{At}\big\rvert_{t=0}=0\cdot I+1\cdot A+0\cdot A^2=A$. This agrees with $\frac{d}{dt}e^{At}=Ae^{At}$, which gives $A$ at $t=0$. Both tests are a fast way to catch a wrong coefficient.

> [!question]- Check (slide 77, Remark): $C$ is upper triangular with the rows $(1,\ 1,\ 0)$, $(0,\ 1,\ 0)$, $(0,\ 0,\ 2)$. It has the same $\Delta$ as the slide's $A$ and $B$. Compute $e^{Ct}$ with the slide's $h_0,h_1,h_2$. Does a $te^t$ term survive? What is $\Psi$ of $C$?
> Same $\Delta=(\lambda-1)^2(\lambda-2)$, so the same $h$. Only the matrix that goes into $h$ changes.
> $$C^2=\begin{bmatrix}1&2&0\\0&1&0\\0&0&4\end{bmatrix},\qquad e^{Ct}=h_0I+h_1C+h_2C^2=\begin{bmatrix}h_0+h_1+h_2&h_1+2h_2&0\\0&h_0+h_1+h_2&0\\0&0&h_0+2h_1+4h_2\end{bmatrix}$$
> The three entries are the left sides of the slide's three equations: $h_0+h_1+h_2=e^t$, $h_1+2h_2=te^t$, $h_0+2h_1+4h_2=e^{2t}$.
> $$e^{Ct}=\begin{bmatrix}e^t&te^t&0\\0&e^t&0\\0&0&e^{2t}\end{bmatrix}$$
> Yes, $te^t$ survives at position $(1,2)$. $C$ has a Jordan block of size 2 for $\lambda=1$: $(C-I)(C-2I)$ has the entry $-1$ at $(1,2)$, so it is not zero, and $\Psi=(\lambda-1)^2(\lambda-2)=\Delta$. $C$ is not diagonalizable.

> [!question]- Check (slide 77, Example 3): $J$ is the size-3 Jordan block of $\lambda_1=2$. Use the formula of Example 3 to write $J^5$ and $e^{Jt}$.
> $J^5$: $f(\lambda)=\lambda^5$, $f'=5\lambda^4$, $f''=20\lambda^3$. At $\lambda_1=2$: $f=32$, $f'=5\cdot16=80$, $\frac12f''=\frac12\cdot20\cdot8=80$.
> $$J^5=\begin{bmatrix}32&80&80\\0&32&80\\0&0&32\end{bmatrix}$$
> $e^{Jt}$: $f(\lambda)=e^{\lambda t}$, $f'=te^{\lambda t}$, $f''=t^2e^{\lambda t}$ (derivatives with respect to $\lambda$). At $\lambda_1=2$: $e^{2t}$, $te^{2t}$, $\frac12t^2e^{2t}$.
> $$e^{Jt}=e^{2t}\begin{bmatrix}1&t&\frac12t^2\\0&1&t\\0&0&1\end{bmatrix}$$
> A block of size $s$ gives powers of $t$ up to $t^{s-1}$ in $e^{Jt}$.

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
> [!question]- 1. For $A$ with the rows $(1,\ 1)$ and $(0,\ 2)$ and $f(\lambda)=\lambda^2+1$, compute $f(A)$.
> $A^2=\begin{bmatrix}1&3\\0&4\end{bmatrix}$, $f(A)=A^2+I=\begin{bmatrix}2&3\\0&5\end{bmatrix}$. Diagonal check: $f(1)=2$, $f(2)=5$.

> [!question]- 2. A matrix has $\Delta(\lambda)=\lambda^2+1$. What is $A^4$?
> $\lambda^4=(\lambda^2+1)(\lambda^2-1)+1$, and $\Delta(A)=0$, so $A^4=I$.

> [!question]- 3. Find $\Psi$ for $\operatorname{diag}(2,2,5)$ and for $M$ with the rows $(2,\ 1,\ 0)$, $(0,\ 2,\ 0)$, $(0,\ 0,\ 5)$. Which is diagonalizable?
> Both have $\Delta=(\lambda-2)^2(\lambda-5)$. For the diagonal matrix $(D-2I)(D-5I)=0$, so $\Psi=(\lambda-2)(\lambda-5)$: diagonalizable. For $M$, $(M-2I)(M-5I)\neq0$, so $\Psi=(\lambda-2)^2(\lambda-5)$: index 2, not diagonalizable.

> [!question]- 4. A $5\times5$ matrix has the single eigenvalue 0 with Jordan blocks of sizes 2, 2, 1. $\Delta$ and $\Psi$?
> $\Delta=\lambda^5$. Largest block has size 2, so $\Psi=\lambda^2$.

> [!question]- 5. Compute $e^{At}$ for $A$ with the rows $(1,\ 1)$ and $(0,\ 1)$ with the interpolating polynomial.
> $\Delta=(\lambda-1)^2$, $h=h_0+h_1\lambda$. $h_0+h_1=e^t$, $h_1=te^t$. $e^{At}=h_0I+h_1A=e^t\begin{bmatrix}1&t\\0&1\end{bmatrix}$.

> [!question]- 6. Redo slide Example 2 with $\Psi=(\lambda-1)(\lambda-2)$: $h=h_0+h_1\lambda$. Same $e^{At}$?
> $h_0+h_1=e^t$, $h_0+2h_1=e^{2t}$: $h_1=e^{2t}-e^t$, $h_0=2e^t-e^{2t}$. $h_0I+h_1A$ gives the same matrix, for example entry $(3,3)$: $h_0+3h_1=-e^t+2e^{2t}$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L04 - Equations, eigenvalues, diagonalization]]. Next: [[EE502 L06 - Matrix exponential]]. Jordan blocks: [[EE502 L07 - Jordan form]]
- Used by the midterm. The Quiz 2 revision pack for slides 36-79 (rank, eigen, $f(A)$, Cayley-Hamilton) is kept for Quiz 3 and the midterm.
- Full step-by-step notes (PDF): [EE502_Lecture_05_Matrix_Functions.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_05/EE502_Lecture_05_Matrix_Functions.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_05/EE502_Lecture_05_Matrix_Functions.pdf`
- Original slides (PDF, pp. 68-77): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`
- Quiz: [[EE502 L05 - Functions of a matrix - quiz]]

Slides not embedded: 68 (section title).
