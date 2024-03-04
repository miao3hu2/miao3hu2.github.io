---
title: Summary of My Master's Thesis
date: 2024-03-04 17:40:00 +0100
tags: [summary, thesis]
math: true
---

Research in quantum information is guided by the goal of fully exploring and exploiting a phenomenon in quantum systems --- entanglement. This phenomenon is, by definition, said to exist in a multi-party (or global) quantum system whenever the state of the system is not separable, i.e. it cannot be described by a collection of states each belonging to a member (or local) system, and it is very beneficial for many quantum technologies to have a protocol that can probe and characterize entanglement in a quantum system. Randomized measurements give such a protocol that draws favorable attention as it has the advantage of being able to be processed purely in a local manner. More explicitly, people have shown, for example at [here](https://arxiv.org/abs/1808.06558), [here](https://arxiv.org/abs/1910.10732), and [here](https://arxiv.org/abs/1605.08529), that one can measure and quantify, to some extent, entanglement in a global system by repeating the measurement of a local observable on a random basis.  

It is worth mentioning that a dataset obtained from randomized measurements can be naturally analyzed using random tensor theory and graph theory. To put things clearer, we consider a global system $$\mathcal{H}$$ consisting of $$D$$ local systems $$\{\mathcal{H}_c\}_{c=1,\cdots, D}$$, i.e. $$\mathcal{H}=\bigotimes_{c=1}^D\mathcal{H}_c$$. Then such a dataset is a distribution of a random variable $$X$$ with the following structure 
$$
\begin{equation}
  X=\mathrm{Tr}(AU\rho U^{\dagger}), \text{ where } \left\{
  \begin{array}{l}
    A=\bigotimes_{c=1}^DA_c \text{ for } A_c:\mathcal{H}_c\to\mathcal{H}_c \\
    U=\bigotimes_{c=1}^DU_c \text{ for } U_c \text{ a unitary matrix }\\
    \rho:\mathcal{H}\to\mathcal{H}
  \end{array}\right.
\end{equation}
$$
and $$\rho$$ is the density operator describing the state of the global system and $$\{A_c\}_{c=1, \cdots, D}$$ are observables belonging to their corresponding local systems. Valuable information that can be extracted from randomized measurements is contained in the moments of the distribution of the random variable $$X$$, that is 
$$
\begin{equation}
  \langle X^n \rangle = \int\prod_{c=1}^DdU_c\,[\mathrm{Tr}(AU\rho U^{\dagger})]^n
\end{equation}
$$
where $$dU_c$$ is the Haar measure and hence the analysis of these moments falls naturally into the theory of random tensors as presented in [this paper](https://arxiv.org/abs/2201.12778). 

The motivation for the work in my master's thesis is to clarify the "to some extent" part of the aforementioned comment on the relation between randomized measurements and entanglement detection. With the toolbox from random tensor theory and graph theory, this goal becomes achievable, starting with the question --- can we relate the moments of the distribution from randomized measurements with the amount and form of entanglement in a system at a state of general interest in quantum information?

At the outset of resolving the above question, we have focused on two parametric families of states on bipartite systems important in quantum information for their invariance properties: the isotropic states (invariant under $$U\otimes U^*$$ transformation) and the $$O\otimes O$$ invariant states (convex combination of the isotropic states and the Werner states where the latter are $$U\otimes U$$ invariant). In conclusion, we have found that randomized projections of an isotropic state give an exponential distribution at the limit where $$\dim\mathcal{H}_c=\infty$$ for all $$c$$, or, to use the language in free probability theory, converges weakly to an exponential distribution. This result can also be interpreted as follows. In a bipartite system, an exponential distribution from randomized projections is always associated with an entangled state in the form of isotropic states, and the fatness of the exponential distribution is linked with the amount of entanglement in the form of isotropic states. The interpretation has a remarkable consequence. It tells us that in the case where we have a general distribution from randomized projections, by dividing out an exponential distribution from the general distribution, one can extract the amount of entanglement existing in a bipartite system in the form of isotropic states, which has also been confirmed by our result on the randomized projections of a more general family of states, the O-O invariant states. Thus, the work in my master's thesis brings us one step closer to the full clarification of the "to some extent" part of the comment above. 

Of course, there are other unexpected results beyond the scope of randomized measurements in the thesis. A nameable one is an invariant property of a special set of polynomials of the density operators --- the set of trace invariants, which is studied in the thesis since it not only contains polynomials that measure entanglement but also spans the set of moments from randomized measurements, under any graph isomorphisms. More specifically, we have discovered that if one adopts graphical representations for the trace invariants of the density operators describing the isotropic states,  then there is a recursive relation relating these trace invariants with the polynomials similarly defined on the graphs obtained by deleting and contracting an edge in these graphical representations. Such a recursive relation is known as the edge deletion-contraction relation and it is the defining property of many graph polynomials, such as the Tutte polynomial and the Bollobás-Riordan polynomial, which have been studied extensively in graph theory since they encode fine structures of graphs and give a way to study these structures algebraically. Our results add one more application of graph polynomials in quantum information, in addition to the existing applications in statistical mechanics (the Potts model) and mathematical physics (non-commutative quantum field theory). 
