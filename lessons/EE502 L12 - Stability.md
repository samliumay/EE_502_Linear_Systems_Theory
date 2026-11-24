---
course: EE 502 Linear System Theory
lecture: 12
title: Stability
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 114-129)
full_notes: lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf
---
# EE 502 · Lecture 12 · Stability: BIBO and internal

> [!summary] In short
> - BIBO stability (input to output): every bounded input gives a bounded output. For LTI: $\int_0^\infty\lvert g\rvert<\infty$, or all poles of $\hat g(s)$ strictly in the left half-plane.
> - Internal stability (the state): all eigenvalues of $A$ have negative real part. Marginal stability allows eigenvalues on the imaginary axis with index 1.
> - Poles are a subset of the eigenvalues. So BIBO-stable does not imply internally stable.
> - Tests without root-finding: the Lyapunov equation $A^{\mathsf T}M+MA=-N$ and the Routh table.
> - LTV: decide from $\Phi(t,t_0)$, never from the frozen eigenvalues of $A(t)$.

Slide numbers below are pages of the 220-page ABO file.

## 1. BIBO stability, single input and output (slides 115-117)
![[ee502_eee501alllecturenotesabo_p115.jpg]]
![[ee502_eee501alllecturenotesabo_p116.jpg]]
![[ee502_eee501alllecturenotesabo_p117.jpg]]

**Notes.** A relaxed LTI system has impulse response $g(t)$ and transfer function $\hat g(s)$:
$$y(t)=\int_0^t g(t-\tau)u(\tau)\,d\tau,\qquad \hat g(s)=\int_0^\infty g(t)e^{-st}\,dt .$$
It is **BIBO-stable** if $\lvert u(t)\rvert\le M$ for all $t$ implies $\lvert y(t)\rvert\le N$ for all $t$, for some $N$.

**Fact 1.** Equivalent:
1. the system is BIBO-stable;
2. $g$ is absolutely integrable: $\int_0^t\lvert g(\tau)\rvert\,d\tau\le K$ for all $t$;
3. all poles of $\hat g(s)$ are in the open left half-plane (for rational $\hat g$).

Proof ideas: (2) $\Rightarrow$ (1): $\lvert y(t)\rvert\le M\int_0^t\lvert g\rvert\le MK$. (1) $\Rightarrow$ (2): the input $u(t_1-\tau)=\operatorname{sign}g(\tau)$ gives $y(t_1)=\int_0^{t_1}\lvert g\rvert$. (3) $\Rightarrow$ (2): partial fractions give terms $t^ke^{\alpha t}$ with $\alpha<0$, each absolutely integrable.

Recipe: cancel common factors, find the poles, all with $\operatorname{Re}<0$ means BIBO-stable. A pole on the imaginary axis already fails. Zeros do not matter.

> [!warning] Slide error (p. 117 example)
> For $\hat g(s)=\dfrac{s+3}{(s+2)(s+1)^3}$ the slide's expansion is wrong. Correct:
> $$\hat g(s)=\frac{2}{(s+1)^3}-\frac{1}{(s+1)^2}+\frac{1}{s+1}-\frac{1}{s+2},\qquad g(t)=(t^2-t+1)e^{-t}-e^{-2t}.$$
> In the triangle-inequality bound every term enters with a plus sign: $\int_0^\infty\lvert g\rvert\le 2+1+1+\tfrac12=\tfrac92$, not $\tfrac{11}{2}$. The exact area is $\tfrac32$. The conclusion (BIBO-stable, poles $-1,-2$) is unaffected.

> [!warning] Watch out
> $g(t)\to 0$ is not enough: $1/(1+t)\to 0$ but $\int_0^T\tfrac{dt}{1+t}=\ln(1+T)\to\infty$.

## 2. BIBO stability, multivariable case (slide 118)
![[ee502_eee501alllecturenotesabo_p118.jpg]]

**Notes.** Same definition with vector norms $\lVert\mathbf{u}(t)\rVert$, $\lVert\mathbf{y}(t)\rVert$.

**Fact 2.** A MIMO system is BIBO-stable iff every entry $g_{ij}(t)$ of $G(t)$ is absolutely integrable iff every entry of $\hat G(s)$ has all its poles in the open left half-plane. One bad channel is enough to fail.

> [!example] Slide example
> $G(t)=\begin{bmatrix}1+e^{-2t}&e^{-t}\end{bmatrix}$ is not BIBO-stable: $\int_0^\infty\lvert 1+e^{-2t}\rvert\,dt=\infty$. In the $s$-domain, $\hat G(s)=\begin{bmatrix}\dfrac{2s+2}{s(s+2)}&\dfrac{1}{s+1}\end{bmatrix}$ has a pole at $s=0$.

## 3. Internal stability: poles and eigenvalues (slides 119-120)
![[ee502_eee501alllecturenotesabo_p119.jpg]]
![[ee502_eee501alllecturenotesabo_p120.jpg]]

**Notes.** For $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$:
$$\hat G(s)=\frac{C\operatorname{adj}(sI-A)B+D\det(sI-A)}{\det(sI-A)},\qquad\{\text{poles of }\hat G\}\subseteq\{\text{eigenvalues of }A\}.$$
Cancellations can remove eigenvalues from $\hat G$.

> [!example] Slide example
> $\dot x=x+u$, $y=0.5u$: eigenvalue $1$, no poles ($\hat g=0.5$). BIBO-stable, but $x(t)$ grows without bound.

**Definition.** With zero input, $\mathbf{x}(t)=e^{At}\mathbf{x}_0$.
- **Stable in the sense of Lyapunov (marginally stable):** $\mathbf{x}(t)$ is bounded for every $\mathbf{x}_0$.
- **Internally (asymptotically) stable:** $\mathbf{x}(t)\to\mathbf{0}$ for every $\mathbf{x}_0$.

**Fact.**
- Marginally stable iff all eigenvalues have $\operatorname{Re}\lambda\le 0$ and each eigenvalue with $\operatorname{Re}\lambda=0$ has index 1 (simple root of the minimal polynomial, largest Jordan block $1\times 1$).
- Asymptotically stable iff all eigenvalues have $\operatorname{Re}\lambda<0$.

Reason: the entries of $e^{At}$ are combinations of $t^{j}e^{\lambda_it}$, $j<m_i$ (see [[EE502 L09 - LTI state equation solution]]).

For a repeated eigenvalue on the axis, compare the number of independent eigenvectors $n-\operatorname{rank}(A-\lambda I)$ with the multiplicity. Equal means index 1.

> [!warning] Watch out
> - BIBO-stable does not imply internally stable (hidden eigenvalues). Asymptotically stable does imply BIBO-stable.
> - Marginally stable does not imply BIBO-stable (the integrator $1/s$).
> - The slide says "for every nonzero initial state and for every input" $x\to\infty$. Read it as the generic case.

## 4. Lyapunov theorem (slides 121-123)
![[ee502_eee501alllecturenotesabo_p121.jpg]]
![[ee502_eee501alllecturenotesabo_p122.jpg]]
![[ee502_eee501alllecturenotesabo_p123.jpg]]

**Notes.** **Theorem.** $\dot{\mathbf{x}}=A\mathbf{x}$ is asymptotically stable iff for any symmetric $N>0$ there is a unique $M>0$ with
$$A^{\mathsf T}M+MA=-N .$$
- Only if: $M=\int_0^\infty e^{A^{\mathsf T}t}Ne^{At}\,dt$ is positive definite and satisfies the equation, because $\tfrac{d}{dt}\bigl[e^{A^{\mathsf T}t}Ne^{At}\bigr]$ integrates to $-N$.
- If: for an eigenpair $A\mathbf{v}=\lambda\mathbf{v}$, $-\mathbf{v}^*N\mathbf{v}=2\operatorname{Re}\{\lambda\}\,\mathbf{v}^*M\mathbf{v}$, so $\operatorname{Re}\lambda<0$.
- Lemma (uniqueness): $AM+MB=C$ has a unique solution for every $C$ iff $\lambda_i+\mu_j\ne 0$ for all eigenvalues $\lambda_i$ of $A$, $\mu_j$ of $B$.

One $N$ is enough (Remark 2): solve $A^{\mathsf T}M+MA=-I$ and check $M>0$. A matrix with all eigenvalues in the open left half-plane is called **Hurwitz**.

> [!example] $A=\begin{bmatrix}0&1\\-2&-3\end{bmatrix}$, $N=I$
> Unknown $M=\begin{bmatrix}m_1&m_2\\m_2&m_3\end{bmatrix}$. The three equations give $M=\begin{bmatrix}5/4&1/4\\1/4&1/4\end{bmatrix}$. Minors: $\tfrac54>0$, $\det M=\tfrac14>0$. So $M>0$ and $A$ is Hurwitz (eigenvalues $-1,-2$).
> For $A=\begin{bmatrix}0&1\\-2&1\end{bmatrix}$ the unique solution is $M=\begin{bmatrix}-7/4&1/4\\1/4&-3/4\end{bmatrix}$, not positive definite: not Hurwitz.

> [!warning] Slide misprint (Remark 1)
> The third term of $\mathbf{v}^*M\mathbf{v}$ is printed as $-j\mathbf{v}_r^{\mathsf T}M\mathbf{v}_r$. Correct: $\mathbf{v}^*M\mathbf{v}=\mathbf{v}_r^{\mathsf T}M\mathbf{v}_r+j\mathbf{v}_r^{\mathsf T}M\mathbf{v}_i-j\mathbf{v}_i^{\mathsf T}M\mathbf{v}_r+\mathbf{v}_i^{\mathsf T}M\mathbf{v}_i$, and the two imaginary terms cancel.

## 5. Routh-Hurwitz criterion (slide 124)
![[ee502_eee501alllecturenotesabo_p124.jpg]]

**Notes.** For $\Delta(s)=a_0s^n+a_1s^{n-1}+\dots+a_n$, $a_0>0$: first row $a_0,a_2,a_4,\dots$, second row $a_1,a_3,a_5,\dots$. Each new row comes from the two rows above:
$$b_1=\frac{a_1a_2-a_0a_3}{a_1},\quad b_2=\frac{a_1a_4-a_0a_5}{a_1},\quad c_1=\frac{b_1a_3-a_1b_2}{b_1},\ \dots$$
If the first column has no zero, the number of right half-plane roots equals the number of sign changes in the first column.

> [!example] Slide example: $\Delta(s)=s^4+3s^3+5s^2+11s+8$
> | | | | |
> |---|---|---|---|
> | $s^4$ | $1$ | $5$ | $8$ |
> | $s^3$ | $3$ | $11$ | |
> | $s^2$ | $4/3$ | $8$ | |
> | $s^1$ | $-7$ | | |
> | $s^0$ | $8$ | | |
>
> First column $1,3,\tfrac43,-7,8$: two sign changes, two right half-plane eigenvalues ($0.1241\pm j1.8822$). The others are $-2.2483$ and $-1$.

Quick facts: all roots stable implies all coefficients positive. For $n=2$ that is also sufficient. For $n=3$: stable iff $a_1,a_2,a_3>0$ and $a_1a_2>a_3$ (monic). Example from our notes: $s(s+1)(s+2)+K$ is stable iff $0<K<6$.

> [!warning] Watch out
> Positive coefficients do not prove stability for $n\ge 3$: the slide's polynomial has only positive coefficients and two unstable roots.

## 6. BIBO stability of LTV systems (slides 126-127)
![[ee502_eee501alllecturenotesabo_p126.jpg]]
![[ee502_eee501alllecturenotesabo_p127.jpg]]

**Notes.** A relaxed LTV system: $y(t)=\int_{t_0}^{t}g(t,\tau)u(\tau)\,d\tau$. It is BIBO-stable iff there is one $K$ with
$$\int_{t_0}^{t}\lvert g(t,\tau)\rvert\,d\tau\le K\quad\text{for all }t\ge t_0 .$$
Multivariable: $\int_{t_0}^{t}\lVert G(t,\tau)\rVert\,d\tau\le K$ with any matrix norm (induced 2-norm, or Frobenius $\lVert A\rVert_F^2=\operatorname{tr}(A^*A)$). All norms are equivalent, so this is the same as "every entry is absolutely integrable". There is no pole test for LTV systems.

## 7. Stability of LTV state representations (slides 128-129)
![[ee502_eee501alllecturenotesabo_p128.jpg]]
![[ee502_eee501alllecturenotesabo_p129.jpg]]

**Notes.** With $G(t,\tau)=C(t)\Phi(t,\tau)B(\tau)+D(t)\delta(t-\tau)$, BIBO-stable iff
$$\int_{t_0}^{t}\lVert C(t)\Phi(t,\tau)B(\tau)\rVert\,d\tau\le M_1,\qquad\lVert D(t)\rVert\le M_2\quad\text{for all }t\ge t_0 .$$
Zero-input response: $\mathbf{x}(t)=\Phi(t,t_0)\mathbf{x}_0$.
- Marginally stable iff $\lVert\Phi(t,t_0)\rVert\le\kappa$ for all $t_0$ and all $t\ge t_0$.
- Asymptotically stable iff, in addition, $\lVert\Phi(t,t_0)\rVert\to 0$ as $t\to\infty$.

Both kinds of stability are kept by Lyapunov transformations (slide exercise): $\hat\Phi(t,t_0)=P(t)\Phi(t,t_0)P(t_0)^{-1}$ with $P$, $P^{-1}$ bounded. See [[EE502 L11 - Equivalence and realization]].

> [!example] Two cautions (our notes)
> - $A(t)=\begin{bmatrix}-1&e^{2t}\\0&-1\end{bmatrix}$ has eigenvalues $-1,-1$ for every $t$, but $\Phi_{12}(t,0)=\sinh t$ is unbounded: unstable.
> - $\dot x=-\tfrac{1}{1+t}x+u$, $y=x$: $\Phi(t,\tau)=\tfrac{1+\tau}{1+t}\to 0$, asymptotically stable. But $\int_0^t\Phi(t,\tau)\,d\tau=\tfrac{t+t^2/2}{1+t}$ is unbounded: not BIBO-stable.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| BIBO (LTI) | $\int_0^\infty\lvert g\rvert<\infty$ $\iff$ poles of $\hat g$ in $\operatorname{Re}s<0$ |
| Poles and eigenvalues | $\{\text{poles}\}\subseteq\{\text{eigenvalues of }A\}$ |
| Asymptotic (LTI) | all $\operatorname{Re}\lambda<0$ (Hurwitz) |
| Marginal (LTI) | $\operatorname{Re}\lambda\le 0$, index 1 on the imaginary axis |
| Lyapunov equation | $A^{\mathsf T}M+MA=-N$, $N>0$; Hurwitz iff $M>0$ |
| Routh | sign changes in the first column = number of right half-plane roots |
| Cubic rule | $s^3+a_1s^2+a_2s+a_3$ stable iff all $a_i>0$ and $a_1a_2>a_3$ |
| BIBO (LTV) | $\int_{t_0}^{t}\lVert G(t,\tau)\rVert\,d\tau\le K$ for all $t$ |
| Internal (LTV) | $\lVert\Phi(t,t_0)\rVert$ bounded (marginal), and $\to 0$ (asymptotic) |
| Implications (LTI) | asymptotic $\Rightarrow$ BIBO; BIBO $\not\Rightarrow$ asymptotic; marginal $\not\Rightarrow$ BIBO |

## Check yourself
> [!question]- 1. Is $\hat g(s)=\dfrac{s-1}{(s+1)(s+2)}$ BIBO-stable? Find $g(t)$.
> Poles $-1,-2$: BIBO-stable (the zero at $+1$ does not matter). $g(t)=-2e^{-t}+3e^{-2t}$, and $\int_0^\infty\lvert g\rvert\le 2+\tfrac32=\tfrac72$.

> [!question]- 2. Is $\hat g(s)=\dfrac{1}{s^2+4}$ BIBO-stable? Give a bounded input with unbounded output.
> Poles $\pm 2j$ on the axis: not BIBO-stable. $u=\sin 2t$ gives $y(t)=\tfrac18(\sin 2t-2t\cos 2t)$, unbounded.

> [!question]- 3. $A=\operatorname{diag}(-1,2)$, $B=(1,0)^{\mathsf T}$, $C=\begin{bmatrix}1&1\end{bmatrix}$. BIBO-stable? Internally stable?
> $\hat g(s)=\tfrac{1}{s+1}$: BIBO-stable. Eigenvalue $2$: not internally stable. The input never reaches $x_2$, so $\hat g$ cannot see it.

> [!question]- 4. Classify $A=\begin{bmatrix}-1&1\\0&-1\end{bmatrix}$ and $A=\begin{bmatrix}0&0\\0&-2\end{bmatrix}$.
> First: double eigenvalue $-1$, asymptotically stable (the index matters only on the axis). Second: eigenvalues $0,-2$, the $0$ is simple: marginally stable.

> [!question]- 5. Solve $A^{\mathsf T}M+MA=-I$ for $A=\begin{bmatrix}0&1\\-1&-2\end{bmatrix}$. Hurwitz?
> Equations: $-2m_2=-1$, $m_1-2m_2-m_3=0$, $2m_2-4m_3=-1$. So $M=\begin{bmatrix}3/2&1/2\\1/2&1/2\end{bmatrix}$, minors $\tfrac32$ and $\tfrac12$, both positive: Hurwitz.

> [!question]- 6. For which $K$ are all roots of $s^3+2s^2+3s+K$ in the open left half-plane?
> First column $1,\ 2,\ \tfrac{6-K}{2},\ K$: all positive iff $0<K<6$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L11 - Equivalence and realization]]. Next: [[EE502 L13 - Controllability]]
- Needs: [[EE502 L08 - Positive definiteness and SVD]] (positive definite $M$), [[EE502 L10 - LTV state equation solution]] ($\Phi$)
- Full step-by-step notes (PDF): [EE502_Lecture_12_Stability.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_12/EE502_Lecture_12_Stability.pdf`
- Original slides (PDF, pp. 114-129): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Our notes also cover discrete-time stability (unit disk, $A^{\mathsf T}MA-M=-N$), which is not on these slides. See the PDF.

Slides not embedded: 114, 125 (section titles).
