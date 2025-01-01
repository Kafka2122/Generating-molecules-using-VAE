# SMILES-based VAE for Molecular Data

This project implements a Variational Autoencoder (VAE) model to process molecular data, specifically using SMILES (Simplified Molecular Input Line Entry System) representations of chemical compounds. The goal of the project is to process molecular data to extract meaningful representations for downstream tasks such as molecular property prediction.

## Project Overview
The project uses the SMILES notation of chemical compounds and a Variational Autoencoder (VAE) model to learn representations of molecular structures. The model is trained on a dataset containing various chemical properties, and the SMILES strings are used as input for the VAE to generate an embedding space for molecules.

The dataset used contains chemical data from the ChEMBL database, and includes information like molecular weight, solubility, and other molecular descriptors. 

## Requirements
To run this project, you'll need to install the following libraries:

- `numpy`
- `pandas`
- `matplotlib`
- `rdkit`
- `scikit-learn`
- `torch`
- `tqdm`

You can install the required packages using the following pip command:

```bash
pip install numpy pandas matplotlib rdkit scikit-learn torch tqdm
```
## Data Preprocessing

The dataset used in this project is a CSV file that contains molecular data. The following preprocessing steps are performed:

1. Handling Missing Data: Rows with missing values for key columns such as 'Smiles', 'Standard Value', and other chemical descriptors are removed.

2. Unit Normalization: The values are normalized based on Z-scores, focusing on 'nM' as the unit of interest.

3. SMILES Encoding: The SMILES strings are converted to one-hot encoded vectors to be used as input for the neural network model.

## Model Description

The model implemented is a Variational Autoencoder (VAE), which consists of the following components:

1. Encoder: This part takes the one-hot encoded SMILES string as input and reduces it to a lower-dimensional latent space representation.

2. Reparameterization Trick: Samples from the latent space using the mean and log variance computed by the encoder.

3. Decoder: This part reconstructs the input (SMILES) from the latent vector.

#### VAE Architecture:

1. Encoder: Fully connected layer with input size 295*56 (for SMILES encoding) and output size latent_size (default is 20).

2. Decoder: Fully connected layer that reconstructs the original SMILES string from the latent representation.

The model is trained using the Adam optimizer with a learning rate of 0.004, and the loss function combines binary cross-entropy (BCE) for reconstruction and Kullback-Leibler divergence (KLD) for regularization.
