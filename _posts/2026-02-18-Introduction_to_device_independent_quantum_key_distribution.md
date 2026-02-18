---
title: Introduction to device independent quantum_key distribution
date: 2026-02-18 17:10:00 +0100
tags: [notes, quantum key distribution]
math: true
---

*This is a lecture note for the fourth session of Quantum Cryptography Workshop in Toulouse. More information can be found [here](https://gulatiaabhas.github.io/qcryptintoulouse/).* 

## A short introduction to quantum key distribution 

(needs to be finished)

## Review of BB84 protocol 

In the [last session](https://gulatiaabhas.github.io/qcryptintoulouse/quantum-crypto/session-3-qkd.html), we have learned the BB84 quantum key distribution protocol, proposed by **B**ennett and **B**rassard in 19**84**. This protocol has an equivalent version, given below: 

> **Protocol 1** -- Purified BB84
> 1. Alice prepares $N$ EPR pairs $|\phi^{+}\rangle$ and sends the second qubit of each pair to Bob. 
> 2. Alice chooses a uniformly random basis string $\theta=\theta_1\dots \theta_N \in \{0, 1\}^N$, and measures each of her qubits in the $Z(\theta_i=0)$ or $X(\theta_i=1)$ basis to obtain a string $x=x_1\dots x_N\in\{0, 1\}^N$.
> 3. Bob chooses a uniformly random basis string $\tilde{\theta}=\tilde{\theta}_1\dots\tilde{\theta}_N\in\{0, 1\}^N$, and measures each of his qubit in the $Z(\tilde{\theta}_i=0)$ or $X(\tilde{\theta}_i=1)$ basis to obtain a string $\tilde{x}=\tilde{x}_1\dots\tilde{x}_N\in\{0, 1\}^N$.
> 4. Alice and Bob exchange their basis strings $\theta, \tilde{\theta}$ over Classical Authenticated Channel (CAC).
> 5. Alice and Bob throw away the bits from all rounds $i\in[N]$ in which they did not measure in the same basis, and keep only $x_S, \tilde{x}_S$ where $S=\{i\in[N]|\theta_i=\tilde{\theta}_i\}$.
> 6. Alice and Bob check for eavesdroppers: 
>     1. Alice picks a random subset $T\subseteq S$ of size $|T|\approx|S|/2$ and tells Bob over CAC.
>     2. Alice and Bob exchange $x_{T}, \tilde{x}_T$ over CAC and compute the error rate $\delta=|W|/|T|$, where $W=\{i\in T| x_i\neq\tilde{x}_i\}$. If $\delta$ is too large, they abort the protocol. 
> 7. Alice and Bob perform information reconciliation and privacy amplification on the remaining bits $x_R, \tilde{x}_R$ where $R=S\backslash T$. 

Its security relies on Heisenberg uncertainly principle in quantum mechanics, that is if Eve intercepts Alice's qublit and tries to measure it in a basis different from Alice's choice, it will then introduce an error in Bob's measurement with probability $1/2$, and the error rate $\delta$ calculated in Step 6 is sensitive to any of such disturbance. In general, for a protocol not to be aborted, the conditional min-entropy has a lower bound $H_{\min}(X_R|E)\geq |R|(1-h(\delta))$ where $h(\delta)$ is the binary entropy function. This lower bound suggests that Eve has limited knowledge about the remaining bits and a round of privacy amplification then extracts a key that Eve is ignorant about. 


---
### Eve's attack

In the argument above, we have assumed that the devices that perform the measurements are reliable and do the exact tasks as required. However, for mistrusted devices, the security of this protocol is broken. 

Consider the following senario where Alice and Bob get misbehaved devices from Eve:
* When Alice prepares $N$ EPR pairs, she actually prepares $N$ of the following state
$$\rho_{ABE} = \sum_{x, z=0}^1|x, z\rangle\langle x, z|_A\otimes |x, z\rangle\langle x, z|_B\otimes |x, z\rangle\langle x, z|_E$$
* When $\theta_i=0$, Alice and Bob's devices actually measures the first qubit they have in $Z$ basis and when $\theta_i=1$, their devices actually measures the second qubit they have in $Z$ basis. 

Back to the purified BB84 protocol, we will find that by this attack, Eve can now obtain $x$ without disturbing Bob's measurement outcome at all. Hence, the error rate in Step 6 is zero $\delta=0$ while the conditional min-entropy nevertheless vanishes $H_{\text{min}}(X_R|E)=0$. The key distribution protocol becomes insecure. 

Clearly, this can happen because Alice and Bob are using mistrusted measurement devices which they do not know very well. Thus, the notion device independent quantum key distribution protocol becomes important. To design a device independent quantum key distribution protocol, the idea is to take advantage of CHSH games.

## CHSH game 

In Clauser–Horne–Shimony–Holt (CHSH) game, there are two players, Alice and Bob, and each round, a referee sends a random bit $x, y\in\{0, 1\}$ to Alice and Bob respectively. Alice and Bob will then return a bit $a, b\in\{0, 1\}$ respectively to the referee. If $a\oplus b=x\wedge y$, then Alice and Bob win the game. 

To maximize the winning probability, Alice and Bob may use the following strategy: 
> **Optimal strategy of CHSH game**
> 1. Before the game starts, Alice and Bob share an EPR pair $|\phi^+\rangle$. 
> 2. When Alice receives $x=0$ from the referee, she measures her qubit in the standard basis $\{|0\rangle, |1\rangle\}$, and when Alice receives $x=1$ from the referee, she measures her qubit in the Hadamard basis $\{|+\rangle, |-\rangle\}$. i.e. Alice measures the values of following observables
> $$A_0=|0\rangle\langle0|-|1\rangle\langle1|=Z(x=0)\quad\text{and}\quad A_1=|+\rangle\langle+|-|-\rangle\langle-|=X(x=1)$$
> 3. When Bob receives $y=0$ from the referee, he measures his qubit in the basis $\{\cos(\pi/8)|0\rangle+\sin(\pi/8)|1\rangle, -\sin(\pi/8)|0\rangle+\cos(\pi/8)|1\rangle\}$, and when Bob receives $y=1$ from the referee, he measures his qubit in the basis $\{\cos(\pi/8)|0\rangle-\sin(\pi/8)|1\rangle, \sin(\pi/8)|0\rangle+\cos(\pi/8)|1\rangle\}$. i.e. Bob measures the values of the following observables 
> $$B_0=H(y=0)\quad\text{and}\quad B_1=\tilde{H}=\frac{1}{\sqrt{2}}\left(\begin{matrix}1 & -1 \\ -1 & -1 \end{matrix}\right)(y=1)$$
> 4. Alice and Bob return their measurement results $a, b$ to the referee.

It can be shown that the winning probability for this strategy is $p_{a\oplus b=x\wedge y}=\cos^2\pi/8$, which is also the maximum value you can get in any quantum strategy. In particular, in CHSH games, to reach this a success probability of $\cos^2\pi/8$, it is necessary that Alice and Bob are using the above optimal strategy or equivalent due to the CHSH rigidity theorem. 

> **CHSH rigidity theorem.**
> Suppose given a state $|\psi\rangle_{AB}\in\mathbb{C}^{d_A}\otimes\mathbb{C}^{d_B}$ and observables $A_0, A_1$ for Alice and $B_0, B_1$ for Bob such that the corresponding strategy has a success probability $\cos^2\pi/8$ in the CHSH game. Then there exist local isometries $U_A:\mathbb{C}^{d_A}\to\mathbb{C}^2\otimes \mathbb{C}^{d_{A^{\prime}}}$ and $V_B:\mathbb{C}^{d_B}\to\mathbb{C}^2\otimes \mathbb{C}^{d_{B^{\prime}}}$ such that 
> $$U_A\otimes V_B|\psi\rangle_{AB} = |\phi^+\rangle\otimes |\text{junk}\rangle_{A^{\prime}B^{\prime}}$$
> and 
> $$(U_A\otimes V_B)(A_0\otimes I_B)|\psi\rangle = ((Z\otimes I)|\phi^+\rangle)\otimes |\text{junk}\rangle$$
> $$(U_A\otimes V_B)(A_1\otimes I_B)|\psi\rangle = ((X\otimes I)|\phi^+\rangle)\otimes |\text{junk}\rangle$$
> $$(U_A\otimes V_B)(I_A\otimes B_0)|\psi\rangle = ((I\otimes H)|\phi^+\rangle)\otimes |\text{junk}\rangle$$
> $$(U_A\otimes V_B)(I_A\otimes B_1)|\psi\rangle = ((I\otimes \tilde{H})|\phi^+\rangle)\otimes |\text{junk}\rangle$$

**The CHSH rigidity theorem tells us that when two parties are playing CHSH games, their wining probability equals $\cos^2\pi/8$ if and only if they share an EPR pair (upto some local rotations).**

## E91 protocol 

We will now introduce a device independent quantum key distribution protocol --- E91 protocol, proposed by **E**kert in 19**91**. In particular, we consider the protocol to be secure in the following scenario. 

> **The assumptions**
> 1. Alice and Bob’s labs are perfectly isolated: once the protocol starts no information enters or exits their respective labs that is not specified in the protocol.
> 2. Alice and Bob’s random number generators are perfect.
> 3. The devices used by Alice and Bob to perform measurements are arbitrary. These devices are initialized in a state $\rho_{ABE}$ that may be chosen by the adversary. At each step of the protocol, each of Alice and Bob’s devices makes a measurement when instructed, and always produces an outcome $x \in \{0,1\}$. The measurement that is performed is arbitrary. In particular the device may have memory and behave differently in each round.
> 4. At the end of the protocol the devices are discarded and will never be re-used. It is assumed that they will never fall in Eve’s hands.

Device independence refers to the freedom in Assumption 3, which allows the devices to perform any kind of measurements, on any states; both may have been decided on by Eve as part of her “attack”.

> **Protocol 2** -- E91
> 1. Alice prepares $N$ EPR pairs $|\phi^+\rangle$ and sends the second qubit of each pair to Bob. 
> 2. Alice chooses a uniformly random basis string $\theta=\theta_1\dots\theta_N\in\{0, 1\}^N$ and sequentially instructs her measurement device to measure $Z(\theta_i=0)$ or $X(\theta_i=1)$. The device returns a string of outcomes $x=x_1\dots x_N$.
> 3. Bob chooses a uniformly random basis string $\tilde{\theta}=\tilde{\theta}_1\dots\tilde{\theta}_N\in\{0, 1, 2\}^N$ and sequentially instructs his measurement device to measure $H(\tilde{\theta}_i=0)$, $\tilde{H}(\tilde{\theta}_i=1)$, or $Z(\tilde{\theta}_i=2)$. The device returns a string of outcomes $\tilde{x}=\tilde{x}_1\dots\tilde{x}_N$. 
> 4. Alice and Bob tell each other their basis strings $\theta, \tilde{\theta}$ respectively over CAC. 
> 5. Alice selects a random subset $T\subseteq [N]$ of size $N/2$ and announces $T$ to Bob. They set $T^{\prime}=\{j\in T, \tilde{\theta}_j\in\{0, 1\}\}, T^{\prime\prime}=\{j\in T, \theta_j=0\wedge\tilde{\theta}_j=2\}$, and $R=\{j\notin T, \theta_j=0\wedge\tilde{\theta}_j=2\}$. 
> 6. Alice and Bob announce $x_T$ and $\tilde{x}_T$ to each other over CAC. They compute the success probabilities $p_{\text{win}}=|\{j\in T^{\prime}, x_j\oplus \tilde{x}_j=\theta_j\wedge\tilde{\theta}_j\}|/|T^{\prime}|$ and $p_{\text{match}}=|\{j\in T^{\prime\prime}, x_j=\tilde{x}_j\}|/|T^{\prime\prime}|$. If $p_{\text{win}}<\cos^2\pi/8-\delta$ or $p_{\text{match}}<1-\delta$ they abort.
> 7. Alice and Bob perform information reconciliation and privacy amplification on their respective outcomes $x_R, \tilde{x}_R$. 

If both Alice and Bob's devices are ideal (i.e. do the exact tasks as required), then Alice and Bob are playing CHSH games using the optimal strategy to check for eavesdropper. Hence, the security of this protocol relies on the rigidity of CHSH games. In order to avoid the abortion of the protocol, at Step 6, we need to check this protocol is correct ($p_{\text{match}}\geq 1-\delta$) and also win the CHSH game $(p_{\text{win}}\geq\cos^2\pi/8-\delta)$ with high probability. The CHSH rigidity theorem makes sure that there is a strong quantum entanglement shared between Alice and Bob and the monogamy principle of quantum entanglement then guarantees that Eve cannot be strongly correlated with the entanglement between Alice and Bob. Hence, Eve has limited knowledges about $x_R=\tilde{x}_R$. A round of privacy amplification then extracts a key that Eve is ignorant about. 

## The security of E91 protocol

It can be shown that the conditional min-entropy has a lower bound $H_{\text{min}}(X_R|E)\geq |R|(1-C\sqrt{\delta})$ for some small constant $C$ under *collective attacks*. 

A collective attack is one in which the initial state of the devices takes the form $\rho_{ABE}^{\otimes N}$, and moreover the measurement performed by the device in each round is the same (on the same inputs), i.e. the device is memoryless. Under this assumption, the conditional min-entropy $H_{\text{min}}(x_j|E)$ is the same for each bit $j\in R, T^\prime$ and is additive among these bits. 

It suffices to show the lower bound for a single bit conditional min-entropy, and the idea follows. First, we need to know the difference between the true winning probability $\hat{p}_{\text{win}}$ and the observed winning probability $p_{\text{win}}$ in Protocol 2 given that $p_{\text{win}}\geq\cos^2\pi/8-\delta$ for passing the security check at Step 6. We will need to use the following theorem to show the concentration of $p_{\text{win}}$ around its true value $\hat{p}_{\text{win}}$.  
> **Theorem 1 -- Chernoff bound.** Let $X_1, \dots, X_N$ be i.i.d random variables taking values in $\{0, 1\}$, and $\mu=\mathbb{E}[X_i]$. Then for all $0<\alpha<1$,
> $$\text{Pr}\left(\left|\frac{1}{N}\sum_{i=1}^NX_i-\mu\right|>\alpha\mu\right)\leq 2e^{-\frac{\alpha^2\mu N}{3}}.$$
We apply the above theorem for $Z_1, \dots, Z_{|T^\prime|}$ where $Z_i=1$ if Alice and Bob win CHSH game at $i$-th round and $Z_i=0$ otherwise. It hence leads to the following relation: 
$$\text{Pr}(\hat{p}_{\text{win}}<\frac{1}{1+\alpha}p_{\text{win}})\leq e^{-\frac{\alpha^2\hat{p}_{\text{win}}|T^\prime|}{3}}.$$
Noticing that for the worst strategy in CHSH game, we still have $\hat{p}\geq\frac{1}{2}-\frac{\sqrt{2}}{4}$ and $|T^{\prime}|\approx \frac{N}{3}$, we can then always conclude that when $N$ is large enough, 
$$\hat{p}_{\text{win}}\geq p_{\text{win}}/(1+\alpha)\geq\cos^2\pi/8-2\delta (\text{choose }\alpha=\delta),$$
conditioned on the protocol not being absorted. The above lower bound for the true winning probability limits the probability that Eve guess Alice's key correctly according to the following lemma. 

> **Lemma 1 -- CHSH gussing lemma.** Consider a guessing game with three players, Alice, Bob, and Eve. Alice receives an input $\theta\in\{0, 1\}$, Bob receives a $\tilde{\theta}\in\{0, 1, 2\}$, and Eve receives no input. The players produce outcomes $x, \tilde{x}, z\in\{0, 1\}$ respectively. They win the game if and only if the following conditions hold: 
> 1. If $\tilde{\theta}\in\{0, 1\}$, then $x\oplus \tilde{x}=\theta\wedge\tilde{\theta}$.
> 2. If $\theta=0$ and $\tilde{\theta}=2$, then $x=z$.
> 
> Let $p_{\text{win}}$ be the probability that the first test passes and $p_{\text{id}}$ be the probability that the second test passes. For an arbitrary strategy for the players in the this game, if $p_{\text{win}}\geq\cos^2\pi/8-\delta$, then $p_{\text{id}}\leq 1/2+2\delta^{1/2}$. 

It is straightforward to conclude that $\hat{p}_{\text{id}}\leq 1/2 + 2(2\delta)^{1/2}$ given the lower bound of $\hat{p}_{\text{win}}$ from above. Hence 
$$H_{\text{min}}(x_j|E)= -\log \hat{p}_{\text{id}} \geq -\log\left(\frac{1}{2}+2(2\delta)^{1/2}\right)\geq 1-C\sqrt{\delta},$$
for some constant $C$. Summing over $j\in R$, we obtained the desired lower bound for the conditional min-entropy. A round of privacy amplification for such a ($\approx |R|$)-source will extract a key that Eve is ignorant about. 