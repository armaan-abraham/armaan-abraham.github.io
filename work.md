---
layout: default
title: Work
---

# Work

## Papers

*[Multivalent binding model quantifies antibody species from systems
serology](https://www.biorxiv.org/content/10.1101/2024.07.05.602296v1)* __Armaan A.
Abraham__, Zhixin Cyrillus Tan, Priyanka Shrestha, Emily R. Bozich, Aaron S. Meyer (2024) Preprint.

_[Integrative, high-resolution analysis of single cells across experimental
conditions with
PARAFAC2](https://www.biorxiv.org/content/10.1101/2024.07.29.605698v1)_ Andrew
Ramirez, Brian T. Orcutt-Jahns, Sean Pascoe, __Armaan A. Abraham__, Breanna Remigio,
Nathaniel Thomas, Aaron S. Meyer (2024) Preprint.

## Projects

#### **Reinforcement learning of abstract, multimodal tasks from AI feedback**

<div style="float: right; margin-left: 20px; max-width: 300px">  
<img src="/assets/images/terminal_model.png" alt="Reward model visualization">
<figcaption style="text-align: center; font-style: italic;">LLM-derived reward model predictions for the pendulum control task</figcaption>
</div>
([github](https://github.com/armaan-abraham/intention-learning))

- My objective here is to use a text+image LLM to train agents to perform
abstract, arbitrary tasks that can be specified with human-interpretable text
and images.
- The multimodal LLM evaluates pairs of states in the environment and judges
which state is more representative of the specified goal. These judgments are
then used to optimize the agent's policy to pursue the goal, as would be done in
RLHF (except instead of a human, it's a multimodal LLM that's generating
feedback, and much more frequently). [Constitutional
AI](https://arxiv.org/abs/2212.08073) is an example of this approach, except
purely for chat-based objectives in text (as opposed to tasks that may require
visual perception).
- At a high level, I think this approach is a way to convert the perceptual
capability and rich knowledge representations of LLMs into agentic capability (i.e.
choosing actions that steer the world into some area of state space).
- My main motivation for this approach is AI alignment. LLMs have shown to
possess a robust understanding of human concepts and, importantly, values, but
by directing LLMs in a classic RL setting with hand-crafted reward signals,
we're throwing these human value representations away and creating
vulnerabilities for task misspecification. This problem becomes more severe when
the tasks are more complex and abstract. However, by using the raw, pretrained,
LLM as the judge for an agent, we can leverage these human value representations
directly. I hope that this is on the path to being able to ask an AI to "please
do what we want" (see [coherent extrapolated
volition](https://intelligence.org/files/CEV.pdf)) and to just have that work.
- This is a work in progress. So far, I have gotten the approach working for the
simple pendulum control problem (but with the only reward signal coming from the
LLM). I hope to demonstrate this approach's advantage by training an agent on
some objective that is abstract or relies on implicit human understanding, for
which traditional RL is ill-suited.

#### **Unaligned Low-rank Tensor Regression with Attention (ULTRA)**

- I invented and implemented this method as a way to automatically construct
mechanistic explanations of arbitrary sample metadata (e.g. patient disease
status) from single-cell RNA sequencing data.
- I discovered that a very natural way to solve this problem is to use a form of
*cell attention* to pick out cell types for which the expression of some gene(s) is maximally
covariant with the response variable.
- While existing tensor decomposition methods allow the reduced-rank
regression of regular (i.e. aligned) tensors (e.g.
[CP-PLSR](https://www.semanticscholar.org/paper/Multiway-calibration.-Multilinear-PLS-Bro/5d7a1f4c37d36b804183d4240a304d1539cf5551))
and there exist unsupervised tensor decomposition methods for unaligned
tensors (e.g. PARAFAC2, which [our lab also applied to
scRNA](https://www.biorxiv.org/content/10.1101/2024.07.29.605698v1)), there
is currently no way to perform reduced-rank regression on unaligned tensors,
which is the structure of scRNA-seq data.
- This method automatically answers a very typical type of question that
researchers ask in scRNA, of the form "which genetic programs in which subsets
of cells are responsible for this phenotype".
- This is a work in progress. For the math and preliminary results, see [my
slides](/assets/mm-presentation.key).

#### **RL-based generation of peptide sequences conditioned on fuzzy structural constraints**
([github](https://github.com/armaan-abraham/Qres))
- [AlphaFold2](https://www.nature.com/articles/s41586-021-03819-2) allows us to
predict protein structure from sequence. Additionally, [inverse
models](https://www.biorxiv.org/content/10.1101/2022.04.10.487779v2) have also
been developed, which predict the sequences of naturally occurring proteins from
their structure. However, both of these models are limited in many protein
engineering contexts, where we have some particular structural feature that we
want to generate in an engineered protein. 
- A crucial problem here is that we __don't know exactly what protein structures
are possible__ (i.e. for which structures there exists some sequence), and our
structure-to-sequence models do not yet have the capability to find similar
structures, for which sequences exist, to a target structure. Additionally,
aside from this target design feature, the rest of the protein structure is often
irrelevant, and thus we would like a way to search for proteins based on a fuzzy
structural search.  One approach to this has been [searching over a latent
design
space](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1010271)
(e.g. from a VAE) to find proteins with the desired structural feature.
- Here, I propose the approach of using an RL protein design agent along with
AlphaFold2 to assemble proteins conditioned on loose structural constraints. In
this process, the RL agent generates an amino acid sequence incrementally,
receiving feedback on how well the structure (from AlphaFold2) of the current
prototypical sequence meets the design criteria after each incremental
generation step.
- One can think of this as either (1) a sequence generator as a model-free agent
in a simulated environment that is AlphaFold2 or (2) a model-based RL agent
where the policy is produced by the sequence generator and the model is
AlphaFold2, and the objective is to produce some output sequence that meets the
design criteria when it is actually synthesized in a lab. When thinking of this
as (2), one can see a sort of capability bootstrapping, where we can increase
intelligence related to proteins without having to collect any more measurements
from the real world. This is along the same line of thinking as Yoshua Bengio's
idea of [using a world model to develop a very large amortized inference
machine](https://yoshuabengio.org/2023/03/21/scaling-in-the-service-of-reasoning-model-based-ml/).
- This is a work in progress. I am currently still working on generating
peptides conditioned on structural constraints.
