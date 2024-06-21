---
marp: true
theme: slides
size: 16:9
paginate: true
---

<!-- _paginate: false -->

<style scoped>
p {
    font-size: 24px;
}
</style>

# Statistical Connectomics

## Thesis Committee Meeting

<br>

### Jaewon Chung

_(he/him)_ - [NeuroData lab](https://neurodata.io/)
Johns Hopkins University
Department of Biomedical Engineering

![icon](../images/icons/mail.png) [_j1c@jhu.edu_](mailto:j1c@jhu.edu)
![icon](../images/icons/github.png) [_@j1c (Github)_](https://github.com/j1c)
![icon](../images/icons/twitter.png) [_@j1c (Twitter)_](https://twitter.com/j1c)

![bg right:45% w:450](../images/logos/nd_logo_small.png)

<!-- https://neurodata.io/talks/tathey1/23_06_12_thesis/pres.html#2 -->

---

# Outline

- What we've done

  - **Deriving Connectomes of Human Brains**
  - Statistical Modeling for Connectomes
  - Heritability of Human Connectomes
  - `graspologic` + `hyppo` + `m2g`

- Graduation plan

---

# Representing brains as networks

<div class="columns">
<div>
Networks (or graphs) are mathematical abstractions to represent relational data

- **Vertices** - the set of objects (brain regions)
- **Edges** - the set of connections between those objects (brain regions)
  - E.g. region 1 connects to region 2 with 100 neural bundles

</div>

<div>

![center h:500](../images/brain-network.png)

</div>
</div>

---

# Connectomes from diffusion MRI (dMRI)

- _in vivo_ imaging technique
- Exploits direction of water diffusion
  - Anisotropic in white matter tracts
  - Isotropic in other tissues
- Estimates of number of white matter tracts via tractography

![center h:275](./images/white-matter-tract-hori.jpeg)

---

# MRI to graphs (m2g)

<div class="columns">
<div>

- Easy to use end-to-end pipeline
  - Input: MRI data
  - Output: Connectomes, QA measures, derivatives
- Reproduces biological properties
  - Stronger ipsilateral connections
- High discriminability
  - Same subjects' connectomes are more similar than different subjects'

</div>

<div>

![center w:500](./images/m2g-structural.png)

<!-- ![center h:525](../images/fiber-tract-vert.jpeg) -->

</div>
</div>

<footer>

[Chung et al. "A low-resource reliable pipeline..." <i>In review, Nature Methods</i> (2024)](https://www.biorxiv.org/content/10.1101/2021.11.01.466686v2)

</footer>

---

# Outline

- What we've done

  - Connectomes of Human Brains
  - **Statistical Modeling for Connectomes**
  - Heritability of Human Connectomes
  - `graspologic` + `hyppo` + `m2g`

- Graduation plan

---

# Different data, same statistics (Ascombe's Quartet)

- These four datasets have same statistics!

![center w:650](../images/ascombes.png)

---

# Different networks, same statistics

- These four networks have same (graph) statistics!

<br>
<br>

![center w:750](../images/ten-node-graphs.gif)

<footer>

[Chung et al. "Statistical connectomics." <i>Annual Review of Statistics and Its Application</i> (2021)](https://www.annualreviews.org/content/journals/10.1146/annurev-statistics-042720-023234)

</footer>

---

# Statistical models for networks

- Random dot product graphs (RDPGs)
  - Each vertex has a low $d$ dimensional latent position.
  - Estimate latent position matrix $X$ via adjacency spectral embedding.
  - $P[i\rightarrow j]$ = $\langle x_i, x_j\rangle$

![center h:300](./images/ase.png)

<!--
<footer>

Athreya et al. "RDPG..." _JMLR_ (2021)

</footer> -->

---

# Two sample graph testing

<div class="columns">

<div>

- Suppose we have two networks
- Want to test if they are "same" or not

Hypothesis:

- $H_0: F($<span style="color: var(--network1)">Network 1</span>$) = F($<span style="color: var(--network2)">Network 2</span>$)$
- $H_A: F($<span style="color: var(--network1)">Network 1</span>$) \neq F($<span style="color: var(--network2)">Network 2</span>$)$

More precisely:

- $H_0: F_X = F_Y \circ W$
- $H_A: F_X \neq F_Y \circ W$

</div>
<div>

###### Drosophila Left vs Right Brain

![center w:450](./images/nonpar.png)

</div>

</div>

<footer>

[Chung et al. "Valid two-sample graph testing..." <i>Stat</i> (2022)](https://doi.org/10.1002/sta4.429)

</footer>

---

# Outline

- What we've done

  - Connectomes of Human Brains
  - Statistical Modeling for Connectomes
  - **Heritability of Human Connectomes**
  - `graspologic` + `hyppo` + `m2g`

- Graduation plan

---

# Heritability of connectomes?

- Heritability = proportion of phenotypic variance due to genetic variance
  - Predict disease rick
  - Potential for targeted treatments
  - Genes -> structure -> function -> behavior

---

# Heritability as causal problem

![center h:460](../images/heritability/dag.png)

<footer>

[Chung et al. "Are human connectomes heritable?" <i>In prep, Imaging Neuroscience</i> (2024)](https://www.biorxiv.org/content/10.1101/2023.04.02.532875v3)

</footer>

---

# Do <span style="color: var(--genome)">genomes</span> affect <span style="color: var(--connectome)">connectomes</span>?

<div class="columns">

<div>

- Our hypothesis:
  $H_0: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>$) = F($<span style="color: var(--connectome)">C</span>$)F($<span style="color: var(--genome)">G</span>$)$
  $H_A: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>$) \neq F($<span style="color: var(--connectome)">C</span>$)F($<span style="color: var(--genome)">G</span>$)$

- Known as independence testing
- Test statistic: _distance correlation (Dcorr)_
- Implication if false: there exists an **associational** heritability.

</div>

<div>

<br>
<br>

![center](./images/associational.png)

</div>

</div>

---

# Do <span style="color: var(--genome)">genomes</span> affect <span style="color: var(--connectome)">connectomes</span> given <span style="color: var(--neuroanatomy)">covariates</span>?

<div class="columns">
<div>

- Want to test:
  $H_0: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) =
  F($<span style="color: var(--connectome)">C</span>|<span style="color: var(--neuroanatomy)">Co</span>$) F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$
  $H_A: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) \neq F($<span style="color: var(--connectome)">C</span>|<span style="color: var(--neuroanatomy)">Co</span>$)F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$
- Known as conditional independence test
- Test statistic: Conditional distance correlation (CDcorr)
- Implication if false: there exists causal dependence of connectomes on genomes.
</div>

<div>

![center](./images/conditional.png)

</div>

</div>

---

# Human Connectome Project

- Brain scans from identical (monozygotic), fraternal (dizygotic), non-twin siblings.
- Regions defined using Glasser parcellation (180 regions).

<br>

![center w:700](./images/hcp_demographics.svg)

<footer>
Van Essen, David C., et al., The WU-Minn human connectome project: an overview (2013)

Glasser, Matthew F., et al. "A multi-modal parcellation of human cerebral cortex." Nature (2016).

</footer>

---

# Methods of comparing connectomes

- Exact : measures all differences in latent positions
  - Differences in the latent positions implying differences in the connectomes themselves
- Global : considers the latent positions of one connectome are a scaled version of the other
  - E.g. males may have globally fewer connections than females
- Vertex : similar to the global differences, but it allows for each vertex to be scaled differently
  - E.g regions have preferences in connections
  - regions tend to connect strongly within hemisphere

---

# We see stochastic ordering along familial relationships

<div class="columns">

<div>

Connectome Models
![center h:450](./images/hist-plot-vert.png)

</div>

<div>

Neuroanatomy

![center h:150](./images/hist-plot-neuro-vert.png)

</div>

</div>

![center h:75](./images/legend.png)

---

# We detect heritability (associational)

![center w:700](./images/associationa-tests.png)

---

# Some signals disappear after conditioning

![center w:700](./images/all-tests.png)

---

# To sum up...

![center h:250](./images/genome_to_connectome.png)

<!-- - Causal models = rigorous, interpretab -->

- Statistical models = nuanced investigations
- Connectomes are dependent on genome, up to some common structures.

---

# Outline

- What we've done

  - Connectomes of Human Brains
  - Statistical Modeling for Connectomes
  - Heritability of Human Connectomes
  - **`graspologic` + `hyppo` + `m2g`**

- Graduation plan

---

## How to use these tools?

<div class="columns">
<div>

## [graspologic](https://github.com/microsoft/graspologic)

[![h:30](https://pepy.tech/badge/graspologic)](https://pepy.tech/project/graspologic)
[![h:30](https://img.shields.io/github/stars/microsoft/graspologic?style=social)](https://github.com/microsoft/graspologic)
[![h:30](https://img.shields.io/github/contributors/microsoft/graspologic)](https://github.com/microsoft/graspologic/graphs/contributors)

<br><br>

![w:450](../images/logos/graspologic-logo.svg)

</div>

<div>

## [hyppo](https://github.com/neurodata/hyppo)

[![h:30](https://pepy.tech/badge/hyppo)](https://pepy.tech/project/hyppo)
[![h:30](https://img.shields.io/github/stars/neurodata/hyppo?style=social)](https://github.com/neurodata/hyppo)
[![h:30](https://img.shields.io/github/contributors/neurodata/hyppo)](https://github.com/neurodata/hyppo/graphs/contributors)

![w:450](../images/logos/hyppo.jpeg)

</div>

<div>

## [m2g](https://github.com/neurodata/m2g)

[![h:30](https://pepy.tech/badge/m2g)](https://pepy.tech/project/m2g)
[![h:30](https://img.shields.io/github/stars/neurodata/m2g?style=social)](https://github.com/neurodata/m2g)
[![h:30](https://img.shields.io/github/contributors/neurodata/m2g)](https://github.com/neurodata/m2g/graphs/contributors)

<!-- ![w:450](../images/logos/brain-logo.jpeg) -->

</div>

</div>

---

# Outline

- What we've done

  - Connectomes of Human Brains
  - Statistical Modeling for Connectomes
  - Heritability of Human Connectomes
  - `graspologic` + `hyppo`

- **Graduation plan**

---

# Summary of work so far

<style scoped>

ul,p {
    font-size: 23px;
}
</style>

<div class="columns">
<div>

#### Manuscripts

- (Co)-First author
  - Heritability, in review at _Imaging Neuro_ (2024)
  - m2g, in review at _Nature Methods_ (2024)
  - Two-sample graph testing, _Stat_ (2022)
  - Statistical Connectomics, _ARISA_ (2021)
  - `graspologic`, _JMLR_ (2019)
- Second author
  - Indep. Testing in Time Series, _TMLR_ (2024)
  - Causal Conditional DCorr, _in review_ (2023)
  - Multiscale Connectomics, _in review_ (2023)
- Others
  - 5 others published

</div>
<div>

#### Conference Presentations

- OHBM (x3)
- SfN (x3)
- Neuromatch (x2)
<!-- - NeurIPS Workshop (x1) -->

#### Invited Lectures & Talks

- JSM, 2023
- Advanced Graph Analytics Workshop (JHU), 2023
- OHBM, 2019

#### Awards

- BRAIN Initiative Trainee Highlight Award
- AWS Research Credit Grants (x2)

</div>
</div>

---

# Summary of work to be done

<style scoped>

ul,p {
    font-size: 26px;
}
</style>

<div class="columns">
<div>

#### Manuscripts

- Respond to reviews
- Collaboration with Child Mind Institute
<!-- - Collaboration with Alex Badea -->

#### Conferences/Talks

- Collaborative Research in Computational Neuroscience (CRCNS)
- Advanced Graph Analytics Workshop (JHU), 2024

</div>
<div>

#### Code

- Continue to develop `graspologic` and `hyppo`

</div>
</div>

<style scoped>
h2 {
    justify-content: center;
    text-align: center;
}
</style>

<br>

## Graduation $\approx$ May 2024

---

# Acknowledgements

#### Team

<style scoped>

p {
    font-size: 24px;
}
</style>

<div class='minipanels'>

<div>

![person](../images/faces/ebridge.jpg)
Eric Bridgeford

</div>

<div>

![person](../images/faces/pedigo.jpg)
Ben Pedigo

</div>

<div>

![person](../images/faces/pisner.jpg)
Derek Pisner

</div>

<div>

![person](../images/faces/cencheng.jpg)
Cencheng Shen

</div>

<div>

![person](../images/faces/ronak.jpeg)
Ronak Mehta

</div>

<div>

![person](../images/faces/vivek.jpg)
Vivek Gopalakrishnan

</div>

<div>

![person](../images/faces/powell.jpg)
Mike Powell

</div>

<div>

![person](../images/faces/cep.png)
Carey Priebe

</div>

<div>

![person](../images/faces/jovo.png)
Joshua Vogelstein

</div>

</div>

NeuroData lab, Microsoft Research

---

# Feedback?

<span> </span>
<span> </span>
<span> </span>
<span> </span>

<style scoped>
section {
    justify-content: center;
    text-align: center;
}
</style>

### Jaewon Chung

![icon](../images/icons/mail.png) [j1c@jhu.edu](mailto:j1c@jhu.edu)
![icon](../images/icons/github.png) [@j1c (Github)](https://github.com/j1c)
![icon](../images/icons/web.png) [j1c.org](https://j1c.org/)

---

<!-- paginate: skip -->

# Appendix

---

# How do we compare genomes?

- Neuroimaging twin studies do not sequence genomes.
- Coefficient of kinship ($\phi_{ij}$)
  - Probabilities of finding a particular gene at a particular location.
- d(<span style="color: var(--genome)">Genome</span>$_i$, <span style="color: var(--genome)">Genome</span>$_j$) = 1 - 2$\phi_{ij}$.

<br>
<center>

|   Relationship    |  $\phi_{ij}$  | $1-2\phi_{ij}$ |
| :---------------: | :-----------: | :------------: |
|    Monozygotic    | $\frac{1}{2}$ |      $0$       |
|     Dizygotic     | $\frac{1}{4}$ | $\frac{1}{2}$  |
| Non-twin siblings | $\frac{1}{4}$ | $\frac{1}{2}$  |
|     Unrelated     |      $0$      |      $1$       |

</center>

---

# Neuroanatomy (mediator), Age (confounder)

- Literature show:
  - neuroanatomy (e.g. brain volume) is highly heritable.
  - age affects genomes and potentially connectomes
- d(Covariates$_i$, Covariates$_j$) = ||Covariates$_i$ - Covariates$_j$||$_F$

---

# How do we compare connectomes?

- Random dot product graph (RDPG)

  - Each vertex (region of interest) has a low $d$ dimensional latent vector (position).
  - Estimate latent position matrix $X$ via adjacency spectral embedding.
  <!-- - $P[i\rightarrow j]$ = $\langle x_i, x_j\rangle$ -->

- d(<span style="color: var(--connectome)">Connectome</span>$_k$, <span style="color: var(--connectome)">Connectome</span>$_l$) = $||X^{(k)} - X^{(l)}R||_F$

---

# Distance correlation

- Measures dependence between two _multivariate_ quantities.
  - For example: connectomes, genomes.
- Can detect nonlinear associations.
- Measures correlation between pairwise distances.

![center w:800](./images/unconditional_test.png)

---

# Conditional distance correlation

- Augment distance correlation procedure with third distance matrix.

<br>

![center h:350](./images/conditional_test.png)

---

# Associational Test for Connectomic Heritability

- $H_0: F($<span style="color: var(--connectome)">Connectome</span>, <span style="color: var(--genome)">Genome</span>$) = F($<span style="color: var(--connectome)">Connectome</span>$)F($<span style="color: var(--genome)">Genome</span>$)$
  $H_A: F($<span style="color: var(--connectome)">Connectome</span>, <span style="color: var(--genome)">Genome</span>$) \neq F($<span style="color: var(--connectome)">Connectome</span>$)F($<span style="color: var(--genome)">Genome</span>$)$

![center h:205](./images/hist-plot-connectomes.png)

<br>

<center>

|   Sex   |      **All**      |    **Females**    |     **Males**     |
| :-----: | :---------------: | :---------------: | :---------------: |
| p-value | $<1\times10^{-5}$ | $<1\times10^{-3}$ | $<1\times10^{-2}$ |

</center>

---

# Associational Test for Neuroanatomy

- $H_0: F($<span style="color: var(--neuroanatomy)">Neuroanatomy</span>, <span style="color: var(--genome)">Genome</span>$) = F($<span style="color: var(--neuroanatomy)">Neuroanatomy</span>$)F($<span style="color: var(--genome)">Genome</span>$)$
  $H_A: F($<span style="color: var(--neuroanatomy)">Neuroanatomy</span>, <span style="color: var(--genome)">Genome</span>$) \neq F($<span style="color: var(--neuroanatomy)">Neuroanatomy</span>$)F($<span style="color: var(--genome)">Genome</span>$)$

![center h:205](./images/hist-plot-neuroanatomy.png)

<br>

<center>

|   Sex   |      **All**      |    **Females**    |     **Males**     |
| :-----: | :---------------: | :---------------: | :---------------: |
| p-value | $<1\times10^{-3}$ | $<1\times10^{-2}$ | $<1\times10^{-2}$ |

</center>

---

# Causal Test for Connectomic Heritability

- $H_0: F($<span style="color: var(--connectome)">Conn.</span>, <span style="color: var(--genome)">Genome</span>|Covariates$) = F($<span style="color: var(--connectome)">Conn.</span>|Covariates$)F($<span style="color: var(--genome)">Genome</span>|Covariates$)$
  $H_A: F($<span style="color: var(--connectome)">Conn.</span>, <span style="color: var(--genome)">Genome</span>|Covariates$) \neq F($<span style="color: var(--connectome)">Conn.</span>|Covariates$)F($<span style="color: var(--genome)">Genome</span>|Covariates$)$

<br>

<center>

|   Sex   |      **All**      |    **Females**    |     **Males**     |
| :-----: | :---------------: | :---------------: | :---------------: |
| p-value | $<1\times10^{-2}$ | $<1\times10^{-2}$ | $<1\times10^{-2}$ |

</center>