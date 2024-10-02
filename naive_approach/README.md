### Overview

This contains the exploration for naive models CNN models for the classification using CIFAR10 dataset. Our naive models take the form of two-three convolutional layer followed by three fully connected layers identical to each other. Random seeds were set to ensure reproducibility of model performance. 

---
### Model Architecture 

Three models were utilised for the CIFAR10 classification. The models differed in the number of convolution layers and the kernel sizes. Three identifical fully connected layers were used for the classification. 

Model | Conv Layers | Kernel Size |
--- | --- | --- |
Model 1 | 2 Conv Layer | 5 |
Model 2 | 3 Conv Layer | 4 |
Model 3 | 3 Conv Layer | 3 |

---
### Model Evaluation

Evaluation was performed twice on each model; the first instance model was trained on the original CIFAR10 training sample, in the second instance the model was trained on augmented CIFAR10 training sample. Models trained on augmented data carry the 'aug' term in their model name.

Model | Conv Layers | Kernel Size | Training Accuracy| Validation Accuracy | 
--- | --- | --- | --- | --- |
Model 1 | 2 Conv Layer | 5 | 90.10% | 67.37% |
Model 2 | 3 Conv Layer | 4 | 80.27% | 68.93% |
Model 3 | 3 Conv Layer | 3 | 80.60% | 69.64% |
Model 1 Aug | 2 Conv Layer | 5 | 77.71% | 74.49% |
Model 2 Aug | 3 Conv Layer | 4 | 73.70% | 72.11% |
Model 3 Aug | 3 Conv Layer | 3 | 73.22% | 71.14% |

From the table above, we can observe that the shallower model (Model 1) exhibits the lowest validation accuracy on the original data sample. However, after performing data augmentation Model 1 Aug exhibits the highest validation accuracy for the CIFAR10 classification. Analysis on the training loss for the models trained on augmented data shows the validation still decreasing after 40 epochs. Therefore we will explore the models' performance on the validation at a higher epoch values (from 40 to 50). 

Model | Training Accuracy 40 Epoch | Validation Accuracy 40 Epoch | Training Accuracy 50 Epoch| Validation Accuracy 50 Epoch| 
--- | --- | --- | --- | --- |
Model 1 Aug | 77.71% | 74.49% | 78.80% | 72.55% |
Model 2 Aug | 73.70% | 72.11% | 74.46% | 71.43% |
Model 3 Aug | 73.22% | 71.14% | 75.23% | 72.15% |

Increasing the number of epochs in the training of each model resulted into a decrease in the validation accuracy in all models except for Model 3 Aug with a slight increase. The validation accuracies at 50 epochs are overall worse than the ones at 40 epochs, suggesting some a slight overfit. This observation is also backed by the plateauing of the validation loss of more models trained for 50 epochs. This observation prompts us to explore some regularization techniques to address the overfitting issue. 

Model | Training Accuracy 50 Epoch | Validation Accuracy 50 Epoch | Training Accuracy 50 Epoch with Reg| Validation Accuracy 50 Epoch with Reg| 
--- | --- | --- | --- | --- |
Model 1 Aug | 78.80% | 72.55% | 72.13% | 73.68% |
Model 2 Aug | 74.46% | 71.43% | 71.25% | 70.85% |
Model 3 Aug | 75.23% | 72.15% | 70.52% | 71.72% |

The regularisation was implemented in the form of drop out on the fully connected layer in each model trained on 50 epochs. The same drop out rate of 0.25 was used. As it can be observed in the table above, the dropout implementation only increased the validation accuracy for Model 1 Aug while it decreased the other. The best perfoming model here have a lower validation accuracy that model trained on 40 epochs without regularization (74.49%). This indicates that our chosen model architectures might not be the best suited case for us to achieve +90% classification on the CIFAR10 data. 