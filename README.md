<!-- solve-problem:9cdc37b6-d738-42bd-beb4-f77a8d865a3c -->
# Small-Set Expansion Hypothesis

A [Tangle Solve problem](https://solve.tangle.tools/problems/9cdc37b6-d738-42bd-beb4-f77a8d865a3c).

## What is the problem?

The Small-Set Expansion Hypothesis (SSEH), formulated by Raghavendra and Steurer (2010), conjectures the hardness of a promise problem on regular graphs. Fix parameters ε, δ > 0 (think ε = δ = 0.01). Given a graph G = (V, E), distinguish:

- **YES case:** there exists a set S ⊆ V with |S| = δ·|V| (i.e., "small," measure δ) whose edge expansion is at most ε: Φ(S) := |E(S, V∖S)| / (d·|S|) ≤ ε.
- **NO case:** every set S with |S| ≤ δ·|V| has expansion at least 1 − ε: Φ(S) ≥ 1 − ε.

The hypothesis: for some choice of constants ε, δ (e.g., ε = δ = 0.01), this promise problem is NP-hard. Note the NO condition only constrains sets of measure *exactly* in a range (typically measure in [δ/2, δ], or ≤ δ depending on formulation — this is a genuine ambiguity; the standard version constrains vol(S) ∈ [δ/2, δ]). Graphs are typically taken d-regular; the relevant quantity is expansion relative to the uniform distribution. A proof of the SSEH would be an NP-hardness reduction, e.g., from Label Cover or a CSP.

## Why does it matter?

The SSEH is arguably the combinatorial core of the Unique Games Conjecture: Raghavendra and Steurer showed SSEH implies UGC (up to parameter degradation), so hardness of a huge number of approximation problems (every CSP, via Raghavendra's SDP-hardness program) would follow. It would settle the exact approximability of graph partitioning objectives (Small-Set Expansion, Uniform Sparsest Cut, balanced separator), with consequences for layout/VLSI and clustering applications. Conversely, refuting it (an algorithm) would be a major step toward algorithms for Unique Games and would suggest SDP hierarchies succeed on these problems.

## What's already known?

- **Reduction SSEH → UGC:** Raghavendra–Steurer (2010) show the SSEH implies the UGC, and introduced the problem partly as a candidate route to proving UGC.
- **UGC → SSEH:** A reduction in the other direction was later given (Raghavendra–Steurer 2013, "Reductions between expansion problems", FOCS; verify exact venue), so SSEH and UGC are equivalent up to polynomial parameter transformations.
- **Algorithmic results:** Arora, Barak, Steurer (2010) gave a subexponential 2^(O(n^(1−O(ε)))) algorithm for SSE on graphs with threshold 1 − ε; Raghavendra–Steurer (2010) gave an n^(O(log log n)) algorithm based on subspace enumeration (a subfactor of the SDP hierarchy).
- **SDP/hierarchy upper bounds:** Constant levels of Lasserre/Sum-of-Squares give good approximations; in fact SoS certifies that random-like graphs are NO instances. This is evidence *for* truth of SSEH-style hardness only at high levels — no poly-time algorithm is known.
- **Attempted hardness proofs:** Reductions from Label Cover via "long code"-style gadgets have been tried; the obstacle is that small-set structure is hard to encode with soundness against the NO case (a single bad set can exist in a sound reduction because expansion must hold for *all* small sets simultaneously, unlike CSP soundness which is about assignments).

## What would count as solving it?

1. **Proof (primary goal):** An NP-hardness reduction showing that, for some constants ε, δ > 0 (any explicit constants suffice), distinguishing the YES/NO cases above is NP-hard. Ideally, hardness under UGC-style reductions from Label Cover with constant soundness.
2. **Refutation:** A polynomial-time algorithm distinguishing the two cases for all constants ε, δ (or for the standard parameter regime). This would be a refutation of SSEH and a major step toward refuting UGC.
3. **Partial results of interest:** improved subexponential algorithms matching the Arora–Barak–Steurer barrier; hardness under weaker assumptions; settling the SoS degree complexity of SSE instances.

## How to start

1. Read Raghavendra–Steurer (2010), especially the reduction showing SSEH → UGC and the subspace-enumeration algorithm — this fixes the exact parameterization.
2. Understand why naive Label Cover reductions fail: soundness must rule out *every* small non-expanding set, not just structured ones; study the "dictatorship test" view where SSE plays the role of a noise operator question (operator Φ_1−ε and its small-set behavior).
3. Study the Arora–Barak–Steurer subexponential algorithm — the n^(1−O(ε)) barrier suggests any NP-hardness proof must exploit structure that algorithm misses, or use non-standard reductions.
4. Consider the equivalent formulation via expansion of the random-walk operator: SSE asks whether the operator ½(I + A/d) has small nontrivial sets of low measure with small expansion; connections to hypercontractivity (reverse small-set expansion, Borell's theorem) are natural tools.

## Key references

- M. Raghavendra and D. Steurer, *Graph Expansion and the Unique Games Conjecture*, STOC 2010. Introduces SSEH, shows SSEH implies UGC, gives n^(O(log log n)) algorithm. https://eccc.weizmann.ac.il/report/2009/073/
- S. Arora, B. Barak, D. Steurer, *Subexponential Algorithms for Unique Games and Related Problems*, FOCS 2010. Gives 2^(O(n^(1−O(ε)))) algorithm for SSE (verify exact exponent dependence). https://arxiv.org/abs/1010.1480
- M. Raghavendra and D. Steurer, *Reductions between Expansion Problems*, FOCS 2013 (verify). Shows UGC implies SSEH, giving equivalence up to parameters.
- P. Raghavendra, *Optimal Algorithms and Inapproximability Results for Every CSP?*, STOC 2008. The downstream program: UGC ⇒ tight SDP-based hardness for all CSPs, which SSEH would inherit.
- S. Khot, *On the Power of Unique 2-Prover 1-Round Games*, STOC 2002. The original UGC paper, for background. https://arxiv.org/abs/math/0208055

## Warnings

- The exact definition of "small set" varies across papers: measure exactly δ, at most δ, or in [δ/2, δ]; parameters matter because they change which reductions compose. Always fix the formulation from Raghavendra–Steurer 2010.
- Do not conflate SSE hardness with UGC hardness: they are equivalent only up to parameter loss, and some results hold under one but not cleanly under the other.
- Common dead end: trying to prove SSEH via standard PCP/long-code reductions — soundness fails because the NO case quantifies over all small sets, including "spurious" ones introduced by the reduction. Any reduction must be extremely sound in an average-case sense.
- The Boolean hypercube with noise operator (reverse small-set expansion via Borell's theorem) is the canonical hard-instance candidate; hardness "on the hypercube" does not imply NP-hardness.

---
*`ALGO-000102` · verified open*

## Acceptance guidance

1. **Proof (primary goal):** An NP-hardness reduction showing that, for some constants ε, δ > 0 (any explicit constants suffice), distinguishing the YES/NO cases above is NP-hard. Ideally, hardness under UGC-style reductions from Label Cover with constant soundness.
2. **Refutation:** A polynomial-time algorithm distinguishing the two cases for all constants ε, δ (or for the standard parameter regime). This would be a refutation of SSEH and a major step toward refuting UGC.
3. **Partial results of interest:** improved subexponential algorithms matching the Arora–Barak–Steurer barrier; hardness under weaker assumptions; settling the SoS degree complexity of SSE instances.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/9cdc37b6-d738-42bd-beb4-f77a8d865a3c?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000102.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000102)
