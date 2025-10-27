---
title: "ECO: Energy-Constrained Operator Learning for Chaotic Dynamics with Boundedness Guarantees"
description: "We introduce the Energy-Constrained Operator (ECO), a framework that learns chaotic dynamics while enforcing provable trajectory boundedness. ECO uses a learnable energy function and a novel convex quadratic projection layer to guarantee long-term stability and preserve invariant statistics for chaotic PDEs."
authors:
  - { name: "Sunbochen Tang", url: "https://https://tangsun.github.io", equal: true }
  - { name: "Andrea Goertzen", url: "https://https://www.linkedin.com/in/andrea-goertzen/", equal: true }
  - { name: "Navid Azizan", url: "https://azizan.mit.edu/index.html"}
affiliation: "Massachusetts Institute of Technology"
venue: "Preprint"          # or "NeurIPS 2025 (to appear)"
equal_contrib: true
# year: 2026
# pdf: /static/pdfs/eco_pde.pdf
# poster: /static/pdfs/eco_pde_poster.pdf
# social_image: /static/images/chaos-learning/eco_social_preview.png
keywords: [chaos, dynamical systems, dissipativity, machine learning, forecasting, pde, operator learning, boundedness guarantees]
published_time: 2025-10-26T00:00:00.000Z
related: []
# bibtex: |
#   @inproceedings{tang2026eco,
#     title={{ECO}: {E}nergy-{C}onstrained {O}perator {L}earning for {C}haotic {D}ynamics with {B}oundedness {G}uarantees},
#     author={Anonymous},
#     booktitle={International Conference on Learning Representations},
#     year={2026}
#   }
sections:
- title: "Problem Formulation"
  md: |
    Data-driven models for chaotic partial differential equations (PDEs) often fail during long-horizon forecasting due to a phenomenon called "finite-time blowup". Small, accumulating prediction errors are amplified by the system's chaotic nature, causing trajectories to diverge to unbounded, non-physical values. Our objective is to learn a neural operator for dissipative chaotic systems that preserves the statistical properties of the true dynamics by guaranteeing model stability and preventing this failure model.
- title: "Method Overview"
  image: { src: /static/images/chaos-pde/method.png, alt: "Architecture enforcing dissipativity", caption: "Our Energy-Constrained Operator (ECO) uses an unconstrained backbone, a learned energy functional, and a dissipative projection layer to guarantee boundedness." }
  md: |
    We introduce the Energy-Constrained Operator (ECO), a framework that learns dissipative dynamics by construction. It consists of two learnable components: an unconstrained neural operator backbone (e.g., DeepONet) and a quadratic, energy-like Lyapunov functional. These are integrated into a novel **convex quadratic projection layer** that enforces a computationally efficient dissipativity condition, ensuring the learned model's predictions remain bounded.
- title: "Certified Boundedness"
  md: |
    Leveraging control theory, we derive algebraic conditions that guarantee dissipativity based on a learnable Lyapunov function. We introduce a differentiable convex quadratic projection layer that enforces these conditions in a closed form. While it uses a smooth sigmoid function to approximate a hard projection, we provide a formal proof that this still guarantees the learned dynamical system is dissipative, with all trajectories converging to a learned invariant set. This set also serves as a tight outer estimate of the system's strange attractor.
- title: "Experiments"
  image: { src: /static/images/chaos-pde/NS_snapshots.png, alt: "Forecast accuracy plots", caption: "Comparison on the Kuramoto-Sivashinsky and 2D Navier-Stokes equations." }
  md: |
    We demonstrate ECO's effectiveness on the Lorenz 63, Kuramoto-Sivashinsky (KS), and 2D Navier-Stokes equations with Kolmogorov forcing. In all cases, the unconstrained DeepONet baseline quickly becomes unstable and its predictions blow up. In contrast, ECO produces stable, long-horizon forecasts that accurately recover the complex spatio-temporal patterns and invariant statistics of the true dynamics. Quantitative metrics show ECO achieves significantly lower KL divergence and log-spectral distance compared to the baselineitle: "Ablations & Robustness"
  md: |
    Comparing ECO to an identical DeepONet backbone without the projection layer highlights the critical role of our constraint. The unconstrained model consistently fails, producing unbounded trajectories and unstructured statistical distributions, while ECO remains stable and accurate. This demonstrates the importance of the boundedness guarantee for reliable forecasting. Notably, these stability gains are achieved without any prior knowledge of the system's statistics, as ECO learns the stabilizing energy function directly from data.
---

**Abstract.** Chaos is a fundamental feature of many complex dynamical systems, including weather systems and fluid turbulence. These systems are inherently difficult to predict due to their extreme sensitivity to initial conditions. Many chaotic systems are dissipative and ergodic, motivating data-driven models that aim to learn invariant statistical properties over long time horizons. While recent models have shown empirical success in preserving invariant statistics, they are prone to generating unbounded predictions, which prevent meaningful statistics evaluation. To overcome this, we introduce the Energy-Constrained Operator (ECO) that simultaneously learns the system dynamics while enforcing boundedness in predictions. We leverage concepts from control theory to develop algebraic conditions based on a learnable energy function, ensuring the learned dynamics is dissipative. ECO enforces these algebraic conditions through an efficient closed-form quadratic projection layer, which provides provable trajectory boundedness. To our knowledge, this is the first work establishing such formal guarantees for data-driven chaotic dynamics models. Additionally, the learned invariant level set provides an outer estimate for the strange attractor, a complex structure that is computationally intractable to characterize. We demonstrate empirical success in ECO's ability to generate stable long-horizon forecasts, capturing invariant statistics on systems governed by chaotic PDEs, including the Kuramoto-Sivashinsky and the Navier-Stokes equations.