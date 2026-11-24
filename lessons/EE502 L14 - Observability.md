---
course: EE 502 Linear System Theory
lecture: 14
title: Observability
tags: [ee502, lecture]
slides: lectures/EEE501AllLectureNotesABO.pdf (pp. 140-152, 160-162)
full_notes: lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf
---
# EE 502 · Lecture 14 · Observability, duality, Kalman decomposition

> [!summary] In short
> - $(C,A)$ is observable if the input and output on some $[0,t_1]$ fix the initial state $\mathbf{x}_0$ uniquely.
> - Tests: Gramian $W_o(t)$ nonsingular, $\operatorname{rank}[C;CA;\dots;CA^{n-1}]=n$, PBH with a right eigenvector.
> - Duality: $(A,B)$ controllable iff $(B^{\mathsf T},A^{\mathsf T})$ observable. Every controllability test transposes into an observability test.
> - A change of state keeps both properties. A good choice of $P$ displays the controllable and observable parts (Kalman decomposition). Only the controllable and observable part reaches the transfer matrix.
> - Minimal realization $\iff$ controllable and observable.

Slide numbers below are pages of the 220-page ABO file.

## 1. Definition and two examples (slides 141-142)
![[ee502_eee501alllecturenotesabo_p141.jpg]]
![[ee502_eee501alllecturenotesabo_p142.jpg]]

**Notes.** $\dot{\mathbf{x}}=A\mathbf{x}+B\mathbf{u}$, $\mathbf{y}=C\mathbf{x}+D\mathbf{u}$, or the pair $(C,A)$, is **observable** if for any unknown $\mathbf{x}_0=\mathbf{x}(0)$, knowing $\mathbf{u}(t)$ and $\mathbf{y}(t)$ on $[0,t_1]$ for some $t_1>0$ determines $\mathbf{x}_0$ uniquely.

> [!example] Example 1 (unobservable)
> $A=\begin{bmatrix}0&0\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&0\end{bmatrix}$, $D=1$: $y=x_1+u$. $x_2$ never influences $y$, so $x_2(0)$ cannot be found.

> [!example] Example 2 (observable)
> Same $A,B,D$ with $C=\begin{bmatrix}1&1\end{bmatrix}$. With $U(t)=\int_0^tu$, the readings at $0$ and $t_1$ give
> $$\begin{bmatrix}y(0)-u(0)\\ y(t_1)-U(t_1)-\int_0^{t_1}U-u(t_1)\end{bmatrix}=\begin{bmatrix}1&1\\t_1+1&1\end{bmatrix}\begin{bmatrix}x_{01}\\x_{02}\end{bmatrix}.$$
> The matrix has determinant $-t_1\ne 0$, so $\mathbf{x}_0$ is unique.

> [!warning] Watch out
> The slide writes $y(0)=x_{01}+x_{02}$. With $D=1$ it is $y(0)=x_{01}+x_{02}+u(0)$, so subtract $u(0)$ as above. Also: "not measured" does not mean "unobservable". Only the tests decide.

## 2. The observability Gramian (slides 143-144)
![[ee502_eee501alllecturenotesabo_p143.jpg]]
![[ee502_eee501alllecturenotesabo_p144.jpg]]

**Notes.** Move the known input terms to the left:
$$\hat{\mathbf{y}}(t):=\mathbf{y}(t)-\int_0^tCe^{A(t-\tau)}B\mathbf{u}(\tau)\,d\tau-D\mathbf{u}(t)=Ce^{At}\mathbf{x}_0 .$$
Only the zero-input response matters for observability.

**Theorem 2.** $(C,A)$ is observable iff $W_o(t_1)=\int_0^{t_1}e^{A^{\mathsf T}\tau}C^{\mathsf T}Ce^{A\tau}\,d\tau$ is nonsingular for some $t_1>0$.

- If: multiply $\hat{\mathbf{y}}(\tau)=Ce^{A\tau}\mathbf{x}_0$ on the left by $e^{A^{\mathsf T}\tau}C^{\mathsf T}$ and integrate. Then
$$\mathbf{x}_0=W_o(t_1)^{-1}\int_0^{t_1}e^{A^{\mathsf T}\tau}C^{\mathsf T}\hat{\mathbf{y}}(\tau)\,d\tau .$$
- Only if: if $W_o\mathbf{v}=\mathbf{0}$ with $\mathbf{v}\ne\mathbf{0}$, then $\int_0^{t_1}\lVert Ce^{A\tau}\mathbf{v}\rVert^2d\tau=0$, so $Ce^{A\tau}\mathbf{v}=\mathbf{0}$ for all $\tau$. The initial states $\mathbf{v}$ and $\mathbf{0}$ give the same output.

## 3. Duality and the main theorem (slides 145-146)
![[ee502_eee501alllecturenotesabo_p145.jpg]]
![[ee502_eee501alllecturenotesabo_p146.jpg]]

**Notes.** The **dual** of $(A,B,C,D)$ is $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T},D^{\mathsf T})$. Its controllability Gramian is the original $W_o$, and its observability Gramian is the original $W_c$. So $(A,B)$ is controllable iff $(B^{\mathsf T},A^{\mathsf T})$ is observable, and $(C,A)$ is observable iff $(A^{\mathsf T},C^{\mathsf T})$ is controllable.

**Corollary.** Equivalent:
1. $(C,A)$ is observable.
2. $W_o(t)$ is nonsingular for some $t>0$.
3. The observability matrix has rank $n$:
$$\mathcal{O}=\begin{bmatrix}C\\CA\\ \vdots\\CA^{n-1}\end{bmatrix}.$$
4. $\operatorname{rank}\begin{bmatrix}A-\lambda I\\C\end{bmatrix}=n$ for every eigenvalue $\lambda$ of $A$ (PBH).

> [!warning] Watch out
> $\mathcal{C}$ is a block row, $\mathcal{O}$ is a block column. For controllability the bad vector is a left eigenvector ($\mathbf{v}^{\mathsf T}B=\mathbf{0}^{\mathsf T}$). For observability it is a right eigenvector: $A\mathbf{w}=\lambda\mathbf{w}$ and $C\mathbf{w}=\mathbf{0}$.

## 4. Invariance, controllable and uncontrollable parts (slides 147-150)
![[ee502_eee501alllecturenotesabo_p147.jpg]]
![[ee502_eee501alllecturenotesabo_p148.jpg]]
![[ee502_eee501alllecturenotesabo_p149.jpg]]
![[ee502_eee501alllecturenotesabo_p150.jpg]]

**Notes.** Under $\hat{\mathbf{x}}=P\mathbf{x}$: $\hat{\mathcal{C}}=P\mathcal{C}$ and $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$. Ranks do not change, so controllability and observability are invariant under equivalence.

**Theorem 1.** Let $\operatorname{rank}\mathcal{C}=n_1<n$. Take $n_1$ independent columns $\mathbf{q}_1,\dots,\mathbf{q}_{n_1}$ of $\mathcal{C}$, complete them to a basis, and set $P^{-1}=[\mathbf{q}_1\ \cdots\ \mathbf{q}_n]$. Then
$$\hat A=\begin{bmatrix}\hat A_c&\hat A_{12}\\0&\hat A_{\bar c}\end{bmatrix},\quad\hat B=\begin{bmatrix}\hat B_c\\0\end{bmatrix},\quad\hat C=\begin{bmatrix}\hat C_c&\hat C_{\bar c}\end{bmatrix},$$
with $(\hat A_c,\hat B_c)$ controllable and $C(sI-A)^{-1}B+D=\hat C_c(sI-\hat A_c)^{-1}\hat B_c+D$. The eigenvalues of $\hat A_{\bar c}$ are the uncontrollable modes. They cancel out of the transfer matrix.

Recipe: column $j$ of $\hat A$ holds the coordinates of $A\mathbf{q}_j$ in the basis; $\hat B$ holds the coordinates of the columns of $B$; $\hat C=CP^{-1}$.

> [!example] Slide example (p. 150)
> $A=\begin{bmatrix}1&1&0\\0&1&0\\0&1&1\end{bmatrix}$, $B=\begin{bmatrix}0&1\\1&0\\0&1\end{bmatrix}$, $C=\begin{bmatrix}1&1&1\end{bmatrix}$. $\operatorname{rank}\mathcal{C}=2$. Take $\mathbf{q}_1,\mathbf{q}_2$ = columns of $B$, $\mathbf{q}_3=(1,0,0)^{\mathsf T}$:
> $$\hat A_c=\begin{bmatrix}1&0\\1&1\end{bmatrix},\ \hat B_c=I_2,\ \hat C_c=\begin{bmatrix}1&2\end{bmatrix},\ \hat A_{\bar c}=1,\ \hat C_{\bar c}=1 .$$
> $$\hat C_c(sI-\hat A_c)^{-1}\hat B_c=\begin{bmatrix}\dfrac{1}{s-1}+\dfrac{2}{(s-1)^2}&\dfrac{2}{s-1}\end{bmatrix}=C(sI-A)^{-1}B .$$

> [!warning] Slide slip (p. 149)
> The proof states that $\hat{\mathcal{C}}$ has rank $n$. Since $\hat{\mathcal{C}}=P\mathcal{C}$, the rank is $n_1$.

## 5. Observable parts and the Kalman decomposition (slides 151-152)
![[ee502_eee501alllecturenotesabo_p151.jpg]]
![[ee502_eee501alllecturenotesabo_p152.jpg]]

**Notes.** **Theorem 2.** Let $\operatorname{rank}\mathcal{O}=n_2<n$. Build $P$ from $n_2$ independent **rows** of $\mathcal{O}$, completed to a nonsingular matrix. Then
$$\hat A=\begin{bmatrix}\hat A_o&0\\\hat A_{21}&\hat A_{\bar o}\end{bmatrix},\quad\hat B=\begin{bmatrix}\hat B_o\\\hat B_{\bar o}\end{bmatrix},\quad\hat C=\begin{bmatrix}\hat C_o&0\end{bmatrix},$$
with $(\hat C_o,\hat A_o)$ observable and the same transfer matrix from $(\hat A_o,\hat B_o,\hat C_o,D)$.

**Theorem 3 (Kalman canonical decomposition).** Some $P$ gives
$$\hat A=\begin{bmatrix}\hat A_{co}&0&\hat A_{13}&0\\\hat A_{21}&\hat A_{c\bar o}&\hat A_{23}&\hat A_{24}\\0&0&\hat A_{\bar co}&0\\0&0&\hat A_{43}&\hat A_{\bar c\bar o}\end{bmatrix},\quad\hat B=\begin{bmatrix}\hat B_{co}\\\hat B_{c\bar o}\\0\\0\end{bmatrix},\quad\hat C=\begin{bmatrix}\hat C_{co}&0&\hat C_{\bar co}&0\end{bmatrix},$$
with $(\hat A_{co},\hat B_{co})$ controllable, $(\hat C_{co},\hat A_{co})$ observable, and
$$C(sI-A)^{-1}B+D=\hat C_{co}(sI-\hat A_{co})^{-1}\hat B_{co}+D .$$
Subscripts: $c$ controllable, $\bar c$ uncontrollable, $o$ observable, $\bar o$ unobservable.

**Minimal realization (our notes).** A realization has the smallest possible state dimension exactly when it is controllable and observable. Otherwise $(\hat A_{co},\hat B_{co},\hat C_{co},D)$ is a smaller one.

> [!warning] Slide slips (p. 151)
> The completing rows are printed as $\mathbf{p}_{n_1+1},\dots,\mathbf{p}_n$ and the output matrix as $[\hat C_c\ \ 0]$. Intended: $\mathbf{p}_{n_2+1},\dots,\mathbf{p}_n$ and $[\hat C_o\ \ 0]$.

## 6. Observability of LTV systems (slides 161-162)
![[ee502_eee501alllecturenotesabo_p161.jpg]]
![[ee502_eee501alllecturenotesabo_p162.jpg]]

**Notes.** $(C(t),A(t))$ is **observable at $t_0$** if $\mathbf{u}$ and $\mathbf{y}$ on $[t_0,t_1]$, for some $t_1>t_0$, determine $\mathbf{x}(t_0)$ uniquely. The dual system is
$$\frac{d}{dt}\hat{\mathbf{x}}=-A^{\mathsf T}(t)\hat{\mathbf{x}}+C^{\mathsf T}(t)\mathbf{u},\qquad\mathbf{y}=B^{\mathsf T}(t)\hat{\mathbf{x}}+D^{\mathsf T}(t)\mathbf{u},$$
with state transition matrix $\hat\Phi(t,t_0)=\Phi(t_0,t)^{\mathsf T}$ (slide exercise; see the adjoint system in [[EE502 L10 - LTV state equation solution]]).

**Theorem 6.**
1. Observable at $t_0$ iff $W_o(t_0,t)=\int_{t_0}^{t}\Phi(\tau,t)^{\mathsf T}C(\tau)^{\mathsf T}C(\tau)\Phi(\tau,t)\,d\tau$ is nonsingular for some $t>t_0$.
2. Sufficient rank test: $N_0(t)=C(t)$, $N_{k+1}(t)=N_k(t)A(t)+\tfrac{d}{dt}N_k(t)$. If $\operatorname{rank}[N_0(t_1);N_1(t_1);\dots;N_{n-1}(t_1)]=n$ for some $t_1>t_0$, the pair is observable at $t_0$.

Slide exercise: Chen's Gramian uses $\Phi(\tau,t_0)$ instead of $\Phi(\tau,t)$. Since $\Phi(\tau,t)=\Phi(\tau,t_0)\Phi(t_0,t)$, the two differ by the nonsingular factor $\Phi(t_0,t)$ on both sides, so one is nonsingular exactly when the other is.

> [!warning] Watch out
> The LTV dual uses $-A^{\mathsf T}(t)$, not $A^{\mathsf T}(t)$. The rank test is sufficient only, and the recursion includes the derivative $\dot N_k$. The slide lists "$k=0,\dots,n-2$" for the recursion index; the test uses $N_0,\dots,N_{n-1}$.

## Key formulas and terms
| Term | Meaning / formula |
|---|---|
| Observable | $\mathbf{u}$, $\mathbf{y}$ on $[0,t_1]$ fix $\mathbf{x}_0$ uniquely |
| Gramian | $W_o(t)=\int_0^te^{A^{\mathsf T}\tau}C^{\mathsf T}Ce^{A\tau}d\tau$ |
| Reconstruction | $\mathbf{x}_0=W_o(t_1)^{-1}\int_0^{t_1}e^{A^{\mathsf T}\tau}C^{\mathsf T}\hat{\mathbf{y}}(\tau)\,d\tau$ |
| Observability matrix | $\mathcal{O}=[C;CA;\dots;CA^{n-1}]$, $nq\times n$, rank $n$ |
| PBH | $\operatorname{rank}[A-\lambda I;\ C]=n$ at every eigenvalue |
| Dual | $(A^{\mathsf T},C^{\mathsf T},B^{\mathsf T},D^{\mathsf T})$; swaps $W_c$ and $W_o$ |
| Equivalence | $\hat{\mathcal{C}}=P\mathcal{C}$, $\hat{\mathcal{O}}=\mathcal{O}P^{-1}$ |
| Kalman decomposition | only $(\hat A_{co},\hat B_{co},\hat C_{co})$ is in the transfer matrix |
| Minimal | minimal $\iff$ controllable and observable |
| LTV | $W_o(t_0,t)$ with $\Phi(\tau,t)$; $N_0=C$, $N_{k+1}=N_kA+\dot N_k$ (sufficient) |

## Check yourself
> [!question]- 1. $A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$. Observable with $C=\begin{bmatrix}1&0\end{bmatrix}$? With $C=\begin{bmatrix}0&1\end{bmatrix}$?
> First: $CA=\begin{bmatrix}0&1\end{bmatrix}$, $\mathcal{O}=I$: observable. Second: $CA=\begin{bmatrix}0&0\end{bmatrix}$, rank 1: not observable, $x_1$ is invisible.

> [!question]- 2. $A=\operatorname{diag}(-1,-2)$, $C=\begin{bmatrix}1&0\end{bmatrix}$. Which mode is unobservable?
> $\mathcal{O}=\begin{bmatrix}1&0\\-1&0\end{bmatrix}$, rank 1. Eigenvector $\mathbf{e}_2$ of $\lambda=-2$ has $C\mathbf{e}_2=0$: mode $-2$ is unobservable.

> [!question]- 3. Dual of $A=\begin{bmatrix}0&1\\-2&-3\end{bmatrix}$, $B=\begin{bmatrix}0\\1\end{bmatrix}$, $C=\begin{bmatrix}1&0\end{bmatrix}$.
> $\hat A=\begin{bmatrix}0&-2\\1&-3\end{bmatrix}$, $\hat B=\begin{bmatrix}1\\0\end{bmatrix}$, $\hat C=\begin{bmatrix}0&1\end{bmatrix}$. $[\hat B\ \ \hat A\hat B]=I=\mathcal{O}^{\mathsf T}$.

> [!question]- 4. $A=\begin{bmatrix}-4&-3\\1&0\end{bmatrix}$, $B=\begin{bmatrix}1\\0\end{bmatrix}$, $C=\begin{bmatrix}1&3\end{bmatrix}$. Observable? Hidden mode?
> $CA=\begin{bmatrix}-1&-3\end{bmatrix}$, $\mathcal{O}$ has rank 1: not observable. At $\lambda=-3$, $\mathbf{w}=(-3,1)^{\mathsf T}$ and $C\mathbf{w}=0$: mode $-3$ is hidden. $\hat g=\tfrac{s+3}{(s+1)(s+3)}=\tfrac{1}{s+1}$, minimal order 1.

> [!question]- 5. True or false: if $\hat g=N/D$ is coprime with $\deg D=n$, every $n$-state realization is controllable and observable.
> True. Nothing cancels, so the minimal order is $n$, and minimal means controllable and observable.

> [!question]- 6. $A(t)=0$, $C(t)=\begin{bmatrix}1&t^2\end{bmatrix}$. Observable at $t_0$?
> $N_0=(1,t^2)$, $N_1=(0,2t)$, $\det=2t\ne 0$ for $t\ne 0$. Pick $t_1>t_0$ with $t_1\ne 0$: observable at every $t_0$.

## Links
- Course index: [[EE502 Home]]
- Previous: [[EE502 L13 - Controllability]]. Next: [[EE502 L15 - State feedback (extra)]] (observers need observability)
- Needs: [[EE502 L11 - Equivalence and realization]] (change of state, canonical forms)
- Full step-by-step notes (PDF): [EE502_Lecture_14_Observability.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lecture_notes/lecture_14/EE502_Lecture_14_Observability.pdf`
- Original slides (PDF, pp. 140-152 and 160-162): [EEE501AllLectureNotesABO.pdf](file:///home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf) `/home/umaysamli/Desktop/university/ms/semester_2/ee_502/lectures/EEE501AllLectureNotesABO.pdf`

Slides not embedded: 140, 160 (section titles).
