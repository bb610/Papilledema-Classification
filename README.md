# Papilledema Classification via Deep Learning

Welcome to the Papilledema Classification repository! Here, we will be using Convolutional Neural Networks (CNNs) to diagnose Papilledema from images of the back of the eye. The goal is to use the power of deep learning to accurately and non-invasively detect Papilledema (swollen optic disc) which is an indicator of intra-cranial hypertemsion.

Through this repository, you'll find a thorough breakdown of each segment of our pipeline, ranging from data preparation and augmentation to model creation, training, and validation. We aim to provide a comprehensive guide, enabling you to understand the methodologies employed and to adapt or extend them as needed.

---

## Table of Contents

1. [Data Processing](./data-processing)
2. [Model Creation](./models)
3. [Model Training](./training)
4. [Model Evaluation](./evaluation)
5. [Predictions on New Data](./predictions)
6. [Utilities and Helper Functions](./utils)
7. [Required Libraries](./required-imports.py)

---

## Data Processing

The success of a deep learning model heavily depends on the quality and structure of the data it's trained on. In this project, we've emphasized rigorous data preprocessing to ensure optimal performance.

### Highlights:

- **Data Source**: Our first dataset has been sourced from [Kim, U. (2018, August 1). Machine learning for Pseudopapilledema](https://doi.org/10.17605/OSF.IO/2W5CE). Our second dataset was sourced from [The William F. Hoyt Neuro-Ophthalmology Collection](https://novel.utah.edu/Hoyt/collection.php). We appreciate and credit the contributors for making this valuable data available.

- **Data Augmentation**: To increase the robustness of our model and counteract overfitting, we've used data augmentation techniques such as simple rotations, scaling and translation. This artificially expands the dataset by introducing minor alterations to the existing images, with the aim of increasing the extent to which the model is able to generalize to new data.

- **Normalization**: All images have been normalized to ensure consistent pixel value ranges, facilitating better and faster convergence during training.

- **Data Split**: The dataset is partitioned into training, validation, and test sets. This separation ensures that our model is evaluated on unseen data, giving a genuine measure of its performance.

- **Handling Imbalanced Data**: Special attention has been paid to handle class imbalances, ensuring that each category has a fair representation in the training process.

For a more detailed walkthrough of our data preprocessing steps and to view the code, check out the [Data Processing directory](./data-processing).

---

## Model Creation

In this section, we've used the EfficientNetB3 model, a convolutional neural network architecture that is well-regarded for its efficiency and accuracy. The steps for model creation are outlined as follows:

1. **Input Specifications**: Images are reshaped to a size of 224x224 pixels with 3 channels, representing the RGB color space.
  
2. **Base Model - EfficientNetB3**: The model is initialized without its top layers, enabling us to use its pre-trained weights from the ImageNet dataset for transfer learning. The output of the last convolutional layer is max-pooled.

3. **Custom Layers**: 
   - **Batch Normalization**: Normalizes the activations of the previous layer for a smoother training process.
   - **Dense Layer**: A fully connected layer with 256 neurons and ReLU activation function. Regularizations (both L1 and L2) are applied for better generalization.
   - **Dropout**: A dropout rate of 0.4 is used to prevent overfitting by randomly setting a fraction of input units to 0 during training.
   - **Output Layer**: A dense layer with a number of neurons corresponding to the number of classes in our dataset. The softmax activation function ensures the output values are in the range of [0,1], representing the predicted class probabilities.

4. **Model Compilation**: 
   - **Optimizer**: Adamax optimizer with a learning rate of 0.001, known for its efficiency and low memory requirements.
   - **Loss Function**: Categorical Crossentropy, suitable for multi-class classification tasks.
   - **Metrics**: Accuracy, providing a clear measure of the model's performance during training.

With this setup, the model leverages the power of transfer learning from EfficientNetB3, while also being flexible enough to cater to the specifics of our dataset through the custom layers.



