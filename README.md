# DD-PRiSM
Readme file for the source code of DD-PRiSM: A Deep Learning Framework for Decomposition and Prediction of Synergistic Drug Combinations


# Package dependency
(The specified version of the listed packages is the version of each package that DD-PRiSM was developed, but the disagreement of version may not affect the function of the model for most packages, as we used the fundamental built-in function for most cases)

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

- Three util-related notebooks used in main notebook files
  - 00_Utils.ipynb: Basic functions used on the Monotherapy model and the Combination therapy model.

    - MinMaxNormalization: Simple min-max normalization
   
    - estimate_density: Density estimation with arbitrary precision (here, the precision was set as 2, which means the value will be rounded to the nearest hundredths)
   
    - get_weight: Calculate the density-based weight for the density-weighted loss function.
   
    - PCC: Pearson correlation coefficient on two torch tensors
   
    - MSE: Mean squared error on two torch tensors
      
    - RMSE: Root Mean squared error on two torch tensors
   
    - WeightedMSE: The MSE corrected by the sample density (dMSE in our paper)
   
    - CustomLoss (Class): The class for the loss function used in our study (sample density weighting MSE with correlation)
   
    - batch_dot: Batch-level dot product of vectors (manually defined as the built-in batch dot was too slow)
   
    - get_tensor_value: Get the value of a pyTorch tensor
   
    - Hook: The class that extracts the output value of the intermediate layer of the model
   
    - get_intermediate_output: Get the value of the intermediate layer using Hook class



  - 00_MonotherapyUtils.ipynb: The Monotherapy model and functions related to the Monotherapy model.
 
    - MonotherapyDataset (Class): The dataset class for the monotherapy treatment data (for the training of the Monotherapy model)
   
      - The function __getitem__ gives a datapoint in (features, viability) form
      
      - Features consist of the cell line feature (pathway-grouped gene expressions), the drug feature (512-bits Morgan fingerprint), and the concentration value (a scalar value)
   
    - MonotherapyDataset2device: Load a device (GPU) with sample data (features and the viability)
   
    - MonotherapyModel (Class): The Monotherapy model that takes features (=Cell line feature+Drug feature+Dosage information) and predicts the cell viability
   
    - train_mono: Train the Monotherapy model with the monotherapy dataset
   
    - test_mono: Test the Monotherapy model with the monotherapy dataset (return the loss and performance metrics)
   
    - predict_mono: predict the viability of samples in the dataset with a trained Monotherapy model (return the real viabilities and the predicted liabilities)



  - 00_CombinationtherapyUtils.ipynb: The Combination therapy model and functions related to the Combination therapy model.
 
    -　CombinationDataset (Class): The dataset class for the combination therapy treatment data (for the training of the Combination therapy model)

      - The function __getitem__ gives a datapoint in (features, viability) form
   
      - Features consist of the pathway attentions (pathway attention of monotherapy1, pathway attention of monotherapy2) and the viability of monotherapies (monotherapy1 viability, monotherapy2 viability)
   
    - CombinationDataset2device: Load a device (GPU) with sample data (features and the viability)
   
    - CombinationTherapyModel (Class): The Combination therapy model that takes features (=Pathway attention from two monotherapies+Predicted viability from two monotherapies) and predicts the combination therapy's cell viability
   
    - train_comb: Train the Combination therapy model with the combination therapy dataset
   
    - test_comb: Test the Combination therapy model with the combination therapy dataset (return the loss and performance metrics)
   
    - predict_comb: predict the viability of samples in the dataset with a trained Combination therapy model (return the real viabilities and the predicted liabilities)



- A Dataset-related notebook
  - 01_Preprocessing.ipynb: Links to obtain the dataset used in this study, and preprocessing steps.

    - Download data used in DD-PRiSM (Datasets for the training and the validation, Features, etc.)

    - All needed data will be downloaded by following the notebook step-by-step


   
- Main notebooks related to training and validation of models 
  - 02_MonotherapyModel_Pretraining.ipynb: The pretraining of the Monotherapy model on NCI60 dataset.

    - Pretrain the Monotherapy model on the NCI60 dataset downloaded in 01_Preprocessing.ipynb
   
    - The performance of the model on the test set can be evaluated with the last cell of the notebook
    
    - Change the linkage variable 'test_dataloader' to another dataloaders (cellline_dataloader/drug_dataloader/both_dataloader)

    
  - 03_MonotherapyModel_Finetuning.ipynb: The finetuning of the Monotherapy model on monotherapy data points of the NCI-ALMANAC dataset, which was already trained on the NCI60 dataset.
 
    - Fine-tune the pretrained Monotherapy model on monotherapy data points of NCI-ALMANAC dataset downloaded in 01_Preprocessing.ipynb
   
    - The performance of the model on the test set can be evaluated with the last cell of the notebook
    
    - Change the linkage variable 'test_dataloader' to another dataloaders (cellline_dataloader/drug_dataloader/both_dataloader)


    
- A Combination therapy model notebook
  - 04_CombinationTherapyModel_Training.ipynb: The training of the Combination therapy model on combination therapy data points of the NCI-ALMANAC dataset.

    - Predict the monotherapy value and extract pathway attentions of all monotherapies
    
    - Train the Combination therapy model on combination therapy data points of the NCI-ALMANAC dataset downloaded in 01_Preprocessing.ipynb
   
    - The performance of the model on the test set can be evaluated with the last cell of the notebook
    
    - Change the linkage variable 'test_dataloader' to another dataloaders (cellline_dataloader/drug1_dataloader/drug2_dataloader/both_dataloader)
