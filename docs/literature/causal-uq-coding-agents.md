# Causal & UQ analyses of coding agents — literature scan

Compiled 16 Nov 2026 for the Harness paper. Scope: papers and blogs that analyse coding harnesses / coding agents, their trajectories and failure modes, using causal inference or uncertainty quantification (UQ). Built on top of the Drive folder's *Causal Inference for AI Verification & Compliance* literature review, notes and deck.

Living version (Claude Doc): https://claude.ai/artifact/3aUJ2Bpp2kZSoHVyAGoYqQ

## Bottom line

- **The existing search has only one agent-trajectory paper**: Who&When (Zhang et al., ICML 2025). Everything below is **new** to the search unless marked otherwise.
- **No paper yet does formal causal inference (SCM / do-interventions with a causal estimand) on coding-agent trajectories at SWE-bench scale.** The causal failure-attribution methods (counterfactual replay, Shapley over steps, abduction–action–prediction) are all validated on Who&When / TRAIL multi-agent logs, not on coding agents. That is the clearest gap for the paper.
- **Harness effects are now studied with controlled designs** (component ablations, two-arm harness swaps, variance decomposition), but none frames them as causal estimands with identification and sensitivity analysis.
- **UQ for coding agents is active in 2026** (early outcome prediction, draft-model gates, uncertainty propagation, Bayesian control), and the variance work says single-run SWE-bench numbers move 2–6 pp from noise alone; one study attributes about 54% of outcome variance to run-to-run repetition.

Method tags: **[Causal]** formal causal method; **[Interv]** interventional / controlled design without a formal causal framework; **[UQ]** uncertainty quantification or calibration; **[Stat]** error bars / variance analysis; **[Desc]** descriptive only. All entries were checked against their arXiv or venue page (abstracts, not full papers) on 16 Nov 2026.

## 1. Directly on target: coding agents with causal or interventional analysis

| Paper | Venue / date | Method | Relevance |
|---|---|---|---|
| [CAM: A Causality-based Analysis Framework for Multi-Agent Code Generation Systems](https://arxiv.org/abs/2602.02138) (Lyu et al.) | arXiv Feb 2026, v3 Jul 2026; ACM DOI 10.1145/3832238 | [Interv] simulated error injection on intermediate outputs to rank causal importance | Closest to causal analysis of a code-gen agent pipeline; repairing top-3 features succeeds 73.6%, pruning cuts tokens up to 33.6%. |
| [Agents Are Systems, Not Models: Rethinking Agentic Evaluation](https://arxiv.org/abs/2610.01618) (Wiedmann et al.) | arXiv Oct 2026 | [Interv] + [Stat] controlled configuration interventions, variance decomposition | ~54% of outcome variance is run-to-run noise; information given to the agent beats model size. Releases 18K+ trajectories. |
| [An Empirical Study of Harness Design for Coding Agents](https://arxiv.org/abs/2609.20804) (Fan et al.) | arXiv Sep 2026 | [Interv] component ablations, 176 matched settings, SWE-bench Verified + Terminal-Bench 2.1 | Most direct harness-component study; context management matters most as the window tightens. |
| [Same Model, Different Harness: Different Coding-Agent Results](https://arxiv.org/abs/2608.26218) (Lewis) | arXiv Aug 2026 | [Interv] two-arm harness comparison, model fixed | Context-shortening harness lifts fail-to-pass from 28% to 49% on SWE-bench Verified. |
| [The Scaffold Effect in Coding Agents: Harness Choice as a Hidden Variable](https://arxiv.org/abs/2607.22585) (Vats & Golev) | arXiv; appears on ICML 2026 virtual site (unconfirmed) | [Stat] paired-task bootstrap CIs | Harness changes tokens per solved task up to 40×; pass-rate gaps 0–8 pp, mostly within CIs. Flag: arXiv ID and submission date look inconsistent. |
| [Beyond Resolution Rates: Behavioral Drivers of Coding Agent Success and Failure](https://arxiv.org/abs/2604.02547) (Mehtiyev & Assunção) | arXiv Apr 2026 | [Desc] with confound control | 19 agents, 9,374 trajectories; the length–failure correlation reverses once task difficulty is controlled. A ready-made confounding example for the paper. |
| [Adoption and Impact of Command-Line AI Coding Agents (Microsoft rollout of Claude Code / Copilot CLI)](https://arxiv.org/abs/2607.01418) (Murphy-Hill et al.) | arXiv Jul 2026 | [Causal] CausalImpact synthetic control, fixed-effects Poisson, placebo test | Field causal estimate: +24% merged PRs (95% CI 14.5–33.7%). Productivity, not trajectories, but a methods template. |
| [CIVER: Causal Intervention Verification for Reliable Code Review](https://arxiv.org/abs/2610.36010) (Song et al.) | arXiv Oct 2026 (comment says WWW 2026, inconsistent) | [Interv] repair-oriented perturbations test whether review findings respond | Interventional test of code-review agents; 77% of genuine defects confirmed. |
| [Capable but Unreliable: Canonical Path Deviation as a Causal Mechanism of Agent Failure](https://arxiv.org/abs/2602.19008) (Lee) | arXiv Feb 2026 | [Causal] natural experiment (same model, same task, success vs failure) + restart intervention | Tool-use agents on Toolathlon, not coding, but the design transfers directly: each off-path call raises next off-path odds by 22.7 pp; restarting low-adherence runs +8.8 pp. |

## 2. Directly on target: coding agents with UQ

| Paper | Venue / date | Method | Relevance |
|---|---|---|---|
| [Uncertainty-Aware Self-Correction for Coding Agents](https://iclr.cc/virtual/2026/10016345) (Almeida et al.) | ICLR 2026 workshop *Agents in the Wild* | [UQ] simplified SAUP step-uncertainty propagation, resample at uncertain steps | SWE-Rebench; up to +15.6 pp pass@1 at 1.2–3× latency. |
| [UQ for LLM Agents via Semantic Abstraction Trajectories](https://icml.cc/virtual/2026/74289) (Kazeev & Ustyuzhanin) | ICML 2026 workshop (SPIGM) | [UQ] black-box trajectory-shape features → failure classifier, abstention | ROC-AUC 0.89 for SWE-agent failure. |
| [How to Speculate about Uncertainty in Agentic Coding? A Draft-Model Gate Method](https://arxiv.org/abs/2609.05274) (Grotov et al.) | arXiv Sep 2026 | [UQ] small draft model scores agent tokens; pre-execution veto gate | Works without logits; −6–8 pp execution errors, −14–19% tokens. |
| [Bayesian control for coding agents](https://arxiv.org/abs/2606.24453) (Papamarkou, …, Shelmanov) | arXiv Jun 2026 | [UQ] belief over candidate correctness; cost-sensitive sequential testing | 6 generators × 9 coding benchmarks. Same MBZUAI group as the AAAI 2026 UQ tutorial in `docs/slides/`. |
| [EarlyEval: Cheaper Agent Evaluation via Early Outcome Prediction](https://arxiv.org/abs/2609.02783) (Shi et al., incl. David Lo) | arXiv Sep 2026 | [UQ] calibrated success/failure classifiers on trajectory prefixes | SWE-bench Verified, Terminal-Bench, Toolathlon; 89–97% accuracy, cuts 13–26% of steps. |
| [Testing-Driven Reliability Audit of Trajectory-Based Early Outcome Prediction](https://arxiv.org/abs/2609.25647) (Cao) | arXiv Sep 2026 | [UQ] calibration transfer across agents (leave-one-agent-out) | Calibration does not transfer cleanly across agents on SWE-bench Verified trajectories. |
| [On Randomness in Agentic Evals](https://arxiv.org/abs/2602.07150) (Bjarnason, Silva, Monperrus) | arXiv Feb 2026 | [Stat] 60K SWE-bench Verified trajectories, 3 models × 2 scaffolds | Single-run pass@1 moves 2.2–6.0 pp; SD > 1.5 pp at temperature 0. Key citation for error bars. |
| [Ask or Assume? Uncertainty-Aware Clarification-Seeking in Coding Agents](https://arxiv.org/abs/2603.26233) | arXiv Mar 2026 | [UQ] (from title) | Abstract could not be fetched (rate-limited); verify before citing. |
| [Agent psychometrics: task-level performance prediction in agentic coding benchmarks](https://arxiv.org/abs/2604.00594) (Ge et al., incl. Fried) | arXiv Apr 2026 | [Stat] item response theory, separates LLM vs scaffold ability | Predictive, not causal, but decomposes harness vs model contribution. |
| [A Rubric-Supervised Critic from Sparse Real-World Outcomes](https://arxiv.org/abs/2603.03800) (Wang, Chen, Ji, Neubig) | arXiv Mar 2026 | Critic on 24 trace features (borderline UQ) | Early stopping +17.7 with 83% fewer attempts. |
| [Task Abstention for LLMs in Code Generation](https://arxiv.org/abs/2605.17029) (Zhou et al.) | arXiv May 2026 | [UQ] distribution-free abstention via multiple testing | Single-shot code gen, not agentic; useful conformal-style baseline. |
| [METR: Analyzing coding agent transcripts to upper-bound productivity gains](https://metr.org/notes/2026-02-17-exploratory-transcript-analysis-for-estimating-time-savings-from-coding-agents/) (Deng) | METR note, Feb 2026 | [Stat] LLM judge + bootstrap CIs; explicitly no causal claim | 5,305 Claude Code transcripts; useful as a counter-example of what transcripts can and cannot support. |

## 3. Causal failure attribution for general / multi-agent systems (methods to transfer to coding)

| Paper | Venue / date | Method | Relevance |
|---|---|---|---|
| [Which Agent Causes Task Failures and When?](https://arxiv.org/abs/2505.00212) (Zhang et al.) — **already in search** | ICML 2025 | Benchmark | 53.5% agent-level, 14.2% step-level. The baseline everything below is measured against. |
| [Causal Agent Replay: Counterfactual Attribution for LLM-Agent Failures](https://arxiv.org/abs/2606.08275) (Shah) | arXiv Jun 2026 | [Causal] run as SCM, do() on a step + re-execution, Monte-Carlo Shapley over steps with CIs | The most formal causal treatment; validated on synthetic SCMs only. A related open-source tool, [trajectory-causal-attribution](https://pypi.org/project/trajectory-causal-attribution/), does step-ablation and Shapley replay (synthetic headline results). |
| [AgenTracer: Who Is Inducing Failure in LLM Agentic Systems?](https://arxiv.org/abs/2509.03312) (Zhang et al.) | ICLR 2026 (proceedings) | [Interv] counterfactual replay + fault injection to label data; RL-trained 8B attributor | Beats Gemini-2.5-Pro / Claude-4-Sonnet by up to 18% on Who&When. |
| [Failure Attribution and Critical Step Prediction Based on Causal Inference](https://arxiv.org/abs/2509.08682) (Ma et al.) | arXiv Sep 2025 | [Causal] Shapley blame + causal discovery (CDC-MAS), counterfactual checks | 36.2% step-level accuracy; fixes raise success 22.4%. |
| [Abduct, Act, Predict (A2P)](https://arxiv.org/abs/2509.10401) (West et al.) | arXiv Sep 2025 | [Causal] Pearl's abduction–action–prediction, simulated by the LLM | 47.5% step accuracy on Who&When algorithm-generated (2.85× baseline). |
| [DoVer: Intervention-Driven Auto Debugging for LLM Multi-Agent Systems](https://arxiv.org/abs/2512.06749) (Ma et al.) | arXiv Dec 2025 | [Interv] edit messages / plans and re-run to test failure hypotheses | Flips 18–28% of failures to successes. |
| [REFLECT: Intervention-Supported Error Attribution for Silent Failures](https://arxiv.org/abs/2606.09071) (Lin et al.) | arXiv Jun 2026 | [Interv] controlled replay with a diagnosis-specific patch | Largest gains on tool-use traces. |
| [CausalFlow: Causal Attribution and Counterfactual Repair for LLM Agent Failures](https://arxiv.org/abs/2605.25338) (Bonagiri et al.) | arXiv May 2026 | [Interv] step-level counterfactual interventions → causal responsibility scores | Includes code generation as one of four domains. |
| [From Flat Logs to Causal Graphs (CHIEF)](https://arxiv.org/abs/2602.23701) (Wang et al.) | arXiv Feb 2026 | [Interv] hierarchical causal graph + counterfactual screening (loose) | Who&When. |
| [FALAT: Tracing Failures via Dependency-Guided Search](https://arxiv.org/abs/2606.00765) (Rafi et al.) | arXiv May 2026 | [Interv] counterfactual-style correction check | 46.0% / 29.1% step accuracy on Who&When. |

Adjacent but not causal: [Rethinking Failure Attribution (MP-Bench)](https://icml.cc/virtual/2026/77945) (ICML 2026 workshop; argues attribution has multiple valid answers), [MASPrism](https://arxiv.org/abs/2605.07509) (prefill NLL/attention signals), [Tracing Agentic Failure from the Flow of Success](https://arxiv.org/abs/2607.12747) (anomaly detection), [Who Broke the System?](https://arxiv.org/abs/2607.07989) (judge with confidence-aware aggregation).

## 4. UQ for general agents (frameworks and metrics)

| Paper | Venue / date | Method | Relevance |
|---|---|---|---|
| [Towards a Science of AI Agent Reliability](https://arxiv.org/abs/2602.16666) (Rabanser, Kapoor, …, Narayanan) | ICML 2026 | [Stat]/[UQ] 12 metrics: consistency, robustness, predictability, safety | Capability gains brought little reliability gain. Princeton HAL group. |
| [Agentic Uncertainty Reveals Agentic Overconfidence](https://arxiv.org/abs/2602.06948) (Kaddour, …, Kusner) | arXiv Feb 2026; listed on ICLR 2026 virtual site | [UQ] verbalised success probability before / during / after | Agents succeeding 22% predict 77%. |
| [UQ for LLM Agents: Taxonomy, Evaluation Protocol, Empirical Study](https://arxiv.org/abs/2609.07395) (Lin et al.) | arXiv Sep 2026 | [UQ] TC-ECE trajectory-checkpoint calibration | Step-level calibration does not imply trajectory-level calibration. |
| [Proper Scoring Rules for Agentic UQ](https://arxiv.org/abs/2605.24756) (Raghu et al.) | arXiv May 2026 | [UQ] Trajectory Proper Score, censored trajectories | Argues trajectory ECE and AUROC miss recalibration effects. |
| [UProp](https://arxiv.org/abs/2506.17419) (Duan et al.) | arXiv Jun 2025 | [UQ] intrinsic vs extrinsic uncertainty via pointwise MI | Uncertainty propagation across agent steps. |
| [SAUP](https://arxiv.org/abs/2412.01033) (Zhao et al.) | arXiv Dec 2024 | [UQ] situation-weighted step propagation | Base method used by the coding-agent self-correction paper above. |
| [When Can Conformal Risk Control Certify LLM Outputs?](https://arxiv.org/abs/2606.29054) (Kotte) | arXiv Jun 2026 | [UQ] CRC bounds and impossibility | Static CRC fails under shift on 14 of 16 transfers; a caution for conformal claims on agents. |

## 5. Descriptive coding-trajectory studies (context, no causal or UQ method)

- [Understanding Code Agent Behaviour: Success and Failure Trajectories](https://arxiv.org/abs/2511.00197) (Majgaonkar et al., Oct 2025): failed runs are longer and more variable; OpenHands, SWE-agent, Prometheus.
- [Failure as a Process: An Anatomy of CLI Coding Agent Trajectories](https://arxiv.org/abs/2607.09510) (Zhao et al., Jul 2026): 63K annotated steps; failures start early and stay hidden.
- [What Resolve Rate Hides: Trajectory Structure Diagnostics](https://arxiv.org/abs/2607.06184) (Shu et al., Jul 2026): search loops are the most stable failure signal.
- [Coherence Collapse](https://arxiv.org/abs/2603.24631) (Kim et al., Mar 2026): 60–69% of failures reach and edit the right functions but still fail.
- [Wink: Recovering from Misbehaviors in Coding Agents](https://arxiv.org/abs/2602.17037) (Nanda et al., Feb 2026; AIWare 2026 per awesome-list): misbehaviour in ~30% of 10K production trajectories, and a **live production A/B test** — the only randomised experiment found on a coding harness.
- [How Coding Agents Fail Their Users](https://arxiv.org/abs/2605.29442) (Tang et al., 2026): 20,574 real sessions.
- [Hindsight-Distilled Sentinel for Coding Agents](https://arxiv.org/abs/2609.39957) (Zhao et al., Sep 2026) and [Log analysis is necessary for credible evaluation](https://arxiv.org/abs/2605.08545) (Kirgis et al., May 2026).
- [Establishing Best Practices for Rigorous Agentic Benchmarks (ABC)](https://arxiv.org/abs/2507.02825) (Zhu et al., 2025).

Causal interpretability of code models (not agents): [Toward a Theory of Causation for Interpreting Neural Code Models (docode)](https://arxiv.org/abs/2302.03788) (Palacio et al., IEEE TSE 2024) and Palacio's [thesis](https://arxiv.org/abs/2505.15023). Fits next to section 6 of the existing review.

## 6. Venues, workshops and blogs to watch

- **ICML 2026 workshop: Statistical Frameworks for Uncertainty in Agentic Systems** ([site](https://agentic-uncertainty-icml2026.github.io/), Seoul, 11 Jul 2026, non-archival). Relevant accepted titles: [When Uncertainty Isn't Enough: Self-Correction in Code Generation](https://icml.cc/virtual/2026/74488), [Do Coding Agents Deceive Us? Capped Evaluation with Randomized Tests](https://icml.cc/virtual/2026/74493), [Conformal Agent Error Attribution](https://icml.cc/virtual/2026/74525), [Predicting Agent Errors from Semantic Scale Trajectories](https://icml.cc/virtual/2026/74472), [Behavioral Consistency as an Uncertainty Signal](https://icml.cc/virtual/2026/74530), [Sparse Binary Reward Degrades Agent UQ in Multi-Seed Evaluation](https://icml.cc/virtual/2026/74517), [Hierarchical Structure for UQ in Agentic Evaluation](https://icml.cc/virtual/2026/74534), [E-valuator: Agent Verifiers with Sequential Testing](https://icml.cc/virtual/2026/74515), [The Illusion of Intervention: LLM-Simulated Experiments are Observational Studies](https://icml.cc/virtual/2026/74531). Titles only; not individually verified.
- **ICML 2026 workshop: Failure Modes in Agentic AI — Reproducible Triggers, Trace Diagnostics, and Verified Fixes** ([page](https://icml.cc/virtual/2026/workshop/54094)). Worth a full sweep.
- **ICLR 2026 workshop: Agents in the Wild** (home of the coding-agent self-correction paper).
- **AAAI 2026 tutorial: UQ for LLMs** (Shelmanov et al., [site](https://sites.google.com/view/aaai-2026-tutorial-th07)); one section on agentic UQ. Slides already in `docs/slides/`.
- **Princeton, [Emerging Trends in AI Agent Evaluation](https://sage.cs.princeton.edu/trends/emerging-trends-paper.pdf)** (Oct 2026): recommends factorial designs for causal attribution of harness components and repeated runs with pass^k.
- Survey list: [awesome-agent-trajectory](https://github.com/YintongHuo/awesome-agent-trajectory).
- Blogs (anecdotal, uncontrolled comparisons): [The Harness Effect](https://codex.danielvaughan.com/2026/04/19/the-harness-effect-same-model-different-tool-different-score/) (Vaughan) and [Why the Harness Changes the Score](https://futureagi.com/blog/coding-agent-harness-benchmark/) (Future AGI, vendor).

Venues from the existing review (NeurIPS, ICML, ICLR, AISTATS, CLeaR, TMLR, JMLR, AAAI, FAccT, CAV, TACAS, FSE, OOPSLA, TOSEM) were searched. The causal-for-agents work appears mostly at ICML / ICLR and their workshops; SE venues (FSE, TOSEM, AIWare) carry the coding-trajectory studies but not yet causal analyses of them.

## 7. Gaps the paper could fill

1. **Formal causal attribution on coding-agent trajectories.** Port counterfactual replay / Shapley-over-steps (Causal Agent Replay, A2P, AgenTracer) from Who&When to SWE-bench or Terminal-Bench, where tests give a cheap, objective outcome and harnesses can be made deterministic.
2. **Harness effects as causal estimands.** Existing harness studies are controlled comparisons; none states the estimand, checks overlap, or reports sensitivity bounds. A factorial harness × model design with CIs would answer Princeton's call directly.
3. **Variance before effects.** With ~54% of variance from repetition and 2–6 pp single-run swings, any harness effect needs repeated runs and UQ; few causal-flavoured papers report this.
4. **Joining the two strands.** UQ papers predict failure; attribution papers explain it. Nobody yet uses step-level uncertainty as a candidate cause, or tests whether uncertainty signals mediate harness effects.

## Caveats

- Only abstracts and venue pages were read, not full papers; numbers are as stated in abstracts.
- Venues are as stated on the fetched pages. Flags: Scaffold Effect (ID/date mismatch, ICML listing unconfirmed), CIVER (WWW 2026 comment vs Oct 2026 submission), Ask or Assume (abstract not read).
