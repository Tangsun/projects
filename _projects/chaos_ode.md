---
title: "Learning Chaotic Dynamics with Embedded Dissipativity"
description: "Neural operator learns chaotic dissipative dynamics with a learned Lyapunov certificate to enforce bounded trajectories and preserve long-term statistics."
authors:
  - { name: "Sunbochen Tang", url: "https://tangsun.github.io" }
  - { name: "Themistoklis Sapsis", url: "https://sandlab.mit.edu/about/" }
  - { name: "Navid Azizan", url: "https://azizan.mit.edu/index.html" }
affiliation: "Massachusetts Institute of Technology"
venue: "arXiv preprint"
equal_contrib: false
year: 2024
arxiv: 2410.00976
pdf: /static/pdfs/chaos_ode.pdf
poster: /static/pdfs/chaos_ode_poster.pdf
social_image: /static/images/chaos-learning/social_preview.png
keywords: [chaos, dynamical systems, dissipativity, machine learning, forecasting]
published_time: 2024-10-02T00:00:00.000Z
related: []
bibtex: |
  @article{tang2024learning,
    title={Learning Chaotic Dynamics with Embedded Dissipativity},
    author={Tang, Sunbochen and Sapsis, Themistoklis P. and Azizan, Navid},
    journal={arXiv preprint arXiv:2410.00976},
    year={2024}
  }
sections:
- title: "Problem Formulation"
  md: |
    Many data-driven models for chaotic systems fail to produce bounded trajectories, which is a crucial prerequisite for generating reliable long-term statistics. The core challenge is to mitigate this instability, where models trained on limited data can drift outside the training region and diverge, especially given the error amplification inherent in chaotic systems. Our goal is to build a neural network emulator that generates bounded trajectories over long horizons to reliably reproduce the system's invariant statistics.
- title: "Method Overview"
  image: { src: /static/images/chaos-ode/PNAS_Main.png, alt: "Architecture enforcing dissipativity", caption: "Our framework learns a dynamics emulator and an energy function to construct a dissipative projection layer that guarantees trajectory boundedness." }
  md: |
    We introduce a modular framework that enforces dissipativity as a hard, mathematical constraint. The model simultaneously learns three components: an unconstrained neural network dynamics emulator, a quadratic energy-like (Lyapunov) function, and an energy level parameter . These are used to construct a "dissipative projection" layer. This layer modifies the output of the unconstrained emulator, projecting it into a subspace that guarantees the resulting dynamics are dissipative, ensuring trajectory boundedness.
- title: "Certified Boundedness"
  md: |
    Based on Lyapunov stability theory, we derive a computationally efficient, algebraic condition that guarantees dissipativity. The projection layer enforces this condition by solving a simple optimization problem that has a closed-form solution computable with a ReLU activation function. This certifies that the learned system is dissipative, and every trajectory is guaranteed to be bounded and converge to a learned invariant level set. As a secondary benefit, this learned level set provides a tight outer approximation of the system's strange attractor.
- title: "Experiments"
  image: { src: /static/images/chaos-ode/KS_spatiotemporal.png, alt: "Forecast accuracy plots", caption: "Comparison on a reduced-order Kuramoto–Sivashinsky model." }
  md: |
    We demonstrate our method on the Lorenz 63, Lorenz 96, and a 32-dimensional Kuramoto-Sivashinsky (KS) reduced-order model. While a standard multilayer perceptron (MLP) baseline generates unbounded trajectories that suffer from finite-time blow-ups, our constrained model produces stable, long-horizon forecasts that accurately preserve the systems' invariant statistics. Quantitative evaluation shows our model achieves significantly lower KL divergence on the attractor's distribution and lower relative error in the Fourier energy spectrum compared to the unconstrained baseline.
---

**Abstract.** Chaotic dynamics, commonly seen in weather systems and fluid turbulence, are characterized by their sensitivity to initial conditions, which makes accurate prediction challenging. Recent approaches have focused on developing data-driven models that preserve invariant statistics over long horizons since many chaotic systems observe dissipative behaviors and ergodicity. A crucial prerequisite for producing reliable statistics is that the model must generate bounded trajectories, a condition many models fail to guarantee, despite their empirical success. To address this fundamental challenge, we introduce a modular framework that enforces formal, provable guarantees of trajectory boundedness for neural network chaotic dynamics models. Our core contribution is a "dissipative projection" layer that leverages control-theoretic principles to ensure the learned system is dissipative. Specifically, our framework simultaneously learns a dynamics emulator and an energy-like function, where the latter is used to construct an algebraic dissipative constraint within the projection layer. A secondary benefit is that the learned invariant level set provides an outer estimate for the system's strange attractor, which is known to be very difficult to characterize due to its complex geometry. We demonstrate our model's ability to produce bounded long-horizon forecasts that preserve invariant statistics for chaotic dynamical systems including Lorenz 96 and a reduced-order model of the Kuramoto-Sivashinsky equation.