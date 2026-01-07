# Predicting Physics Observables with LHC Data  
## Machine-Learning Classification of Prompt and Non-Prompt D* Mesons

---

## Project Summary

This repository implements a complete heavy-flavor analysis pipeline for classifying reconstructed

D*+ → D0 π+

candidates into prompt, non-prompt, and background categories using decay-topology-based machine learning.

The analysis follows workflows commonly used in modern LHC experiments, combining physics-motivated feature selection with a Boosted Decision Tree (BDT) classifier. The emphasis is on physically interpretable separation rather than purely kinematic discrimination.

---

## Physics Context

At the Large Hadron Collider, reconstructed D* mesons originate from multiple sources:

- Prompt production: direct charm hadronization at the primary vertex  
- Non-prompt production: secondary charm from displaced B-hadron decays  
- Combinatorial background: random track combinations mimicking the decay topology  

Accurate separation of these components is essential for:

- charm production measurements  
- feed-down subtraction  
- precision heavy-flavor physics  

This project intentionally relies only on decay topology, closely mirroring real experimental analyses where kinematic bias must be avoided.

---

## Dataset Overview

The analysis uses three ROOT files, each corresponding to a physics class:

- Prompt_DstarToD0Pi.root  
- Nonprompt_DstarToD0Pi.root  
- Bkg_DstarToD0Pi.root  

Dataset structure:

- Each file contains a single TTree named `treeMLDstar`  
- Each entry corresponds to one reconstructed D* candidate  
- Entries represent candidates, not collision events  
- Multiple candidates may originate from the same event  

---

## Feature Space

### Topological Features (used for training)

The following variables encode decay displacement and vertex geometry:

- fCpaD0 — cosine of the 3D pointing angle  
- fCpaXYD0 — cosine of the transverse pointing angle  
- fDecayLengthXYD0 — transverse decay length  
- fImpactParameterProductD0 — impact parameter product of D0 daughters  
- fImpParamSoftPi — impact parameter of the soft pion  
- fMaxNormalisedDeltaIPD0 — maximum normalized impact-parameter deviation  

These observables are weakly dependent on momentum and provide strong discrimination between prompt, non-prompt, and background candidates.

---

### Kinematic Variables (excluded from training)

These variables are used only for validation and physics interpretation:

- fPt — transverse momentum  
- fM — D* invariant mass  
- fMD0 — D0 invariant mass  
- fInvDeltaMass — mass difference M(D*) − M(D0)  

They are intentionally excluded from training to prevent the classifier from learning trivial kinematic correlations.

---

## Machine Learning Strategy

- Model: Boosted Decision Tree (XGBoost)  
- Task: Multi-class classification (Background / Non-prompt / Prompt)  
- Train/Test split: 70% / 30%  
- Transverse momentum range: 3.67 < pT < 5.67 GeV/c  

Before training, exploratory data analysis and correlation studies are performed to validate feature behavior and independence.

---

## Performance Evaluation

Classifier performance is evaluated using ROC curves, standard in high-energy physics analyses.

Key results:

- Prompt vs Background: AUC ≈ 0.953  
- Prompt vs Non-prompt: AUC ≈ 0.875  

A physics-motivated working point is selected:

- Prompt efficiency ≈ 90%  
- Background efficiency ≈ 49.6%  
- Non-prompt efficiency ≈ 12.9%  

This operating point provides strong background rejection while retaining the majority of prompt signal.

---

## Analysis Pipeline

ROOT file inspection  
pT selection and candidate filtering  
Exploratory data analysis  
Correlation studies  
Multi-class BDT training  
ROC-based performance evaluation  
Physics-motivated working point selection  

All steps are reproducible and documented.

---

## Documentation

A detailed LaTeX report (PDF) is included, covering:

- relativistic kinematics and heavy-flavor physics  
- decay topology and vertex reconstruction  
- variable definitions  
- machine-learning methodology  
- mathematical definitions of performance metrics  
- physical interpretation of results  

The report is written to be accessible to readers new to machine learning in particle physics.

---

## Tools and Dependencies

- ROOT / uproot  
- NumPy, Pandas  
- Matplotlib  
- Scikit-learn  
- XGBoost  
- LaTeX  

---

## Possible Extensions

- Application to mixed (unknown-class) samples  
- Inclusion of particle identification (PID) variables  
- Training across multiple transverse-momentum bins  
- Systematic uncertainty studies  

---

## Author

Aryan Gupta
24b1810
Engineering Physics  
Indian Institute of Technology Bombay
