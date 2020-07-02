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
   affiliation: "0, 1"
 - name: Jan Boelts
   orcid: 0000-0003-4979-7092
   affiliation: "0, 1"
 - name: Michael Deistler
   orcid: 0000-0002-3573-0404
   affiliation: "0, 1"
 - name: Jan-Matthis Lueckmann
   orcid: 0000-0003-4320-4663
   affiliation: "0, 1"
 - name: Conor Durkan
   orcid: 0000-0001-9333-7777
   affiliation: "0, 3"
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
   index: 0
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
Word limit: 1000 (in the PDF).

# Summary
Scientists and engineers use numerical simulators to model empirically observed phenomena. In contrast to purely statistical models, simulators employ domain-relevant, interpretable parameters. These parameters, not all of which are known or directly measurable, are combined by the simulator with an internal source of randomness to produce its outputs.
If the parameters are well tuned, outputs will be consistent with empirical observations. Simulation-based inference (SBI) is a systematic procedure to infer the unknown parameters of the simulator so that they a) match empirical observations and b) are compatible with prior knowledge. In Bayesian terms, SBI infers a posterior distribution over the parameters of interest from a prior distribution even when an explicit likelihood is unavailable, which is frequently the case for complex simulators. The Bayesian posterior can place probability on diverse parameter combinations that may all explain a given observation, and naturally quantifies the uncertainty about them.

We present `sbi`, a PyTorch-based package that implements SBI algorithms based on neural networks. `sbi` facilitates inference on black-box simulators for practising scientists by providing a unified interface to state-of-the-art methods together with documentation and tutorials.

