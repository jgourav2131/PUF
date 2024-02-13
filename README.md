# Sparse PUF Linear Model 

## Overview

This documentation outlines the approach and results of developing a solver for a Sparse Physically Unclonable Function (PUF) using a sparse linear model. The Sparse PUF is characterized by a Conditional Delay Unit (CDU) chain with a subset of active units whose delays contribute to the total response time for a given challenge.

## Methodology

### Stage 1: Data Preparation

We began by loading the training and testing datasets provided, consisting of challenge-response pairs (CRPs) from a Sparse CDU PUF with 2048 total CDUs, of which only 512 are active. The active CDUs and their corresponding delays are unknown, posing a significant challenge.

### Stage 2: Model Training

The solver's core is a linear model, trained using the provided CRPs. We employed a sparse recovery technique, focusing on identifying the active CDUs and estimating their delays. The model's goal is to predict the PUF's response to unseen challenges accurately.

### Sparse Recovery Approach

Our approach utilized hard thresholding to maintain the model's sparsity constraint, ensuring that only 512 of the total 2048 coefficients are non-zero. This method aligns with the underlying structure of the Sparse PUF, where only a fraction of the CDUs are relevant to the response.

### Implementation Details

- **Hard Thresholding**: We implemented a function to perform hard thresholding on the model vector, retaining the top 512 coefficients with the highest magnitude and setting the rest to zero. This operation ensures our model remains sparse, matching the PUF's structure.
- **Model Training**: We used the `my_fit` function, encapsulating our sparse recovery logic, to train the model on the provided training CRPs. The function returns a sparse linear model that approximates the relationship between challenges and responses.
- **Evaluation Metrics**: The model's performance was evaluated using the Euclidean distance between the learned model and a "gold" model, Mean Absolute Error (MAE) on the test CRPs, and the accuracy in identifying the active CDUs.

## Results

- **Training Time**: The average training time per trial was approximately 9.37 seconds, indicating the efficiency of our implementation.
- **Model Error**: The Euclidean distance between our learned model and the gold standard averaged 238.30, suggesting room for improvement in accurately capturing the active CDUs' delays.
- **Mean Absolute Error**: The MAE on the test CRPs was remarkably low, at approximately 1.95e-07, demonstrating the model's ability to predict responses accurately.
- **Support Recovery**: The accuracy in identifying active CDUs was around 24.02%, highlighting the challenge in precisely determining which CDUs are contributing to the response.

## Conclusion

The Sparse PUF solver developed successfully predicts the PUF's responses to unseen challenges with high accuracy, as evidenced by the low MAE. However, the model's accuracy in identifying the active CDUs and the relatively high model error suggest that further refinement is needed to improve the understanding of the active CDUs' contributions. The methodology and results presented here provide a solid foundation for further research and optimization in PUF modeling and security applications.

##Please refer to the assn1.pdf for details on the problem and Notebook.ipynb for the solution
