(# This readme file is crrenlt in editing)


# DD-PRiSM
Readme file for the source code of DD-PRiSM: A Deep Learning Framework for Decomposition and Prediction of Synergistic Drug Combinations


# Packaged dependency
Matplotlib >= 3.8.0

NumPy >= 1.26.4

Pandas >= 2.2.1

SciPy >= 1.11.4

scikit-learn >= 1.4.1

pyTorch >= 2.2.0

tqdm >= 4.66.2

seaborn >= 0.13.2


# File list
There are seven iPython notebook files

- Three util-related notebooks
  - 00_Utils.ipynb: Basic functions used on the Monotherapy model and the Combination model.

    - MinMaxNormalization: Just simple minmax normalization
   
    - estimate_density: Density estimation with arbitrary precision (here, the precision was set as 2, which means the value will be rounded to the nearest hundredths)
   
    - get_weight: Calculate the density-based weight for the density-weighted loss function.
   
    - PCC: Pearson correlation coefficient on two torch tensors
   
    - MSE: Mean squared error on two torch tensors
      
    - RMSE: Root
   






  - 00_MonotherapyUtils.ipynb: The Monotherapy model and functions related to the Monotherapy model.
 
    -

  - 00_CombinationtherapyUtils.ipynb: The Combination therapy model and functions related to the Combination therapy model.
 
    -

- A Dataset-related notebook
  - 01_Preprocessing.ipynb: Links to obtain the dataset used in this study, and preprocessing steps.

    -
    
- A Monotherapy model notebook
  - 02_MonotherapyModel_Pretraining.ipynb: The pretraining of the Monotherapy model on NCI60 dataset.

    -
    
  - 03_MonotherapyModel_Finetuning.ipynb: The finetuning of the Monotherapy model on NCI-ALMANAC monotherapy dataset, that was already trained on NCI60 dataset.
 
    -
    
- A Combination therapy model notebook
  - 04_CombinationTherapyModel_Training.ipynb: The training of the combination therapy model on NCI-ALMANAC combination therapy dataset.
 
    -

