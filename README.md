<!-- solve-problem:07f6f1cc-1e41-4ec9-810f-737c43ef4e67 -->
# Unique Games Conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/07f6f1cc-1e41-4ec9-810f-737c43ef4e67).

## What is the problem?

A **Unique Game (UG)** instance is a system of constraints on variables $x_1,\dots,x_n$, each taking values in an alphabet $\Sigma = \{1,\dots,k\}$. Each constraint is a pair $(x_i, x_j)$ with a permutation $\pi: \Sigma \to \Sigma$, and is satisfied iff $x_j = \pi(x_i)$. Equivalently, a UG instance is a 2-prover 1-round game where each question has exactly one acceptable answer-pair — hence "unique."

The **Unique Games Conjecture** (Khot, 2002) asserts:

> For every constant $\varepsilon, \delta > 0$, there exists an alphabet size $k = k(\varepsilon,\delta)$ such that it is NP-hard to distinguish between:
> - **(YES)** there is an assignment satisfying at least a $(1-\varepsilon)$ fraction of constraints, and
> - **NO** every assignment satisfies at most a $\delta$ fraction of constraints.

So UGC posits a hardness-of-approximation result for Max-2Lin(k) with an arbitrarily large gap: the optimum is either nearly 1 or nearly 0. Note the alphabet size $k$ may grow as the gap parameters shrink, and this dependence is not pinned down by the conjecture — it suffices that some finite $k$ works. The conjecture is widely believed to be true but this is genuinely open; a refutation (an algorithm) would also be a major result.

## Why does it matter?

UGC, if true, yields optimal inapproximability results for a huge swath of problems: Vertex Cover (2−ε), Max Cut (Goemans–Williamson constant ≈ 0.878), every fixed-template CSP (via Raghavendra's theorem), charting almost the entire approximability landscape of CSPs under one principle. If UGC is false — i.e., a polytime algorithm distinguishes the two cases — the consequences are equally dramatic: subexponential or even polynomial algorithms for many problems, improved approximation algorithms across the board, and semidefinite-programming hierarchies would be far more powerful than currently known. Either resolution reshapes approximation complexity.

## What's already known?

- **Khot (2002)** formulated UGC and derived initial hardness consequences.
- **Khot–Kindler–Mossel–O'Donnell (2007)** proved the Majority-is-Stablest theorem in Gaussian noise stability, exactly the tool needed to prove UGC-hardness of Max Cut at the Goemans–Williamson constant; Mossel–O'Donnell–Oleszkiewicz's invariance principle underpins this.
- **Raghavendra (2008)** showed that a canonical SDP rounding scheme is optimal for every CSP *assuming UGC*; unconditionally, it's optimal among SDP-relaxation-based algorithms.
- **Algorithmic side:** Arora–Barak–Steurer (2010) gave a subexponential algorithm ($2^{O(n^{\mathrm{poly}(\varepsilon)})}$) for $(1-\varepsilon,\tfrac12)$-UG — weak evidence against NP-hardness but consistent with UGC since it's superpolynomial. Trevisan's SOS-based and Lasserre-based results give $(1-O(\varepsilon))$-approximation in $n^{O(k)}$ time, implying UG with constant $k$ is easy — this is why $k$ must grow with the gap.
- **Partial hardness:** NP-hardness is known for restricted cases (bounded-degree, expanding constraint graphs: Khot–Regev 2008; O'Donnell–Wu via composition; constant-wise variants). UGC over integers (Z-UGC) was proven NP-hard (Khot–Moshkovitz).
- **Known obstructions:** Standard reductions amplify gaps via parallel repetition (Raz's theorem; Feige–Kindler–O'Donnell–Rao; Raz's counterexample to strong forms), and the known constructions of UG hardness gadgets appear to hit a barrier around $1 - O(\sqrt{\varepsilon})$ soundness — related to why no known reduction produces $\delta \to 0$ with $1-\varepsilon$ completeness.

## What would count as solving it?

1. **Proof (UGC true):** For every $\varepsilon,\delta>0$, a polynomial-time reduction from, say, 3SAT to UG instances with completeness $1-\varepsilon$ and soundness $\delta$ over some alphabet $k(\varepsilon,\delta)$.
2. **Refutation (UGC false):** A polynomial-time algorithm that, given a UG instance with optimum $\ge 1-\varepsilon$, finds (or certifies) an assignment satisfying $\ge \delta$ fraction, for some fixed constants or appropriately traded-off $\varepsilon,\delta$ with $k$ polynomial in the gap. A weaker refutation — an algorithm distinguishing the two cases in, say, quasipolynomial time for all $k$ — would still be a landmark but not a full resolution.
3. Partial results of interest: NP-hardness at completeness $1-\varepsilon$ and soundness $\delta = \delta(\varepsilon) \to 0$; or unconditional lower bounds for specific SDP/SOS hierarchies on UG instances.

## How to start

1. Read Khot's original 2002 paper, then the survey **Khot, "On the Unique Games Conjecture" (CCC 2010 invited talk)** for the landscape.
2. Read **Raghavendra (STOC 2008)** to understand the "UGC = SDP optimality" dictionary; then **KKMO (FOCS 2004/2007)** for the Gaussian-noise-stability machinery — this is the toolkit any hardness proof likely needs.
3. Understand **why current reductions fail**: study the soundness barrier in Dinur–Mossel–Regev? (verify) and the Arora–Barak–Steurer subexponential algorithm to internalize the lower-bound constraints on $k$.
4. Decide your camp: attack hardness via new composition/dinurization + noise-stability ideas (likely needing a new type of "majority is stablest"-like theorem over non-Gaussian distributions or a smoothness-reducing gadget), or attack algorithms via SDP/SOS with instance structure (e.g., exploiting low-threshold-rank or spectral properties to beat known integrality gaps). The main obstacle for algorithms: known integrality-gap instances (Khot–Vishnoi 2005) show basic SDPs fail; for hardness, the $1-\sqrt{\varepsilon}$ barrier in known gadgets.

## Key references

- **S. Khot, "On the Power of Unique 2-Prover 1-Round Games," STOC 2002.** Introduces UGC and proves initial hardness consequences. (verify final venue details)
- **S. Khot, G. Kindler, E. Mossel, R. O'Donnell, "Optimal Inapproximability Results for MAX-CUT and Other 2-CSPs," FOCS 2004 / SIAM J. Comput. 2007.** Proves Majority-is-Stablest and derives UGC-hardness of Max Cut at the Goemans–Williamson ratio.
- **P. Raghavendra, "Optimal Algorithms and Inapproximability Results for Every CSP?," STOC 2008.** Shows a basic-SDP rounding algorithm is optimal for every CSP assuming UGC.
- **S. Arora, B. Barak, D. Steurer, "Subexponential Algorithms for Unique Games and Related Problems," FOCS 2010.** Gives $2^{O(n^{\mathrm{poly}(\varepsilon)})}$ algorithms for UG, a key structural constraint on UGC's truth.
- **S. Khot, N. Vishnoi, "The Unique Games Conjecture, Integrality Gap for Cut Problems and Embeddability of Negative-Type Metrics into ℓ₁," FOCS 2005.** Constructs canonical SDP integrality-gap instances for UG.
- **S. Khot, "On the Unique Games Conjecture," IEEE CCC 2010 (invited talk survey).** Authoritative survey of the conjecture's status and consequences.
- **IAS exposition (2026)** — referenced in the census record; not independently verifiable, treat as (verify).

## Warnings

- UGC is NOT the same as hardness of Unique Games for fixed alphabet $k$ — that's known to be false (algorithms exist); the conjecture requires $k$ to grow with the gap parameters. Many flawed "refutations" and "proofs" ignore this.
- The conjecture only concerns the $(1-\varepsilon, \delta)$ regime; hardness for constant-gap regimes (e.g., completeness $\tfrac12$) is essentially open in different ways and shouldn't be conflated.
- Watch out for the distinction between refuting UGC (algorithm) and refuting specific consequences (e.g., disproving that GW is optimal for Max Cut would not settle UGC but would strongly suggest it's false).
- Parallel repetition (Raz) is essential but lossy; naive attempts to compose UG reductions have known counterexamples (Feige et al.; Raz's counterexample to polynomial bounds). The "IAS (2026)" source is unverifiable — do not rely on it.

---
*`ALGO-000235` · unverified*

## Acceptance guidance

1. **Proof (UGC true):** For every $\varepsilon,\delta>0$, a polynomial-time reduction from, say, 3SAT to UG instances with completeness $1-\varepsilon$ and soundness $\delta$ over some alphabet $k(\varepsilon,\delta)$.
2. **Refutation (UGC false):** A polynomial-time algorithm that, given a UG instance with optimum $\ge 1-\varepsilon$, finds (or certifies) an assignment satisfying $\ge \delta$ fraction, for some fixed constants or appropriately traded-off $\varepsilon,\delta$ with $k$ polynomial in the gap. A weaker refutation — an algorithm distinguishing the two cases in, say, quasipolynomial time for all $k$ — would still be a landmark but not a full resolution.
3. Partial results of interest: NP-hardness at completeness $1-\varepsilon$ and soundness $\delta = \delta(\varepsilon) \to 0$; or unconditional lower bounds for specific SDP/SOS hierarchies on UG instances.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/07f6f1cc-1e41-4ec9-810f-737c43ef4e67?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000235.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000235)
