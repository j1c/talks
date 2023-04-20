---
marp: true
theme: slides
size: 16:9
paginate: true
---

# Connectomic Heritability: a Causal Modeling Analysis

## Jaewon Chung

_(he/him)_ - [NeuroData lab](https://neurodata.io/)
_Johns Hopkins University - Biomedical Engineering_

![icon](../images/icons/mail.png) [_j1c@jhu.edu_](mailto:j1c@jhu.edu)
![icon](../images/icons/github.png) [_@j1c (Github)_](https://github.com/j1c)
![icon](../images/icons/twitter.png) [_@j1c (Twitter)_](https://twitter.com/j1c)

![bg right:35% w:400](../images/logos/nd_logo_small.png)

---

<style scoped>
h2 {
    justify-content: center;
    text-align: center;
}
</style>

<!--
Heritability studies have led to numerous breakthroughs in our understanding of the genetic influences on various traits, behaviors, and diseases. For example, twin studies have shown that genetic factors play a significant role in the development of type 1 diabetes, and researchers have identified early markers of the disease, such as the presence of specific antibodies, which can predict the onset of type 1 diabetes. This has led to the development of early screening programs and interventions focused on delaying or preventing the onset of type 1 diabetes in high-risk individuals.

With the availability of large-scale neuroimaging datasets, it is now possible to investigate the heritability of the connectome. The connectome is the network of neural connections in the brain, mapping the structural links between different brain regions. In essence, the connectome serves as a comprehensive blueprint of our brain. Connectomic heritability, then, is the study of how genetic factors contribute to individual differences in brain connectivity patterns. This is important because we believe that the connectome is a key determinant of brain function and behavior. Therefore, understanding connectomic heritability can offer valuable insights into the genetic influences on brain function and behavior.

However, there are several challenges in studying connectomic heritability. Connectomes are high-dimensional, non-Eucledian, and non-linear data making current methods for studying heritability, which rely on strong distributional assumptions, inadequate. Furthermore,  most methods assume an associational effect between the genome and a specific trait, rather than a causal effect.

To address these limitations, we propose two solutions: first, we formalize heritability as causal effects. With a causal model, we can identify measurable covariates to control for unmeasured confounding, allowing us to make causal claims. Second, we leverage statistical models that capture the underlying structure and dependence within connectomes. This approach allows us to define different notions of connectome heritability by eliminating common structures, such as differences in connectome scaling. With these solutions, we want to answer the question: do genomes cause connectomes?

We apply our analysis framework to connectomes estimated from the Human Connectome Project diffusion MRI data. The Human Connectome Project is a large-scale neuroimaging study that brain scanned identical twins, fraternal twins, and non-twin siblings.
-->

---

<footer>

[Chung, Jaewon, et al. "Human Connectomes Are Heritable." bioRxiv (2023): 2023-04.](https://www.biorxiv.org/content/10.1101/2023.04.02.532875.abstract)

</footer>

<!--
Using the statistical models for networks, we can learn a low-dimensional, Euclidean representation of connectomes called latent positions, and these latent positions allow us to measure the differences between pairs of connectomes. In panel A, we plot the differences between connectomes separated by familial relationships. Points toward the left in each column indicate smaller differences, while those on the right represent larger differences. If we focus on the diamonds, which represents the median differences, we can observe a pattern: as familial relationships become more distant, the median differences between connectomes tend to increase.

To explain a bit more about the three columns in panel A, the The exact model in column i This model measures all differences between latent positions, with differences in the latent positions implying differences in the connectomes themselves. Global model: This model examines whether the latent positions of one connectome are a scaled version of the other.

In panel B, we show the causal hypothesis test, which tells us that heritability exists if the test is significant. We can see that the test is significant except for the vertex models, which means that we can reject the null hypothesis that there is no causal effect of genomes on connectomes. This suggests that connectomes are heritable, and that genetic factors play a significant role in shaping the connectome.


Our findings reveal that heritability can be detected when considering potential confounding like neuroanatomy, age, and sex. However, once we address for vertex-wise rescaling between connectomes, heritability can no longer be detected.

So where do we go from here?
These results suggest that previous conclusions on connectome heritability may have been driven by rescaling factors, and future studies should address potential confounds in their data.
We hope that our work will help to advance our understanding of the genetic influences on the connectome, and ultimately, the brain. We also hope that our work will help to inform future research directions and potential applications of connectomic heritability. For example, connectomic heritability can be used to inform personalized medicine, early diagnosis and intervention, and improved understanding of brain function and development.
-->

---

<style scoped>
p {
    font-size: 22px
}
h4 {font-size: 28px}
</style>

<div class="columns">

<div>
<h1>Acknowledgements</h2>

#### JHU

<div class='minipanels'>

<div>

![person](../images/faces/ebridge.jpg)
Eric Bridgeford

</div>

<div>

![person](../images/faces/powell.jpg)
Mike Powell

</div>

<div>

![person](../images/faces/pisner.jpg)
Derek Pisner

</div>

<div>

![person](../images/faces/cep.png)
Carey Priebe

</div>

<div>

![person](../images/faces/jovo.png)
Joshua T. Vogelstein

</div>
</div>

#### Microsoft Research

<p style="font-size:20%;">

Dax Pryce, Bryan Tower, Nick Caurvina, Patrick Bourke, Jonathan McLean, Carolyn Buractaon, Amber Hoak.

</p>
</div>
<div class="vl"></div>
<div>
<br><br><br><br><br>
<p><h1 align='center'>Questions?</p>
</div>

</div>

<!--
Last, but not least, I would like to thank my collaborators at Johns Hopkins and Microsoft Research.
-->

---

<br><br><br><br><br>

<p><h1 align="center">Additional Slides</p>

---

# MRI to Connectomes

<br>

![center](../images/heritability/m2g_pipeline.png)

---

# Analysis Framework

![center](../images/heritability/framework.png)

---

# Causal Directed Acyclic Graph

<br>

![center w:800](../images/heritability/dag.png)

---

# Causal Estimand

- $X$ denote exposure, $Y$ denote outcome, $W$ denote measured covariates, $Z$ denote unmeasured covariates.
- Want to estimate the effect of different exposures on the outcome, which is quantified using the backdoor formula if $W$ and $Z$ close all backdoor paths.
  $$f_{w, z}(y|x) = \int_{\mathcal{W}\times\mathcal{Z}}f(y|x, w, z)f(w, z)\mathrm{d}(w, z) $$

- Above integrates over _all_ measured and unmeasured covariates.

$$ f(y | x) = \int\_{\mathcal W \times \mathcal Z}{f(y | x, w, z) f(w, z | x)}{(w, z)} $$

- Averages the true outcome distribution over the _conditional_ distribution of the measured and unmeasured covariates.

---

# Hypothesis Testing

### Associational Heritability

- We observe the pairs $(x_i, y_i)$ for $i\in[n]$.
- Only be able to estimate the functions of $(X, Y)$
- The corresponding hypothesis test is:
  $$
  H_0: f(y|x) = f(y) \quad \text{vs} \quad
  	H_A: f(y|x) \neq f(y).
  $$

### Causal Heritability

- We observe the triples $(x_i, y_i, w_i)$ for $i\in[n]$.
- Only be able to estimate the functions of $(X, Y, W)$
- The corresponding hypothesis test is:
  $$
  H_0: f(y|x, w) = f(y|w) \quad \text{vs} \quad
  	H_A: f(y|x, w) \neq f(y|w).
  $$

---

# Connectome Models

- Exact model: This model measures all differences between latent positions, with differences in the latent positions implying differences in the connectomes themselves.

---

# Connectome Model Simulations

![center w:900](../images/heritability/3-simulations.png)

# Shortcomings - Network model

- Problems with connectome estimation.
  - Inability to determine the precise origin/termination of connections in the cortex.
    - -> false negatives
  - Crossing fibers
    - -> false positives
- RDPG can only represent subset of independent edge networks.

![center h:300](./../../images/network_models.png)

---

# Shortcomings - Model assumptions

- No interaction between genome and environment
- No epistatsis
  - Effect of one gene is dependent on another
  - Ex: black hair and baldness
- No dominance effects
- Strong assumptions in genetic distances
