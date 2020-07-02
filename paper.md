---
title: 'sbi - a toolkit for simulation-based inference'
tags:
  - simulation science
  - likelihood-free inference
  - bayesian inference
  - system identification
  - parameter identification
authors: 
 - name: Alvaro Tejero-Cantero
   orcid: 0000-0002-8768-4227
   affiliation: "*, 1"
 - name: Jan Boelts
   orcid: 0000-0003-4979-7092
   affiliation: "*, 1"
 - name: Michael Deistler
   orcid: 0000-0002-3573-0404
   affiliation: "*, 1"
 - name: Jan-Matthis Lueckmann
   orcid: 0000-0003-4320-4663
   affiliation: "*, 1"
 - name: Conor Durkan
   orcid: 0000-0001-9333-7777
   affiliation: "*, 3"
 - name: Pedro J. Gonçalves
   orcid: 0000-0002-6987-4836
   affiliation: "1, 4"
 - name: David S. Greenberg
   affiliation: "1, 5"
 - name: Marcel Nonnenmacher
   affiliation: "1, 5"
 - name: Jakob H. Macke
   orcid: 0000-0001-5154-8912
   affiliation: "1, 2, 6"
affiliations:
 - name: Equally contributing authors
   index: *
 - name: Computational Neuroengineering, Department of Electrical and Computer Engineering, Technical University of Munich
   index: 1
 - name: University of Tübingen
   index: 2
 - name: School of Informatics, University of Edinburgh
   index: 3
 - name: Max Planck Research Group Neural Systems Analysis, Center of Advanced European Studies and Research (caesar) 
   index: 4
 - name: HZG
   index: 5
 - name: Max Planck Institute for Intelligent Systems, Tübingen
   index: 6
date: 23 June 2020.
bibliography: paper.bib
---

# Summary

Scientists and engineers use numerical simulators to model empirically observed phenomena. In contrast to purely statistical models, simulators employ domain-relevant, interpretable parameters. These parameters, not all of which are known or directly measurable, are combined by the simulator with an internal source of randomness to produce its outputs.
If the parameters are well tuned, outputs will be consistent with empirical observations. Simulation-based inference (SBI) is a systematic procedure to infer the unknown parameters of the simulator so that they a) match empirical observations and b) are compatible with prior knowledge. In Bayesian terms, SBI infers a posterior distribution over the parameters of interest from a prior distribution even when an explicit likelihood is unavailable, which is frequently the case for complex simulators. The Bayesian posterior can place probability on diverse parameter combinations that may all explain a given observation, and naturally quantifies the uncertainty about them.

We present `sbi`, a PyTorch-based package that implements SBI algorithms based on neural networks. `sbi` facilitates inference on black-box simulators for practising scientists by providing a unified interface to state-of-the-art methods together with documentation and tutorials.

# Motivation

Bayesian inference is a principled approach for determining parameters consistent with empirical observations: Given a prior over parameters, a stochastic simulator, and observations, it returns a posterior distribution. In cases where the simulator reduces to a tractable probability density, many methods for approximate Bayesian inference exist [e.g.,@metropolis1953; @neal2003; @VI-papers; @le2016; @baydin2020]. For a more general simulator, however, the likelihood of parameters given data cannot be evaluated. In this 'likelihood-free' setting [@cranmer2019], traditional algorithms are based on Monte-Carlo rejection [@pritchard1999; @sisson2007], an approach referred to as _Approximate Bayesian Computation_ (ABC). More recently, novel algorithms based on neural networks have been developed [@papamakarios2016; @lueckmann2017; @papamakarios2019a; @greenberg2019] that do not reject simulations but train deep neural density estimators or classifiers for interpolation. To support these scenarios, it is desirable to be able to (re-)use sophisticated neural architectures, in particular modern flow-based density estimators [@papamakarios2019c]. For this reason `sbi` closely integrates with PyTorch and offers state-of-the-art neural network-based SBI algorithms [@papamakarios2019a; @hermans2019; @greenberg2019] with flexible choice of network architectures. With `sbi`, researchers can easily implement new neural inference methods, benefiting from the infrastructure to manage simulators and a capable posterior representation. In turn, users can profit from a unified inference interface that still allows them to use their own custom neural network or choose from a growing library of preconfigured options provided with the package.

## Related Software and use in research

There are several mature packages that implement SBI algorithms. `elfi` [@elfi2018] is a package offering BOLFI, a Gaussian process-based algorithm [@gutmann2015], and some classical ABC algorithms. The package `carl` [@louppe2016] implements the method described in @cranmer2015carl. Two other SBI packages, currently under development, are `hypothesis` [@hypothesis-repo] and `pydelfi` [@pydelfi-repo].

`sbi` is closely integrated with PyTorch [@paszke2019] and uses `nflows` [@nflows-repo] for flow-based density estimators. `sbi` builds on experience accumulated developing `delfi` [@delfi-repo], which it replaces. `delfi` was based on `theano` [@theano] (development discontinued) and was developed both for SBI research [@greenberg2019; @lueckmann2017] and for scientific applications [@goncalves2019]. The `sbi` codebase started as a fork of `lfi` [@lfi-repo], which was developed for @durkan2020. `sbi` is currently under active use both as a platform for benchmarking SBI methods as well as in diverse applications in neuroscience.

# Description 

`sbi` currently implements three families of neural inference algorithms, each with advantageous computational properties for different simulation problems:

* Sequential Neural _Posterior_ Estimation [@greenberg2019] trains a neural density estimator that directly estimates the posterior distribution,

* Sequential Neural _Likelihood_ Estimation [@papamakarios2019a] trains a deep neural density estimator of the likelihood, which then allows to sample from the posterior using e.g. MCMC,

* Sequential Neural _Ratio_ Estimation [@hermans2019; @durkan2020] trains a classifier to approximate density ratios, which in turn can be used to sample from the posterior e.g. with MCMC. 

The inference step returns a `NeuralPosterior` object that represents the uncertainty about the parameters conditional on an observation, i.e. the posterior distribution. This object can be sampled from -- and if the chosen algorithm allows, evaluated -- with the same API as a regular PyTorch probability distribution.

An important challenge in making SBI algorithms usable by a broader community is to deal with diverse, often pre-existing, complex simulators. `sbi` works with any simulator as long as it can be wrapped in a Python callable. Furthermore, `sbi` ensures that custom simulators work well with neural networks, e.g. by performing automatic shape inference, standardizing inputs or handling failed simulations. To maximize simulator performance, `sbi` leverages vectorization where available and optionally parallelizes simulations using `joblib` [@joblib]. Moreover, if dimensionality reduction of the simulator output is desired, `sbi` can use a trainable summarizing network to extract relevant features from raw simulator output, rather than the user having to hand-design these features.

In addition to the full-featured interface, `sbi` provides also a _simple_ interface which consists of a single function call with reasonable defaults. This allows new users to get familiarized with simulation-based inference and obtain quick results without having to define custom networks or tune hyperparameters.

With `sbi`, we aim to support scientific discovery by making Bayesian inference applicable to the widest class of models (simulators without a likelihood), and practical for complex problems (via neural inference). We have designed an open architecture and adopted community development practices in order to invite other machine-learning researchers to join us up in this long-term vision.

# Acknowledgements

This work has been supported by the German Federal Ministry of Education and Research (BMBF, project `ADIMEM', FKZ 01IS18052 A-D), the German Research Foundation (DFG) through  SFB 1089 `Synaptic Microcircuits', SPP 2041 `Computational Connectomics' and Germany’s Excellence Strategy – EXC-Number 2064/1 – Project number 390727645.

Conor Durkan was supported by the EPSRC Centre for Doctoral Training in Data Science, funded by the UK Engineering and Physical Sciences Research Council (grant EP/L016427/1) and the University of Edinburgh.

We are grateful to Artur Bekasov, George Papamakarios and Iain Murray for making available `nflows` [@nflows-repo], a package for normalizing flows-based density estimation which `sbi` leverages extensively.

# References
