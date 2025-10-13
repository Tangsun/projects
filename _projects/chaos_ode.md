---
title: "Learning Dissipative Chaotic Dynamics with Boundedness Guarantee"
description: "One-sentence 150–160 character summary of your contribution and findings."
authors:
  - { name: "Sunbochen Tang", url: "https://https://tangsun.github.io"}
  - { name: "Themistoklis Sapsis", url: "https://sandlab.mit.edu/about/" }
  - { name: "Navid Azizan", url: "https://azizan.mit.edu/index.html"}
affiliation: "Massachusetts Institute of Technology"
venue: "Preprint"          # or "NeurIPS 2025 (to appear)"
equal_contrib: false
year: 2024
arxiv: 2410.00976          # or full abs URL, or omit
pdf: /static/pdfs/chaos_ode.pdf
# supplementary: /static/pdfs/chaos_learning_supp.pdf
# code: "Coming Soon"
social_image: /static/images/chaos-learning/social_preview.png
published_time: 2025-06-01T00:00:00.000Z
poster: /static/pdfs/chaos_ode_poster.pdf
keywords: [chaos, dynamical systems, forecasting, machine learning, time series]
# carousel_images:
#   - { src: /static/images/chaos-learning/fig1.jpg, alt: "Lorenz attractor predictions", caption: "Forecasting on Lorenz system." }
#   - { src: /static/images/chaos-learning/fig2.jpg, alt: "Error vs horizon", caption: "Error vs. horizon." }

related: []                # optional curated list of other project slugs
bibtex: |
  @article{tang2024learning,
  title={Learning chaotic dynamics with embedded dissipativity},
  author={Tang, Sunbochen and Sapsis, Themistoklis and Azizan, Navid},
  journal={arXiv preprint arXiv:2410.00976},
  year={2024}
  }

sections:
- title: "Method Overview"
  image: { src: /static/images/chaos-ode/method.png, alt: "Method diagram", caption: "Our architecture and losses." }
  md: |
    We learn a one-step operator with a stabilizer ensuring boundedness…
- title: "Results"
  image: { src: /static/images/chaos-ode/results.png, alt: "Results" }
  md: |
    We compare long-horizon forecasts on Lorenz-63 and … achieving lower NRMSE.

---

**Abstract.** Chaotic dynamics, commonly seen in weather systems and fluid turbulence, are characterized by their sensitivity to initial conditions, which makes accurate prediction challenging. Recent approaches have been focused on developing data-driven models that preserve invariant statistics over long horizons since many chaotic systems observe dissipative behaviors and ergodicity. Although these methods have shown empirical success, many of the models are still prone to generating unbounded trajectories, leading to invalid statistics evaluation. In this paper, we propose a novel neural network architecture that simultaneously learns a dissipative dynamics emulator that guarantees to generate bounded trajectories and an energy-like function that governs the dissipative behavior. More specifically, by leveraging control-theoretic ideas, we derive algebraic conditions based on the learned energy-like function that ensure asymptotic convergence to an invariant level set. Using these algebraic conditions, our proposed model enforces dissipativity through a ReLU projection layer, which provides formal trajectory boundedness guarantees. Furthermore, the invariant level set provides an outer estimate for the strange attractor, which is known to be very difficult to characterize due to its complex geometry. We demonstrate the capability of our model in producing bounded long-horizon trajectory forecasts that preserve invariant statistics and characterizing the attractor, for chaotic dynamical systems including Lorenz 96 and a reduced-order model of the Kuramoto-Sivashinsky equation.
