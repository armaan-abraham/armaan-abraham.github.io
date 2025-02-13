---
layout: post
title: "Proving the absence of deceptive misalignment"
date: 2024-10-20 12:00:00 -0500
excerpt: "A modeling approach and a proof for why it avoids deceptive misalignment in a very limited context."
---

#### Question

Suppose you want to train a model to do superhuman question-answering. To do
that, you collect a dataset of (x, q, a) pairs where x is the output from some
set of sensors at some time, q is some question about the world at that time,
and a is some answer to that question, collected by humans investigating the
question at a later time. You then want to train a machine learning model via
some training scheme to fit that dataset. As an abstraction, we'll think of all
training processes as describable by a prior with the property that, when
conditioned on the dataset, the resulting posterior describes the distribution
of models that result from applying that training process to that dataset. Thus,
when I ask you to describe a training process with particular properties, you
need only specify a prior and a dataset-generating procedure—and you're welcome
to provide any describable prior, computable or not (so a Solomonoff prior is
fair game, for example). Now, here are some models that you might get in such a
situation: The direct translator honestly answers questions according to its
internal model of the world. The human imitator mimics the process used by humans
to produce the answers in the training distribution. The deceptive model has some
completely separate goal—e.g. maximize paperclips—but answers questions honestly
during training specifically because it wants to be selected by the training
process so that it can eventually enact a treacherous turn. The ELK problem asks
you to find a training process that preferentially selects for the direct
translator over the human imitator (it's also slightly different in that it only
asks you to learn a question-answering head on top of an existing predictive
model, whereas here we want to learn the whole thing end-to-end). The problem
here, however, is to find a training process that preferentially selects for the
human imitator over the deceptive model. We're putting aside the question of how
to get the direct translator entirely here and instead just focusing on how to
not get the deceptive model.

#### Answer

We will define a set, S_M, of allowed models (i.e. P=0 for all other models),
but no other priors (i.e. probability is evenly distributed over models in S_M).
S_M contains MLPs (I use MLPs only to help describe the approach in concrete
terms) of identical architecture and thus also identical parameter counts K.
Furthermore, K is low enough that all models in S_M are underparameterized
relative to the dataset, X (i.e., adding more parameters >K can always yield
lower train loss for every M in S_M). Given that there are no other model
priors, our training procedure is to just choose the model in S_M that achieves
the lowest training loss, where the training loss is computed as the difference
between the human-generated answers and the model-generated answers. How the
dataset is collected doesn't matter too much beyond the premises already
outlined in the question, but the larger, more diverse, and accurate the
dataset, the better.

I will prove that this approach avoids deceptive alignment by contradiction:

For deceptive alignment to exist, our training process must be capable of
producing some model, M_d, which possesses a mesa objective O_mesa that will
cause some undesired behavior on the deployment distribution. For this behavior
to exist, M_d *must have some way of checking for a distributional shift*. Such
a circuit would compute P(x,q|deployment) (=1-P(x,q|train)) and then use this to
determine whether to pursue the base objective or the mesa objective. The
crucial detail of this circuit is that it has no effect on the training loss.
One can see this by removing the circuit during training and just have the model
pursue the base objective (e.g. by just hardcoding what would happen if P(train) > 0.5). 
This modification would produce identical behavior on the training
distribution, and thus identical training loss. However, if such a circuit
exists and doesn't affect the training loss, we can replace the parameters
forming that circuit with parameters that are instrumentally useful for pursuing
the base objective and thus reduce the training loss, because M_d is
underparameterized; therefore, there exists another model in S_M with a lower
training loss than M_d, a contradiction.

In a more practical scenario, this approach may still be vulnerable to a
treacherous turn during training. However, this question only asks for a prior
(including those that are non-computable) and a dataset-generating procedure,
which I take to mean that we don't need to specify a particular numerical
optimization process and we can just "jump" to the highest probability model.
Alternatively, you could answer this question using a class of models for which
analytical solutions exist instead of MLPs (even if finding the analytical
solution takes a very long time) and you would avoid this issue. But, more
analysis would be required if we wanted to state a concrete local optimization
procedure to prevent treacherous turns during training itself.
