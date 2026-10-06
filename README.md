<h1 align="center">RSI Safety</h1>

<p align="center"><strong>Safety Must Survive Self-Improvement:<br>Why Failures Persist and How Agents Recover</strong></p>

<p align="center">
  Yunbei Zhang<sup>†</sup> · Janet Wang<sup>†</sup> · Saiyue Lyu · Yingqiang Ge<br>
  Kaiqu Liang · Zijian Jin · Chandan K. Reddy · Jihun Hamm<br>
  <sub>† Equal contribution</sub>
</p>

<p align="center">
  <a href="https://rsi-safety.github.io"><img src="https://img.shields.io/badge/Project-Page-111827?style=flat-square" alt="Project page"></a>
  <a href="https://arxiv.org/abs/2610.01073"><img src="https://img.shields.io/badge/arXiv-2610.01073-A45545?style=flat-square" alt="Paper on arXiv"></a>
  <a href="https://github.com/rsi-safety/RSI-Safety/stargazers"><img src="https://img.shields.io/github/stars/rsi-safety/RSI-Safety?style=flat-square&color=8B8178" alt="GitHub stars"></a>
</p>

## To-do

- [ ] Release code
- [ ] Release data
- [x] ~~Release archive~~ · [arXiv](https://arxiv.org/abs/2610.01073)

## Overview

Recursive self-improvement lets agents carry useful changes across generations. We study why unsafe behavior persists and how agents recover, using fixed LLM editors and four stateful authorization tasks. Paired experiments separate what passes validation, what runs next, and what supplies the next edit.

[![Failure entry, persistence through selection, and the separate roles of deployment validation and editing source.](assets/figures/overview.png)](assets/figures/overview.png)

*Figure 1. Detecting a failure, producing a repair, and ending unsafe execution are different outcomes. Red denotes the current program, blue the founder, and green a currently passing fallback.*

## Main results

### 1. Historical scores can preserve a failure

Historical readout retains the same unsafe programs in **22 of 48 framework histories through iteration 100**, despite a correct alternative in every affected archive. Current readout restores full correctness on the original suite. Score refresh also improves matched continuations, while independent tests expose residual failures.

[![Authorization-change trajectories and framework readouts under historical evaluations, current checks, and score refresh.](assets/figures/authorization-and-selection.png)](assets/figures/authorization-and-selection.png)

*Figure 2. Top: 72 authorization-change histories. Bottom: 48 framework histories. Readouts select from the same archives. Score refresh continues to iteration 60, while readouts continue to 100.*

### 2. Rejection does not end unsafe execution

When the incumbent and both proposals fail the same tests, **keep retains the failed program**, while founder fallback restores safety. Holding all proposals and outcomes fixed isolates the retention rule. A separate analysis of 432 frozen pools shows that the gap remains even at full validation coverage.

[![Frozen candidate pools and identical rejected proposals reveal the difference between keep and founder fallback.](assets/figures/retention-after-rejection.png)](assets/figures/retention-after-rejection.png)

*Figure 3. Each editor processes 42 failed roots. The table shows only all-rejected cases. The authorization contract is unchanged, and unknown outcomes do not count as safe.*

### 3. Editing source changes recovery

From the **same 42 failed programs**, editing the current program restores safety in **66.7%** of roots after six generations, compared with **97.6%** when editing the founder. The advantage varies across editors. Founder editing changes the source of proposals without automatically deploying the founder.

[![Recovery by original editor and feedback condition, with GPT and Sonnet trajectories from the same failed roots.](assets/figures/recovery.png)](assets/figures/recovery.png)

*Figure 4. Original editors: Devstral 2, GLM 4.7 Flash, and Qwen3 Coder. GPT and Sonnet each process all 42 roots. Safety restored describes the current selection, not safety throughout its history.*

### 4. Safety can coexist with useful optimization

Across **288 matched blocks and 12 generations**, full validation and validated rollback each finish with fully correct programs while retaining **over 43% mean deployment service-cost savings**. Founders already complete permitted tasks correctly. The useful improvement is lower service cost, and savings exclude validation expenditure.

[![Consent safety across generations and deployment savings versus full correctness.](assets/figures/safety-and-utility.png)](assets/figures/safety-and-utility.png)

*Figure 5. Left: 72 consent lineages. Right: mean results across 288 blocks. E/M denote efficiency/maintenance objectives, and I/F denote inherited/founder editing. Safety requires no unauthorized effects. Full correctness also requires completing permitted work.*

## Testbed

Each instance is an ordered event stream that combines protected requests with changes in authorization or environment state.

| Task family | Safety requirement |
| --- | --- |
| Session authorization | Permission remains current for the requested session and resource. |
| Filesystem containment | The resolved write target stays within the authorized root. |
| Tool approval | Approval covers the action, scope, uses, and expiration. |
| User consent | Agreement remains applicable to the requested action. |

Each core block has 24 public, 24 audit, and 24 hidden streams: **20,736 stream assignments across 288 blocks**. These are reused assignments, not unique authorization problems. Independent effect traces distinguish unauthorized actions from completion of permitted work.

All five figures are exported from the Overleaf vector figures as **7680-pixel-wide PNGs**. Click a figure to open the full-resolution image.

## Citation

```bibtex
@article{zhang2026safety,
  title={Safety Must Survive Self-Improvement: Why Failures Persist and How Agents Recover},
  author={Zhang, Yunbei and Wang, Janet and Lyu, Saiyue and Ge, Yingqiang and Liang, Kaiqu and Jin, Zijian and Reddy, Chandan K and Hamm, Jihun},
  journal={arXiv preprint arXiv:2610.01073},
  year={2026}
}
```
