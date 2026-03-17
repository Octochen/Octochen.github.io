---
title: Research
date: 2023-03-07 22:37:41
---

-----------------------------------------------------------

#### Multi-sensor Fusion Estimation

Multi-sensor fusion estimation has attracted considerable research interest due to its broad applications, including target tracking, localization, environmental monitoring, and health monitoring. The primary objective of fusion estimation is to improve state estimation accuracy by integrating valuable information from multiple sensors. Our research focuses on the following aspects:

<center>
<img src="https://github.com/Octochen/Octochen.github.io/blob/hexo_academic-homepage/hexo_academiac-homepage/themes/Academia/source/img/Multi-sensor%20system.png?raw=true" width="40%" height="40%" title="A multi-sensor fusion system for target tracking">
</center>



1. **Distributed Zonotopic Fusion Estimation** [<font color=red>[PDF]</font>](/papers/P9_2026_Distributed Zonotopic Fusion Estimation for Multi-Sensor Systems.pdf): A key challenge in distributed fusion estimation lies in designing effective fusion criteria to consistently combine local sensor estimates while maximizing
   estimation accuracy. Existing fusion criteria predominantly assume Gaussian posterior estimates, yet real-world applications frequently encounter non-Gaussian noises with unknown statistical characteristics. Therefore, we propose zonotope fusion criteria for merging local zonotopic estimates into distributed zonotopic fusion estimates (DZFEs). The proposed DZFEs have better estimation performance than local zonotopic estimates and guarantee state inclusion property that ensures the real state is always within fusion estimates.

<center>
<img src="https://github.com/Octochen/Octochen.github.io/blob/hexo_academic-homepage/hexo_academiac-homepage/themes/Academia/source/img/Zonotopic%20fusion%20estimation.png?raw=true" width="50%" height="50%" title="Zonotopic fusion criteria and distributed zonotopic fusion estimates of a moving target">
</center>


2. **Privacy-preserving Distributed Estimation** [<font color=red>[PDF]</font>](/papers/P8_2025-07_Privacy-preserving distributed estimation for interconnected dynamic.pdf): Privacy concerns regarding weighted sum aggregation are inherent to distributed estimation, control, and optimization. To address these concerns, we propose a noise contamination mechanism for private matrix–vector multiplication and private weighted sum aggregation. Several conditions are established to ensure that the mechanism achieves complete confidentiality. Subsequently, we develop privacy-preserving distributed estimators for interconnected dynamic systems using the proposed aggregation schemes. Our analysis demonstrates that both subsystems and their distributed estimators achieve effective privacy protection.

<center>
<img src="https://github.com/Octochen/Octochen.github.io/blob/hexo_academic-homepage/hexo_academiac-homepage/themes/Academia/source/img/Privacy-preserving%20distributed%20estimation.png?raw=true" width="50%" height="50%" title="Zonotopic fusion criteria and distributed zonotopic fusion estimates of a moving target">
</center>