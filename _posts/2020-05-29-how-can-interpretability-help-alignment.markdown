---
layout:  post
title:   "How can Interpretability Help Alignment?"
date:    2020-05-28 10:00:00 +0000
tags:    interpretability safety alignment aisrp
excerpt: We've previously written about what interpretability research might be. In this post we think about how different kinds of interpretability research (even loosely formulated) can help AI alignment research agendas and proposals. It seems that there are meaningful differences in the kind of tools and research different agendas would benefit from, and we aim to make these differences clearer. This is useful in helping prioritise what kinds of interpretability research are likely worth doing.
---

_This post was coauthored by Flo Dorner and [Tomáš Gavenčiak](https://gavento.ucw.cz/), and cross posted to the [Alignment Forum](https://www.alignmentforum.org/posts/uRnprGSiLGXv35foX/how-can-interpretability-help-alignment)_

# Introduction

We've previously written about [what interpretability research might be](https://www.alignmentforum.org/posts/rSMbGFfsLMB3GWZtX/what-is-interpretability). In this post we think about how different kinds of interpretability research (even loosely formulated) can help AI alignment research agendas and proposals. It seems that there are meaningful differences in the kind of tools and research different agendas would benefit from, and we aim to make these differences clearer. This is useful in helping prioritise what kinds of interpretability research are likely worth doing.

### Framing

* In solving the problem of AI Alignment, we’ll need to both answer *research questions* (e.g *Is it optimal to tell the truth in a debate game?*) and work out how to complete *tasks* reliably and quickly (e.g. *Given an AI, tell me whether it will allow us to turn it off*).

    * The *research questions* we only need to answer once (and hence can spend significant research effort on), whereas completing one of the *tasks* can’t be too intensive to make it feasible to complete it regularly, but will require strong tools or methods.

* Interpretability research will be useful for alignment by enabling and enhancing other research proposals and agendas, and so one of the best ways of thinking about what kind of interpretability research to do is to think about other proposals and how specifically interpretability can help them. We see three broad ways interpretability could enable other proposals:

    * Developing a more formal theory of interpretability and explainability could help with avenues such as [open source game-theory](https://arxiv.org/abs/1602.04184) and [mechanistic transparency](https://www.alignmentforum.org/posts/3kwR2dufdJyJamHQq/mechanistic-transparency-for-machine-learning), where some sense of *Interpretation* or *Understanding* is required in an algorithmic sense.

    * Theoretical exploration of components or tools, such as exploring viable general interpretation methods and their desiderata, future strong versions, promises & limits. This will help in understanding how we may be able to use interpretability in the future in other proposals, in scenarios we don’t yet encounter or haven’t considered. This side of interpretability is likely valuable long-term and neglected by the current mainstream ML research. In a sense this post is the result of trying to do this kind of research.

    * Enabling or amplifying the insights gained from experiments performed by researchers (both alignment and mainstream)  today, helping them develop answers to  their proposals’ *research questions*.

# Different types of interpretability can help different areas of AI alignment

As expressed in the previous section, interpretability can help with a wide range of different research agendas and proposals in different ways. We want to give a few examples examining this idea, and then draw some general conclusions from the patterns expressed in these examples.

## [Iterated Distillation and Amplification](https://www.alignmentforum.org/s/EmDuGeRw749sD3GKd) (IDA)

There are a variety of research questions that this proposal will need to tackle to succeed:

* *How do we build a Distillation process that preserves alignment?*

    * *Does Distillation of form X preserve alignment?*

    * *What properties does distillation of form X preserve?*

* *How do we build an amplification process that increases the capabilities of the AI while not diminishing the alignment?*

    * *Is the Factored Cognition hypothesis correct?*

* etc. etc etc.

A key problem which we need to be able to solve for IDA to be safe is to consistently be able to validate whether the distilled agent’s behaviour is faithful to the overseer's behaviour (or the behaviour the overseer aims to incentivise). We think interpretability research is a key way in which we could perform this validation. Methods which work with the form of agent produced by IDA would be necessary; this might be RL agents or another paradigm not yet encountered. An interesting feature of these  methods would be that they only need to work comparatively: they might not need to say something about the distilled agent’s behaviour in isolation. We can use our method to validate the changes at each iteration, and by assumption we have faith in the initial agent, so by similar reasoning to IDA working in the first place, we’d be happy with the final agent even if we can’t completely understand it in isolation.

In terms of the research questions which interpretability might be able to help with, If we start doing experiments with amplification and distillation of AIs, then using interpretability methods on the produced agents might help us generate good intuitions or even proofs of how different properties are changed in the amplification and distillation stages. This is quite generic, and It’s plausible there’s limited work to be done in the true case, as a key part of the process is the human (or collection of humans) being amplified. Human interpretability is a whole different subject from AI interpretability, and while there might be some overlap (systems biology & neuroscience and deep learning have learned from each other before), it’s uncertain whether that kind of work is necessary.

## AI Safety Via Debate

For an explanation of this agenda, see [here](https://arxiv.org/abs/1805.00899) and [here](https://distill.pub/2019/safety-needs-social-scientists/). For debate, there's a broad range of research questions which would need to be answered, including questions (often related to the ones in IDA) about whether Debate works and produces safe AI, such as *Does debate incentivise truth-seeking behaviour or just maximally persuasive behaviour?*. We currently think it’s less likely that AI interpretability can help with [these kinds of questions](https://distill.pub/2019/safety-needs-social-scientists/#questions); game theory and the social science seem best posed to answer them.

It also includes tasks we'll need to be able to perform repeatedly and reliably. In the current technical research on debate, the debate game is often set up with one debater arguing for a truthful statement, and the other arguing against said statement. In this setting, there are questions such as

* *Is this debater telling the truth or lying?*

* *Is this debater honestly presenting the evidence it's presenting or not?*

I believe interpretability methods can help the judges in the debate games answer these questions more effectively, by enabling them to understand what is influencing a debater's action at a specific time. Work such as [Influence Functions](https://arxiv.org/abs/1703.04730) could enable us to see which training data is most impacting the current AI's decision, which could give us insight into what the agent's current motivation is (i.e. if the most influential training data was a time when the debater lied and got away with it, winning the debate, it seems more likely that the debater is currently lying). In the general case, the debaters might not know the truth value of the statement they’re arguing for. Even in this case if our interpretability methods can spot when an agent is trying to be deceitful we can punish this, to try to encourage truth-seeking behaviour. (NOTE: This depends a lot on the operationalisation of "trying to be deceitful", and it’s unclear whether using interpretability in this way would encourage truth-seeking behaviour or just cleverer deceitful behaviour).  In both the case of knowing the truth value of the debate and not, if the judge is another AI, then our interpretability methods would only need to enable that AI to gain insight, not humans. 

Other methods may also be able to help with these kinds of problems; If we can understand the internal structure of the debater in some way, then see which parts of the internals are activated when it acts in a certain way (effectively an MRI for a neural network), then we might be able to understand when it's lying or telling the truth.

In general these methods need only be local (applied to a debater's actions at specific time steps) to still enhance and empower the judge.

## Recursive Reward Modelling

See [here](https://medium.com/@deepmindsafetyresearch/scalable-agent-alignment-via-reward-modeling-bf4ab06dfd84) for an explanation of this alignment proposal. The main idea is that we learn a reward model from humans which we can then use to teach AI. We recurse on this setup by using the AI we've trained so far to help assess the behaviour of the new AI, to try and help us understand whether it's behaviour is good or bad, so the reward model we learn is as good as possible.

In terms of research questions that this method has, they’re in a similar vein to the IDA proposal, but with more of a focus on AIs in the recursion. This might make it more amenable to interpretability methods helping us to find out whether reward modelling is a solution which works well for creating strong aligned AI. If we’re able to build reward models and examine their internals, we can see how well reward modelling tends to work in different scenarios. On the recursive side, having a consistent insight into the differences between the successive reward models we create would be useful. As in IDA, we may only need to look at the difference between reward models and AIs rather than understanding them on their own.

In terms of tasks interpretability could help with, one possibility is interpretability methods to be used by the helper AI in inspecting the behaviour of the current AI, to induce a loss function not just on it's behaviour but also it's internal reasoning. If we had interpretability methods which are strong enough to give this kind of insight then this could be a strong increase in the effectiveness of this method. We would need transparency techniques to allow the helper AI to get a good enough insight on the current AI’s reasoning to induce some kind of reward signal, and methods which actually generate this insight. In this case humans might not ever see the output of the interpretability method, as it’s just used by the reward model to judge the AI’s reasoning.

## Mesa Optimisation

For an explanation of mesa optimisation, see [here](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB). This is one of the most convincing (I believe) examples of how interpretability can be useful, and is concerned with the problem of inner alignment. The classic question here is something like *Does this agent contain an unaligned mesa-optimiser?*. More generally, *Does this training process produce agents which contain unaligned mesa-optimisers?*.

I think the research questions around mesa optimisation are ones that interpretability methods will definitely help us solve; this problem is about how the training procedure of an AI unfolds, and how the internals of the AI reason. Insight could be gained on these kinds of problems through a broad range of methods: *Influence Functions*, *[Loss Change Allocation](https://arxiv.org/abs/1909.01440)* and other methods which introspect on the training procedure seem particularly useful. We think transparency approaches (such as those motivated in [An analytical perspective on AI alignment](https://www.lesswrong.com/posts/8GdPargak863xaebm/an-analytic-perspective-on-ai-alignment)) also have a good chance of enabling the insights we want in a way which doesn't require running the agent (in simulation or not) as it doesn't aim to produce insight from behavioural examination.

Principally, sufficiently strong and farsighted optimizers should not produce unaligned mesa-optimisers, as doing so would usually not be optimal in the long term. Insofar as interpretability helps us (or the advanced optimisation loops we build) with predicting model behaviour in novel situations, it could help us to filter out some unaligned mesa-optimizers. There are two caveats: First, this assumes that our optimizers are already quite powerful without the interpretability method, as even unaligned mesa-optimizers might improve generalization compared to weaker models that do not utilize any optimization. Second, filtering some unaligned mesa-optimizers could turn out net-negative, if the remaining ones are especially malicious, since they are relatively more likely to be selected after filtering.

## Proposal-agnostic ideas

There are some tasks interpretability might help us with which are proposal-agnostic. We won’t go into a lot of detail on these kinds of ideas here, as I’m focusing on differences between proposals, but we thought it was worth mentioning two ideas. 

An often proposed idea for how interpretability could help with alignment it through auditing final models produced by any kind of method. In this setting, once we have produced a model, before deploying it to the real world, we first inspect it with our interpretability tools to make sure it’s not misaligned. This capability probably won’t solve AI alignment on it’s own, as if we discover the AI is misaligned, it doesn’t provide us with a next step apart from training another AI and hoping this one works out. It’s possible that it might be enough, if misaligned models are a small part of the model space, and retraining can quickly get us to an aligned model, but this seems unlikely.

A second idea, [put forward by Chris Olah](https://www.alignmentforum.org/posts/X2i9dQQK3gETCyqh2/chris-olah-s-views-on-agi-safety#Improving_the_field_of_machine_learning), is that interpretability can improve the field of ML, making it a more rigorous, scientific discipline which tries to truly understand the models we’re creating, rather than just pushing for the best results. This is a long shot, but if we achieved this kind of fundamental reorientation, it seems like it would be very beneficial for AI safety and alignment, as we’d understand how our models worked a lot more (and research which built understanding would be rewarded), rather than just creating really good optimisers with little insight into how they work and what behaviour they’ll have.

## Conclusions and Patterns

* Recursive approaches could benefit from methods which compare models, which might be easier to create than methods which look at a single model in isolation

    * This applies to IDA and recursive reward modelling most obviously

* Interpretability seems like it may be able to create a kind of regularisation or optimisation pressure on a trained model to be aligned, and this would be useful in a variety of proposals. In some of these settings a human never has to see the result of the interpretability method.

    * This is different from [our previous thoughts](https://www.alignmentforum.org/posts/rSMbGFfsLMB3GWZtX/what-is-interpretability), where we said interpretability methods should often have a human in the loop. This is a blurry area, but we think research in this direction would be useful, whether you label it interpretability or not.

* For research questions, proposals which can produce experiments instantiated with ML tools can benefit more from the insights gained from applying interpretability methods to these experiments.

* Most agendas want methods which give a global view of the AI's reasoning and internal representations. These kinds of methods will probably be harder to create, but more likely to be helpful. Debate seems like it could still benefit from just local explanations or interpretations.

* In general, most agendas focus on creating or understanding agents. The current paradigm for this kind of research is reinforcement learning, and so more research focusing on interpreting RL agents and training procedures could benefit alignment in general.

    * RL might not be the prevailing paradigm when we actually build AGI - but it’s likely to be closer to the prevailing paradigm that supervised learning, as it has certain characteristics, such as path-dependence, and significant non-learned components (e.g. MCTS), that we will need to keep in mind when building interpretability tools.

# These differences can help you decide which kinds of interpretability research to work on

What does all this mean? What's the use in thinking about all of this? We believe this kind of thinking is useful to help prioritise which kinds of research we might want to pursue, both within interpretability and when considering between interpretability and other related fields. If we believe a particular proposal is more or less likely than others to produce aligned AI, then we would preferentially work on interpretability research which we believe will help this proposal over research which wouldn't, as it wouldn't be as useful. These thoughts would of course also be influenced by what AI timelines you find most plausible, as this influences which AI Alignment proposal seems most likely to succeed, or which proposal most needs to succeed.

An important consideration is whether the interpretability research which seems useful for alignment is research which we expect the mainstream ML research community to work on and solve suitably. If this would happen, then it seems comparatively better to work on other alignment research which is just as necessary but isn’t being worked on by the mainstream. Currently however, we don’t think this is the case. There’s little research which focuses on interpreting reinforcement learning agents (which seems very relevant to AI Alignment), or with an explicit focus on producing methods which scale to stronger AIs and are aimed at solving the tasks we want to focus on in AI Alignment.

Overall, we think interpretability research, if targeted towards methods and insights which will help with AI alignment proposals or agendas, is a useful set of research directions to pursue. I’ve talked about a few of these directions in this post, but no doubt there are more.
