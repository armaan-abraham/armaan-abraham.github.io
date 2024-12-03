---
layout: post
title: "My possible aims for AI alignment research"
date: 2024-12-02 16:59:00 -0800
categories: [agi, alignment]
excerpt: "Some of my high-level and quite tentative aims for AI alignment research over the next few years."
---

I think it is plausible that we create general human-level AI in our lifetimes.
Additionally, once we reach human-level AI, I think that superhuman AI is highly
probable shortly after. I think that such an AI could be either unimaginably
good or catastrophically bad for humans. This outcome is ultimately determined
by whether we are able to solve the AI alignment problem. I think that the
alignment problem, or more specifically the problem of controlling an agent with
superior intelligence to oneself, is fundamentally difficult, and this belief
has no dependence on any technical details about model architectures.
Unfortunately, considering the technical details only makes things seem more
difficult; much more. We have very little idea how deep learning works.

I think that AI alignment is the main challenge between us and an extremely
positive future, and I do mean extremely! I also find these topics intrinsically
interesting, for how much they overlap with existential and moral philosophy. I
am applying to PhD programs to pursue alignment research, and here I lay out
some specific objectives that I find myself gravitating towards.

_Beware! All of this is extremely speculative and not well-cited._ These
opinions are also changing fast.

## Aims

### Aim 1: Understand and engineer goals and goal-oriented behavior

While goals are difficult to define, it does seem to us humans that certain
physical processes are more goal-oriented than others. Although a person going
to the kitchen to get some food is entirely explained by fundamental
interactions between physical particles, for example in the brain of the person
and the forces between the person’s hand and the fridge door handle, there is
some sense to which the teleological explanation of this scenario—that the
person was hungry and therefore sought food from the kitchen—is preferable to
the mechanistic explanation. 

This human preference for teleological reasoning extends to many, if not most,
scenarios involving human behavior that we analyze. We view cooperation as
groups of people working together to achieve shared goals, and we view conflicts
as the resolution of people with opposing goals. On the brink of introducing
human-level artificial intelligences into this world to be shared with humans,
it has therefore been natural to view our interactions with these future AIs
also with this teleological lens. Naturally, the questions become: What goals
will the AIs have? What happens if their goals are different from ours? How can
we affect the goals of the AI?

#### Aim 1.1 Understand how to develop and elicit representations of human-compatible goals

Self-supervised learning works really well. It has powered language models like
[ChatGPT](https://doi.org/10.48550/ARXIV.2005.14165) by learning representations
from vast amounts of unlabeled data. An extremely promising aspect of LLMs is
the representations of human preferences that they have built up implicitly by
predicting the internet. Rich representations of human values already exist in
AI models! I think that this is more exciting from an alignment perspective than
many people currently admit.  However, there is still the challenge of eliciting
these goals in an AI agent. 

There are several technical approaches that leverage these human preference
representations. [Reinforcement learning from human
feedback](https://doi.org/10.48550/ARXIV.1706.03741) (RLHF) is one such
approach. Although RLHF also leverages an external signal of human preferences
to train the model, this approach only works because the human preference
representations are already latent in the LLM. RL from AI feedback (RLAIF), used
in [constitutional AI](https://doi.org/10.48550/ARXIV.2212.08073), is another
way to elicit these human preference representations from LLMs to produce a
useful agent. In constitutional AI, a human preference signal is also provided,
although with fewer required samples than in RLHF, as this is supplemented
through the textual constitution and feedback from the model itself. But again,
RLAIF is only possible because of the latent preference representations that
already exist in the LLM, and the constitution is just a way to help elicit and
create a pointer to these representations. In addition, RLAIF can be applied to
more general scenarios, for example robotics, by using multimodal, text and
image, LLMs. In [my previous work](/2024/09/30/multimodal-RLAIF.html), I demonstrated a proof-of-concept in using a
multimodal LLM to provide feedback for the pendulum control task.

#### Aim 1.2 Explore approaches to bootstrapping alignment or reward models

Self-play also works really well, at least for games. For example,
[AlphaZero](https://doi.org/10.48550/ARXIV.1712.01815) mastered chess, shogi,
and go by playing games against itself. While self-play is effective in
developing the capabilities of AI systems, one of my questions is if there is
some analog for goals, or reward models more technically. To what extent can we
bootstrap reward models? There are some indications that bootstrapping reward
models is possible in some sense. For example, [iterated amplification and
distillation](https://doi.org/10.48550/ARXIV.1810.08575) uses an ensemble of
less capable agents to produce a more capable agent that is aligned with those
less capable agents. It’s not entirely clear if a reward model is being
bootstrapped per se in this scenario, but it seems at least close to being so.

#### Aim 1.3 Build out theoretical foundations of goal-directed behavior.

I’ve found that discussions around AI alignment are often severely hindered by
improper definitions of goals, goal-directed behavior, optimizers, and agents.
For example, in discussions around [inner alignment vs outer
alignment](https://arxiv.org/abs/1906.01820), we run into some pretty major
issues when we recursively follow the outer optimizer reference and end up at
the universe optimizing for… something? Additionally, it’s quite unclear what
LLMs are optimizing for; is it next token prediction? Is it the RLHF objective?
Can next token prediction even be considered as a goal?

There are several unanswered questions around goals. What defines goal-directed
behavior? What are the minimal preconditions for goal-directed behavior? Why
might goal-directed behavior arise in our universe? Physics has already provided
[some progress on these questions](https://en.wikipedia.org/wiki/Life_3.0), and
I believe it can provide more. For example, physics allows us to reason about
these questions through non-equilibrium thermodynamics, particularly
[dissipation-driven
adaptation](https://www.quantamagazine.org/first-support-for-a-physics-theory-of-life-20170726/).
While the second law of thermodynamics states that ΔS>0, the theory of
dissipation-driven adaptation makes a stronger claim that the universe also
evolves such that the rate of entropy production, dS/dt is optimized over time.
At least we may know what the most meta optimizer does.

Fundamentally, I think that physics can help us explore the transition between
teleological and mechanistic reasoning, and that this relationship is more
important for understanding AI.

### Aim 2: Understand deep neural networks for interpretation and modification

AI alignment is plagued by a verifiability problem. We can construct these
capable AI systems with whatever fancy RL technique with whatever fancy reward
model we want, but examining external behavior of the model may not tell you
whether the model is aligned, because a sufficiently capable model could be
deceptive. Therefore, it would be extremely useful for us to look directly in
the mind of the AI to understand whether we did the job correctly. Furthermore,
if we saw something that didn’t look right, could we modify the mind directly,
in a surgical fashion, to fix the issue?

I view neural network interpretability efforts with two lenses, the bottom-up
lens and the top-down lens, or, alternatively, the mechanistic and the
teleological lens. The bottom-up lens seeks to leverage an understanding of
low-level mechanisms of neural networks to interpret model behavior. The
top-down lens seeks to leverage properties of the physical universe that neural
networks are modeling to interpret model behavior. Although these lenses aren’t
always distinct, I will seek to describe them below by elucidating how [sparse
autoencoders](https://transformer-circuits.pub/2023/monosemantic-features), a
very successful mechanistic interpretability technique, can be viewed from
either the bottom-up or top-down lens.

#### Aim 2.1 Understand neural networks from the bottom up

The bottom-up perspective to sparse autoencoders is that we discovered a
characteristic (feature superposition) that efficient neural networks would
exhibit to hold and process more information that is highly specific to the
fundamental structure of a neural network and leveraged this discovery to
automatically dissect neural networks into more interpretable parts using sparse
autoencoders. The foundations for feature superposition were laid out in [Toy
models of
superposition](https://transformer-circuits.pub/2022/toy_model/index.html),
which used a very physics-esque approach in its analysis. I believe that
leveraging perspectives and tools from physics can continue to be successful in
this bottom-up approach to interpretability. One reason is because of the
history of physics in deriving simple, effective theories of systems consisting
of many elementary components and their interactions (e.g., thermodynamics,
statistical mechanics) which [at least
suggests](https://arxiv.org/abs/2106.10165) the effectiveness of physics in
understanding the many simple interacting neurons in neural networks. In line
with this bottom-up approach, [I independently did some
analysis](/2024/10/20/sae.html) of some weird stuff I saw with in
the current literature on feature superposition.

#### Aim 2.2 Understand neural networks from the top down

The top-down perspective to sparse auto encoders is that we used a general
physical property about the universe to imply certain characteristics that
models of the universe will exhibit and leveraged this property to automatically
dissect neural networks into more interpretable parts using sparse autoencoders.
This general physical property is not perfectly defined, but one popular
description is in [Bruno Olshausen’s
work](https://www.sciencedirect.com/science/article/pii/S0042698997001697). A
bit differently from Olshausen’s description, I would describe this property as
that there are many properties about the universe, but these properties are
somewhat local, meaning that not all properties are relevant at any given point
in spacetime. This enables feature superposition because you can superpose
features, relating to physical properties, that are not relevant together. Other
work in related to the top-down approach includes Why does deep and cheap
learning work so well? For different reasons, I also believe physics is quite
valuable for this top-down approach, because this approach relies on
establishing fundamental properties of useful models of our universe which
ultimately depends on our universe and its laws.

### Aim 3: Integrating biological and artificial intelligence for alignment

The AI alignment problem is fundamentally a problem regarding the relationship
between human and AI. Therefore, I think that approaches that jointly study the
brain and AI are promising. 

#### Aim 3.1 Representational alignment between neural networks and brains

Recent work on representational alignment have studied how representations
across models relate to each other, how to make these representations more
similar, and what benefits various representations offer. One particularly
interesting (and very sci-fi-y!) avenue in this area is aligning the
representations of artificial neural networks and the brain. [It has been
found](https://openreview.net/forum?id=SMYdcXjJh1q) that aligning CNN and
macaque inferior temporal cortex representations improves CNN adversarial
robustness. From an alignment perspective, these approaches are all promising
for generating AIs that are less alien to us, in a general sense, for example to
help us anticipate behaviors and failure modes in AIs.

#### Aim 3.2 Using reward centers in the human brain for regularizing RL agents and designing reward functions
The AI representations that we most want aligned with human representations are
representations of goals. [Some existing
work](https://www.nature.com/articles/s42256-024-00854-2) in the area of
integrating the goals of biological and artificial intelligence has involved
using RL agents to directly control the neurons of the C elegans worm to achieve
some externally specified task, although ideally we are looking for the reverse
of this. Work in this area would probably seek to explicitly make the
representations of goals, for example in RL agents, more similar to the goals
encoded in brains, ideally human brains.

## Conclusion

All of these approaches are directly relevant to designing AI systems that
intrinsically seek to benefit humans. Aim 1 will improve our ability to instill
human-centered goals in AI systems, Aim 2 will allow us to verify whether an AI
system is successfully aligned with human preferences, and Aim 3 will more
directly rely on biological brains and their representations to design AIs that
are more compatible and comprehensible to humans. In the ideal scenario, I join a
lab that allows me to pursue all three aims, but focusing on a subset of these
aims is also good and probably more realistic. But aim high!
