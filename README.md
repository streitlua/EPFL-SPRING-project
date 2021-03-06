# Robustness & Manipulability of Interpretable Models

## General Information
This is the repository for the MSc semester project of Luã Streit at the SPRING lab.

The main objective of this project is to determine if the interpretable model __[Select-Regress-Round(SRR)](https://arxiv.org/abs/1702.04690)__ is robust and can be trusted.

SRR takes two main parameters, both integers, which are **k**, the number of features that the model is allowed to use, and **M**, the maximum possible amplitude of the weights.

_Note: The model only accepts categorical features, so any numerical features must first be binned._

We test the robustness & manipulability of the model according to 2 main criteria:
- _Adversarial examples_: Is it possible to attack the model by performing a realistic change to a datapoint and switching the model's decision? In addition, is it possible that the model weights for a feature that was originally numerical are not monotonic and allow adversarial examples?
- _Poisonining attacks_: Is it possible that slightly changing the data or parameters of the training procedure results in a model with a desired property?

### Code structure
The repository is organised as follows:
- The folder `src` contains the python source code of the project
  - `feature_selection.py` contains `forward_stepwise_regression`
  - `loader.py` contains information about the datasets, and more importantly the function `load_dataset`
  - `models.py` contains `SRR`, the Select-Regress-Round implementation, as well as two model substitutes, `SRRWithoutCrossValidation` and `RoundedLogisticRegression`
  - `preprocessing.py` contains preprocessing methods, namely `processing_pipeline`
  - `vulnerabilities.py` contains `find_adversarial_examples`, `binned_features_pass_monotonicity` and many kinds of `poisoning_attack`
- The folder `tests` contains one test file per python file in `src`, which tests the functionality of the functions in this file
- The folder `data` contains the datasets' `.csv` files:
  - There are 21 UCI datasets (retrieved from the repository of the '_Simple Rules for Complex Decisions_' paper)
  - It is here, in the folders `texas` and `ieeecis`, that you should put the texas and IEEECIS datasets (they are too large for git)

### Scripts and Notebooks
There are scripts and Jupyter Notebooks on the main directory, which allow to verify that nothing is broken, and also allow to reproduce some results:
- `adversaries.py` trains SRR on the given dataset with the specified parameters (or loads a model if it was already trained), looks for adversaries by changing only the specified columns, and outputs the adversarial examples that were found
- `all_uci_datasets.py` trains SRR on all UCI datasets, and outputs performance metrics for each of them
- `bankruptcy_monotonicity.py` checks whether SRR trained on `bankruptcy` verifies monotonicity, for many train/test splits
- `case_study.py` imitates `case_study.R` from the repository of the '_Simple Rules for Complex Decisions_' paper
- `verify_monotonicity.py` takes a dataset, k, M, and a number of tests as argument, and checks for many that many train/test splits whether the SRR models verifies monotonicity

## Requirements
Non-exhaustive list of installed conda packages:
|Name                      |Version          |         Build|
| :----------------------- | :-------------: | -----------: |
|numpy                     |1.19.1           |py38hbc911f0_0|
|pandas                    |1.1.3            |py38he6710b0_0|
|pip                       |20.2.2           |        py38_0|
|python                    |3.8.5            |    h7579374_1|
|scikit-learn              |0.23.2           |py38h0573a6f_0|
|scipy                     |1.5.2            |py38h0b6359f_0|
|statsmodels               |0.11.1           |py38h7b6447c_0|
|tqdm                      |4.49.0           |          py_0|
