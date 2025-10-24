---
title: "Meta-Learning for Adaptive Control with Automated Mirror Descent"
description: "We meta-learn mirror-descent adaptive controllers that jointly tune features and geometry, delivering robust quadrotor tracking amid out-of-distribution winds."
authors:
  - { name: "Sunbochen Tang", url: "https://tangsun.github.io" }
  - { name: "Haoyuan Sun" }
  - { name: "Navid Azizan", url: "https://azizan.mit.edu/index.html" }
affiliation: "Massachusetts Institute of Technology"
venue: "L4DC 2025"
equal_contrib: false
year: 2025
arxiv: 2407.20165
pdf: /static/pdfs/mlac_amd.pdf
# supplementary: /static/pdfs/mlac_amd_supp.pdf
code: "Coming Soon"
# social_image: /static/images/mlac-px4/social_preview.png
published_time: 2025-06-01T00:00:00.000Z
# poster: /static/pdfs/mlac_px4_poster.pdf
keywords: [meta-learning, adaptive control, mirror descent, robotics, quadrotors]
# carousel_images:
#   - { src: /static/images/mlac-px4/fig1.png, alt: "Meta-learning and adaptive control pipeline", caption: "Overview of the automated mirror-descent controller." }
#   - { src: /static/images/mlac-px4/fig2.png, alt: "Quadrotor tracking under strong winds", caption: "Learned controller maintains tracking under extreme winds." }
related: []
bibtex: |
  @inproceedings{tang2025meta,
    title = {Meta-Learning for Adaptive Control with Automated Mirror Descent},
    author = {Tang, Sunbochen and Sun, Haoyuan and Azizan, Navid},
    booktitle = {Proceedings of the Learning for Dynamics and Control Conference},
    year = {2025},
    url = {https://arxiv.org/abs/2407.20165}
  }

sections:
- title: "Automated Mirror-Descent Adaptation"
  image: { src: /static/images/mlac-px4/mlac_amd.png, alt: "Meta-learning and adaptive control pipeline", caption: "Offline meta-learning and online mirror-descent control (Fig. 1 in the paper)." }
  md: |
    We recast adaptive control as a bi-level meta-learning problem in which each wind profile defines a separate task. The base learner is a mirror-descent adaptive controller for the manipulator dynamics, initialized with sliding variables $s = \dot{\tilde{q}} + \Lambda \tilde{q}$ and control input $u = \tau(q, \dot{q}) - \hat{Y}(q, \dot{q}; \theta_Y)\hat{a}$. Its update leverages the Bregman divergence $\phi(a) = \lVert a \rVert_p^p$, allowing us to depart from the Euclidean geometry recovered when $p = 2$.

    The meta learner optimizes the feature network parameters $\theta_Y$, controller gains $(P, K, \Lambda)$, and the geometry parameter $p$ so that closed-loop trajectories minimize reference-tracking loss across tasks. Because the true disturbance model is unavailable offline, we fit an ensemble of neural surrogates for the wind-induced drag and unroll them inside a differentiable simulator when computing task losses.

    Jointly searching over representation and geometry lets the controller implicitly regularize parameter updates in a way that matches the underlying disturbance family, yielding faster convergence and tighter Lyapunov certificates than gradient-descent adaptation alone. Theorem 2 in the paper shows that the resulting closed-loop error converges to a compact set proportional to the feature approximation error, and collapses to zero when the learned features are exact.
- title: "Planar Quadrotor Experiments"
  image: { src: /static/images/mlac-px4/tracking_w8.png, width: 90, alt: "Quadrotor tracking under strong winds", caption: "Planar quadrotor tracking performance under crosswinds (Fig. 2 in the paper)." }
  md: |
    We evaluate the learned controller on a fully actuated planar quadrotor subject to crosswinds modeled as quadratic drag with coefficients $(\beta_1, \beta_2) = (0.1, 1.0)$. Tasks arise by sampling wind speeds $w \in [0, 6]$ m/s from a scaled beta distribution and synthesizing random reference loops in the $x$-$y$ plane. Meta-training learns $p \approx 2.2$, signaling a preference for slightly heavier-tailed geometry than the Euclidean baseline $(p = 2.0)$.

    At test time we push the controller far beyond the training distribution, up to `10 m/s` winds. The table summarizes the root-mean-squared tracking error over a 10 s double-loop trajectory:

    | Wind speed (m/s) | RMS, GD baseline (p = 2.0) | RMS, ours (p = 2.2) |
    | ---------------- | --------------------------- | -------------------- |
    | 2.0              | 0.0171                      | 0.0095               |
    | 4.0              | 0.0443                      | 0.0172               |
    | 6.0              | 0.0910                      | 0.0303               |
    | 8.0              | 0.1738                      | 0.0483               |
    | 10.0             | 0.2746                      | 0.0714               |

    The mirror-descent controller halves the tracking error within distribution and delivers even larger gains out of distribution. Figure 2 shows that the learned geometry keeps the roll angle and lateral position on track even after multiple loops, whereas the gradient-descent baseline diverges once the crosswind intensifies.
---

**Abstract.** Adaptive controllers guarantee stability by learning unknown parameters online, but their performance hinges on hand-designed features and Euclidean adaptation laws. We propose MALC-PX4, a meta-learning framework that simultaneously infers disturbance-aware features and the mirror-descent geometry used by the adaptive law. Offline, we solve a differentiable bi-level program over ensembles of wind scenarios to identify the feature network, controller gains, and Bregman divergence parameter that maximize reference-tracking accuracy. Online, the learned mirror-descent controller updates parameters with implicit regularization aligned to the disturbance family, yielding provable convergence to a compact tracking set and exact tracking when the learned features are accurate. Planar quadrotor experiments under strong crosswinds cut the RMS tracking error by over 50% compared to gradient-descent adaptive baselines and generalize to wind speeds well beyond the meta-training range.
