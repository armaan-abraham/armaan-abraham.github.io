---
layout: post
title: "Reinforcement learning of abstract, multimodal tasks from AI feedback"
date: 2024-09-30 12:00:00 -0500
excerpt: "Using a text+image LLM to train agents to perform
abstract, arbitrary tasks that can be specified with human-interpretable text
and images."
github: "https://github.com/armaan-abraham/intention-learning"
importance: 5
---

<div style="float: right; margin-left: 20px; max-width: 300px">  
<img src="/assets/images/terminal_model.png" alt="Reward model visualization">
<figcaption style="text-align: center; font-style: italic;">LLM-derived reward model predictions for the pendulum control task</figcaption>
</div>

[Github](https://github.com/armaan-abraham/intention-learning)

My objective here is to use a text+image LLM to train agents to perform
abstract, arbitrary tasks that can be specified with human-interpretable text
and images.

The multimodal LLM evaluates pairs of states in the environment and judges
which state is more representative of the specified goal. These judgments are
then used to optimize the agent's policy to pursue the goal, as would be done in
RLHF (except instead of a human, it's a multimodal LLM that's generating
feedback, and much more frequently). [Constitutional
AI](https://arxiv.org/abs/2212.08073) is an example of this approach, except
purely for chat-based objectives in text (as opposed to tasks that may require
visual perception).

At a high level, I think this approach is a way to convert the perceptual
capability and rich knowledge representations of LLMs into agentic capability (i.e.
choosing actions that steer the world into some area of state space).

My main motivation for this approach is AI alignment. LLMs have shown to
possess a robust understanding of human concepts and, importantly, values, but
by directing LLMs in a classic RL setting with hand-crafted reward signals,
we're throwing these human value representations away and creating
vulnerabilities for task misspecification. This problem becomes more severe when
the tasks are more complex and abstract. However, by using the raw, pretrained,
LLM as the judge for an agent, we can leverage these human value representations
directly. I hope that this is on the path to being able to ask an AI to "please
do what we want" (see [coherent extrapolated
volition](https://intelligence.org/files/CEV.pdf)) and to just have that work.

 This is a work in progress. So far, I have gotten the approach working for the
simple pendulum control problem (but with the only reward signal coming from the
LLM). I hope to demonstrate this approach's advantage by training an agent on
some objective that is abstract or relies on implicit human understanding, for
which traditional RL is ill-suited.