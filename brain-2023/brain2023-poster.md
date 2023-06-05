---
marp: true
theme: poster
paginate: false
size: 48:40
math: katex
---

<!-- Start header -->
<div class="header">

<!-- Image in the upper left -->
<div>

![headerlogo](../images/logos/hopkins-logo.png)

</div>

<!-- Title and author information -->
<div>

# The Heritability of Human Connectomes: a Causal Modeling Analysis

## Jaewon Chung<span class=super>1\*</span>, Eric Bridgeford<span class=super>1</span>, Michael Powell<span class=super>2</span>, Derek Pisner <span class=super>3</span>, Joshua T. Vogelstein<span class=super>1</span>

##### 1 - Johns Hopkins University, 2 - United States Military Academy, 3 - Independent Researcher, $\ast$ - correspondence: ![icon](../images/icons/mail.png) [_j1c@jhu.edu_](mailto:j1c@jhu.edu) ![icon](../images/icons/github.png) [_@j1c(Github)_](https://github.com/j1c) ![icon](../images/icons/twitter.png) [_@j1chung(Twitter)_](https://twitter.com/j1chung)

</div>

<!-- Image on the upper right -->
<div>

![headerlogo](../images/logos/nd_logo.png)

<!-- ![headerlogo](./DEI-icon.png) -->

</div>

<!-- End header -->
</div>

<!-- Summary box title -->

<span class='h3-noline'> Summary </span>

<!-- Summary box using 5 columns-->
<div class='box'>
<div class="columns-box">

<!-- Box col1 -->
<div>

- Aimed to define heritability for populations of connectomes using statistical modelling.

</div>
<div>

- Structural connectomes are heritable without controlling for neuroanatomy.
- Neuroanatomy is also highly heritable

</div>
<div>

- Connectomes remain heritable after controlling for effects of neuroanatomy on connectomes.

</div>
<div>

- Provide tools for future analysis on populations of connectomes.

</div>

<!-- End columns-box -->
</div>
<!-- End box -->
</div>

<!-- Start main 2 column split for poster -->
<div class="columns-main">

<!-- Start main column 1 -->
<div>

### Motivation

- Understanding how brain connectivity is influenced by genetics can improve our understanding of brain function and diseases.
- Current methods of analyzing connectomes or hertability exhibit limitations:
  - Selection Graph theoretic features
  - Multivariate normality assumptions

### Overview of Analysis

<!-- Big question for this work -->

![center](../images/heritability/framework.png)
**Fig 1:** Overview of the framework for measuring heritability of connectomes.

<br>

## Do <span style="color:var(--genome)"> genomes </span> cause <span style="color:var(--connectome)">connectomes</span>?

<br>

### Causal Analysis of Effect of Genome on Connectomes

- Genome directly affects the structural connectome.
- Neuroanatomy (e.g. brain volume) indirectly affects the connectome.
- Participant history, such as the shared and non-shared environmental influences, and traits are potential confounders.
- The shared and non-shared environment is controlled by comparing between the same sex individuals.

![center h:800](../images/heritability/dag.png)
**Fig 2:** Directed acyclic graph (DAG) illustrating potential relationships between the genome and connectome.

<!-- End main column 1 -->
</div>

<!-- Start main column 2 -->
<div>

### Structural Connectomes from Diffusion MRI

![center w:1500](../images/heritability/data-plot.png)
**Fig 3:** Visualization of connectomes as adjacency matrices using the projected Desikan parcellation with hemispheric labels. **(A)** Average connectome of all subjects with log-transformed edge weights. **(B)** Absolute difference of connectomes from the most different pair of subjects with log-transformed edge weights.

<br>

### New title

![center w:1500](../images/heritability/Desikan-composite-a.png)
**Fig 3:** Visualization of pairwise distances of connectomes and neuroanatomy. Diamonds represent the median. Median distances grow as genetic distances increase.

<br>

### New title

![](../images/heritability/Desikan-composite-b.png)
**Fig 4:** Testing for associational heritability of connectomes and neuroanatomy. Red squares indicate significant tests; blue indicate non-significant tests.

<!-- End main column 2 -->
</div>

<!-- Start main column 3 -->
<div>

### Human Connectome Project 1200

- Structural connectomes are estimated using structural (sMRI) and diffusion magnetic resonance imaging (dMRI).

|            | Monozygotic  |  Dizygotic  | Non-twin siblings |
| :--------: | :----------: | :---------: | :---------------: |
|     N      |     322      |     212     |        490        |
|    Sex     | 196 F, 126 M | 125 F, 87 M |   237 F, 253 M    |
| Age (mean) |  29.6 (3.3)  | 28.9 (3.4)  |    28.3 (3.9)     |

<div align="center">

**Table 1:** Participants and their demographics of HCP1200 Dataset.

</div>

### Three Models of Connectomes

- **Exact:** Are the model parameters of connectomes the same?
- **Global scale:** Are the model parameters same after considering global scaling?
- **Vertex scale:** Are the model parameters same after considering vertex wise scaling?

![center h:1000](../images/heritability/3-simulations.png)
**Fig 3:** Examples of the three different models (exact, global scale, and vertex scale) of connectome heritability visualized as adjacency matrices. Networks are sampled from stochastic block models (SBMs) with different block probabilities.

<br>

### Limitations and extensions

- Potential confounders that are not considered.
- Other staitsical models to consider (e.g. COSIE [3]).
- Repeated analysis on functional MRI or in other twin study datasets.

<!-- Code/Refs/Thanks/Funding - small section -->

###

<div class="columns2">
<div>

#### Code

<div class="columns3-np">
<div>

<!-- Logo for a package -->

![left h:1in](../images/logos/graspologic-logo.svg)

</div>
<div>

<!-- Badges for a package -->

[![h:.4in](https://pepy.tech/badge/graspologic)](https://pepy.tech/project/graspologic)
[![h:.4in](https://img.shields.io/github/stars/microsoft/graspologic?style=social)](https://github.com/microsoft/graspologic)

</div>
<div>

<!-- QR code to a package -->

![center h:1in](../images/qr/graspologic-qr.svg)

</div>
</div>

<div class="columns3-np">
<div>

<!-- Logo for a package -->

<p style="text-align: center;">

**hyppo**

</p>

</div>
<div>

<!-- Badges for a package -->

[![h:.4in](https://pepy.tech/badge/hyppo)](https://pepy.tech/project/hyppo)
[![h:.4in](https://img.shields.io/github/stars/neurodata/hyppo?style=social)](https://github.com/neurodata/hyppo)

</div>
<div>

<!-- QR code to a package -->

![center h:1in](../images/qr/hyppo-qr.svg)

</div>
</div>

<br>

#### Acknowledgements

<footer>
NeuroData lab for many ideas and feedback. Many at Microsoft Research for w/ graspologic.
</footer>

</div>
<div>

#### References

<!-- Need these breaks <br> between refs otherwise formatting breaks for some reason -->
<footer>
[1] Chung et al. "The Heritability of Human Connectomes: a Causal Modeling Analysis," In bioRxiv (2023)
<br>
[2] Chung et al. "Statistical connectomics," Ann. Rev. Statistics and its Application (2021)
<br>
[3] Arroyo et al. "Inference for multiple heterogeneous networks with a common invariant subspace," JMLR (2021)
</footer>

#### Funding

<footer>
J.C. supported by the BRAIN Initiative (1RF1MH123233). J.T.V. supported by NSF CAREER Award (1942963). Findings and conclusions expressed are  those of the authors and not necessarily those of the funders.
</footer>

</div>
</div>

<!-- End main column 2 -->
</div>

<!-- End main columns -->
</div>
