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

# Statistical Connectomics: Developing Methods Towards Understanding Populations of Networks

<br>

### Jaewon Chung

_(he/him)_ - [NeuroData lab](https://neurodata.io/)
Johns Hopkins University
Department of Biomedical Engineering

![icon](../images/icons/mail.png) [_j1c@jhu.edu_](mailto:j1c@jhu.edu)
![icon](../images/icons/github.png) [_@j1c (Github)_](https://github.com/j1c)
![icon](../images/icons/twitter.png) [_@j1c (Twitter)_](https://twitter.com/j1c)

![bg right:45% w:450](../images/logos/nd_logo_small.png)

---

<!-- before i get into the bulk of the talk, i want to steal a page from previous lab members defenses, and start my defense with the acknowledgements. That way if you glaze over or fall asleep later in the talk, I hope you'll remember the important part, which is my graditute to the people which I should probably express more often. -->

# Acknowledgements

---

<!-- First, to my advisor, my committee, and close collaborators. I will be forever humbled that you all trusted me to work on data and problems that you all have spent so much time and energy on. I'm grateful for that opportunity and for all I've learned from you over the years, and I'm confident that we'll keep working together for a long while... -->

# Committee

<style scoped>

p {
    font-size: 24px;
}
</style>


<div class='columns'>
<div>
<div class='minipanels'>
<div>

![person](../images/faces/jovo.png)
Joshua Vogelstein

</div>
<div>

![person](../images/faces/cep.png)
Carey Priebe

</div>
<div>

![person](../images/faces/powell.jpg)
Mike Powell

</div>
</div>

## Collaborators

<div class='minipanels'>
<div>

![person](../images/faces/badea.jpeg)
Alex B.

</div>
<div>

![person](../images/faces/ebridge.jpg)
Eric B.

</div>
<div>

![person](../images/faces/pisner.jpg)
Derek P.

</div>
<div>

![person](../images/faces/cencheng.jpg)
Cencheng S.

</div>
<div>

![person](../images/faces/ronak.jpeg)
Ronak M.

</div>
</div>

<div>

![bg right:45% w:450](../images/logos/nd_logo_small.png)

</div>
</div>

---

<!-- I want to thank many current and past members of the neurodata lab and hopkins. It has been a great honor to get to learn from you all on a daily basis, and not just about machine learning or neuroscience or statistics, but also frisbee -->

<style scoped>

p {
    font-size: 15px;
}

.minipanels {
  display: grid;
  text-align: center;
  grid-template-columns: repeat(9, 80px);
  gap: 0.0rem;
  margin: 0px;
  border: 0px;
  pad: 0px;
  align: left;
}

</style>

<div class="columns-bl">
<div>


<div class='minipanels'>
<div>

![person](https://raw.githubusercontent.com/neurodata/neurodata.io/deploy/source/images/people/alex_loftus.jpg)
Alex

<!-- Loftus -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ali_saad.jpg?raw=true)
Ali

<!-- Saad-Eldin -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/alice_wang.jpg?raw=true)
Alice

<!-- Wang -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/anton_alyakin.jpg?raw=true)
Anton

<!-- ... -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ashwin_headshot.jpg?raw=true)
Ashwin

<!-- ... -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/bear.jpg?raw=true)
Bear

<!-- ... -->

</div>

<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/falk_ben.jpg?raw=true)
Ben 1

<!-- Falk -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/pedigo.jpg?raw=true)
Ben 2

<!-- ... -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/bijan.jpg?raw=true)
Bijan

<!-- ... -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/brandon_duderstadt.jpg?raw=true)
Brandon

<!-- ... -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/devin-crowley.jpg?raw=true)
Devin

<!-- Crowley -->

</div>

<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/drishti.jpg?raw=true)
Drishti

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/bridgeford.jpg?raw=true)
Eric

<!-- Bridgeford -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/hao.jpg?raw=true)
Hao

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/hayden-helm.jpg?raw=true)
Hayden

<!-- Helm -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/javier_how.jpg?raw=true)
Javier

<!-- How -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/jayanta.jpg?raw=true)
Jayanta

<!-- Dey -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/jesus.jpg?raw=true)
Jesus

<!-- Arroyo -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/jong_shin.png?raw=true)
Jong

<!-- Shin -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/kareef_ullah.jpg?raw=true)
Kareef

<!-- Ullah -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/patsolic_jesse.jpg?raw=true)
Jesse

<!-- Patsolic -->

</div>

<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ronak_mehta.jpg?raw=true)
Ronak

<!-- Mehta -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ronan.jpg?raw=true)
Ronan

<!-- Perry -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ross-lawrence.jpg?raw=true)
Ross

<!-- Lawrence -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/sambit-panda.jpg?raw=true)
Sambit

<!-- Panda -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ogihara_suki.jpg?raw=true)
Suki

<!-- Panda -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/tingshan.png?raw=true)
Tingshan

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/tomita_tyler.jpg?raw=true)
Tyler

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/tommy_athey.jpg?raw=true)
Tommy

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/vikram.jpg?raw=true)
Vikram

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/vivek.jpg?raw=true)
Vivek

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/yuxin.jpg?raw=true)
Yuxin

<!-- Bai -->

</div>
<div>

![person](https://github.com/neurodata/neurodata.io/blob/deploy/source/images/people/ziyan.png?raw=true)
Ziyan

</div>
</div>


</div>
<div>

![](../images/nd-photo.jpg)
![](../images/nd-photo2.jpg)

</div>
</div>

---

<!-- To my parents and my brother - I obviously owe them everything that got me to this point. Their unwavering support, encouragement, and love have been the foundation of my journey. -->

![center w:1400](./images/family.jpeg)


---

<!-- To my partner Lina. Im so grateful for that support and that we've made it through this chapter stronger and with so many great memories, and i cant wait to see what the future holds for us in the future. -->


![center w:1400](./images/lina.jpeg)


---

# Outline

- **Connectomes of Human Brains**
- Statistical Modeling for Connectomes
- Heritability of Human Connectomes
- Open-source Software



---

# Connectomes: maps of neural wiring

<div class='columns'>

<div>

- Brains contain **neurons**, which carry information via electrical signals
- Neurons connect to each other via **synapses**, allowing neurons to "talk" to each other
- **Connectome** is a map of the structure of neurons and the synapses between them
    - Shaped by evolution, experience, influences neural activity, behavior

</div>

<div>

![center w:500](../images/neuron-synapse.png)

</div>

</div>

<footer>

Pedigo et al.

</footer>

---


# How do we measure connectomes in humans?

- Diffusion MRI (dMRI): _in vivo_ imaging technique
- Exploits direction of water diffusion
  - Anisotropic in white matter tracts
  - Isotropic in other tissues

![center w:800](../images/nerve-bundle-diagram-horizontal.png)

---


<br>
<br>
<br>

<div class='columns'>
<div>

### MRI Scans

<br>

![center w:300](../images/mri.png)

</div>
<div>

### Preprocessing

![center w:500](../images/mri-processing.png)

</div>

<div>

### Tractography

![center w:500](../images/tractography-gif.gif)


</div>
</div>

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

# Connectomes: maps of neural wiring

![center h:500](./images/why1.png)

<footer>
Images from SciDraw
</footer>

---

# Linking connectivity to other phenotypes

![center h:500](./images/why2.png)

<footer>
Images from SciDraw
</footer>

---

# Linking connectivity to other phenotypes

![center h:500](./images/why3.png)

<footer>
Images from SciDraw
</footer>

---

<!-- Brain diseases disrupt communication between brain regions. This is why studying connectivity can help us develop targeted therapies for diseases like Alzheimer's and Parkinson's. -->

# Linking connectivity to other phenotypes

![center h:500](./images/why4.png)

<footer>
Images from SciDraw
</footer>

---

# Outline

- Connectomes of Human Brains
- **Statistical Modeling for Connectomes**
- Heritability of Human Connectomes
- Open-source Software


---

# Different data, same statistics (Ascombe's Quartet)

<div class="columns">
<div>

- These four datasets have same statistics!
    - Mean ($\bar x$): 9
    - Variance ($s^2_x$): 11
    - Mean ($\bar y$): 7.5
    - Variance ($s^2_y$): 4.12
    - Correlation ($\rho_{xy}$):0.816


</div>

<div>

<br>

![center w:650](../images/ascombes.png)

<footer>

[Wikipedia - Ascombe's Quartet](https://en.wikipedia.org/wiki/Anscombe's_quartet)

</footer>

</div>

</div>


---

# Different networks, same statistics

- These four networks have same (network) statistics!

<br>


![center w:800](../images/ten-node-graphs.gif)

<footer>

[Chung et al. "Statistical connectomics." <i>Annual Review of Statistics and Its Application</i> (2021)](https://www.annualreviews.org/content/journals/10.1146/annurev-statistics-042720-023234)

</footer>


---

# Show the other figure of the same statistics

- Consider all non-isomorphic graphs with 10 vertices


![center w:800](../images/network-stat-dists.gif)


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

- Connectomes of Human Brains
- Statistical Modeling for Connectomes
- **Heritability of Human Connectomes**
- Open-source Software


---

# Heritability?

<div class='columns'>

<div>

- Proportion of phenotypic variance due to genetic variance
  - Predict disease risk
  - Potential for targeted treatments

- **Do genomes cause connectomes?**

</div>

<div>

<br>
<br>


![center h:250](./images/genome_to_connectome.png)

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

# Heritability as causal problem

![center h:460](../images/heritability/dag.png)

<footer>

[Chung et al. "Are human connectomes heritable?" <i>In prep, Imaging Neuroscience</i> (2024)](https://www.biorxiv.org/content/10.1101/2023.04.02.532875v3)

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


# Distribution of distances between connectomes

<div class="columns">

<div>

- Stochastic ordering along familial relationships
- Monozygotic twins have the smallest distances
- Medians (diamonds) shift towards the right as relatedness decreases
- Shifts in medians "decrease" in vertex model

</div>

<div>

![center h:525](./images/hist-plot-connectomes-vert.png)

</div>

</div>

<!-- ![center h:75](./images/legend.png) -->

---

# Do <span style="color: var(--genome)">genomes</span> affect <span style="color: var(--connectome)">connectomes</span>?

<div class="columns">

<div>

- Our hypothesis:
  $H_0: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>$) = F($<span style="color: var(--connectome)">C</span>$)F($<span style="color: var(--genome)">G</span>$)$
  $H_A: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>$) \neq F($<span style="color: var(--connectome)">C</span>$)F($<span style="color: var(--genome)">G</span>$)$

- Known as independence testing
- Test statistic: _distance correlation (Dcorr)_
- p-value: "If genomes don't affect connectomes, what is the probability there is **associational** correlation?"

</div>

<div>

<br>
<br>

![center](./images/associational.png)

</div>
</div>

---

# <span style="color: var(--genome)">Genomes</span> affect <span style="color: var(--connectome)">connectomes</span>

<div class="columns">

<div>

- Our hypothesis:
  $H_0: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>$) = F($<span style="color: var(--connectome)">C</span>$)F($<span style="color: var(--genome)">G</span>$)$
  $H_A: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>$) \neq F($<span style="color: var(--connectome)">C</span>$)F($<span style="color: var(--genome)">G</span>$)$

- p-value: "If genomes don't affect connectomes, what is the probability there is **associational** correlation?"
- All p-values $<10^{-3}$

</div>
<div>

<br>


![center w:550](./images/associational-pvals.png)

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
- p-value: "If genomes don't affect connectomes, what is the probability there is **causal** correlation?"
</div>
<div>

![center](./images/conditional.png)

</div>
</div>

---

# <span style="color: var(--genome)">Genomes</span> affect <span style="color: var(--connectome)">connectomes</span> given <span style="color: var(--neuroanatomy)">covariates</span>

<div class="columns">
<div>

- Want to test:
  $H_0: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) =
  F($<span style="color: var(--connectome)">C</span>|<span style="color: var(--neuroanatomy)">Co</span>$) F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$
  $H_A: F($<span style="color: var(--connectome)">C</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) \neq F($<span style="color: var(--connectome)">C</span>|<span style="color: var(--neuroanatomy)">Co</span>$)F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$
- p-value: "If genomes don't affect connectomes, what is the probability there is **causal** correlation?"
- p-values $<10^{-2}$ for only exact and global models

</div>
<div>

<br>
<br>

![center w:550](./images/conditional-pvals.png)

</div>
</div>

---

# What if we remove "heritable" vertices?

<div class="columns-bl2">
<div>

- Test per vertex $i$:
$H_0: F($<span style="color: var(--connectome)">$C_i$</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) =
  F($<span style="color: var(--connectome)">$C_i$</span>|<span style="color: var(--neuroanatomy)">Co</span>$) F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$
$H_A: F($<span style="color: var(--connectome)">$C_i$</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) \neq F($<span style="color: var(--connectome)">$C_i$</span>|<span style="color: var(--neuroanatomy)">Co</span>$)F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$

- Then test "non-heritable" subgraphs ($C_s$):
$H_0: F($<span style="color: var(--connectome)">$C_s$</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) =
  F($<span style="color: var(--connectome)">$C_s$</span>|<span style="color: var(--neuroanatomy)">Co</span>$) F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$
$H_A: F($<span style="color: var(--connectome)">$C_s$</span>, <span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$) \neq F($<span style="color: var(--connectome)">$C_s$</span>|<span style="color: var(--neuroanatomy)">Co</span>$)F($<span style="color: var(--genome)">G</span>|<span style="color: var(--neuroanatomy)">Co</span>$)$

- p-value: "If genomes don't affect connectome subgraphs, what is the probability there is **causal** correlation?"
- p-values $<10^{-2}$ for 3 hypotheses

</div>
<div>

<br>
<br>

![center w:550](./images/conditional-subgraph-pvals.png)

</div>
</div>

---

# To sum up...
> Are human connectomes heritable?

> Depends on the context.

- Connectomes are heritable, up to some common structures.

---

# Outline

- Connectomes of Human Brains
- Statistical Modeling for Connectomes
- Heritability of Human Connectomes
- **Open-source Software**

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
![w:450](../images/logos/nd_logo_small.png)

</div>

</div>


---

# Questions?

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
