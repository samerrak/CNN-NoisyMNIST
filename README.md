# CNN Ensemble for QMNIST Digit Classification

This repository implements and evaluates three custom CNN architectures (AlexNet‑inspired, LeNet‑based, and VGG16‑derived) on the QMNIST digit dataset, then combines them in an ensemble classifier to maximize accuracy. The final ensemble achieves a **98.61 %** validation accuracy and a **98.70 %** test accuracy on the public Kaggle leaderboard. 
Came in 5th/50 students.

https://www.kaggle.com/competitions/ecse-551-w-25-mp-3

---

## Project Overview

We explore convolutional neural networks for handwritten‑digit recognition on the QMNIST dataset (60 000 training images, 10 000 test images, 10 classes). Our workflow includes:

1. **Data Preparation & Augmentation**  
   • Squeeze and reshape each 28×28 image to remove singleton dimensions.  
   • Apply random rotations, shifts, and normalization only to the training set to improve generalization

2. **CNN Architectures**  
   - **Lightweight AlexNet**  
     • 3 convolutional layers (1→32, 32→64, 64→128 channels), small 3×3 kernels, batch normalization, and final pooling to 3×3 feature maps.  
     • Two fully connected layers with dropout.  
   - **Modified LeNet**  
     • Three convolutional blocks (two conv layers + batch norm each), max‑pooling to 3×3 spatial size, followed by two FC layers and dropout.  
   - **Adapted VGG16**  
     • Original VGG16 depth preserved, input resized to 48×48, five max‑pool layers halving spatial dimensions, ending with 3 FC layers modified to output 10 classes 

3. **Hyperparameter Optimization**  
   We perform grid searches for:  
   • Activation functions (ReLU)  
   • SGD learning rates (AlexNet: 0.005, LeNet: 0.001, VGG16: 0.003)  
   • Dropout rates (AlexNet: 0.7, LeNet: 0.6, VGG16: 0.3)  
   • Early stopping when validation accuracy fails to improve by at least 0.1 % over four epochs

4. **Ensemble Classifier**  
   We combine multiple models to leverage their complementary strengths:  
   - **3‑Model VGG Ensemble** (best three VGG16 variants) → 98.61 % val. accuracy  
   - **4‑Model Ensemble** (3 VGG + 1 LeNet) → 98.34 %  
   - **5‑Model Ensemble** (3 VGG + LeNet + AlexNet) → 98.50 % 

---

## Results

| Model                            | Validation Accuracy | Validation Loss |
|----------------------------------|---------------------|-----------------|
| AlexNet‑inspired                 | 97.17 %             | —               |
| Modified LeNet                   | 97.77 %             | —               |
| Adapted VGG16                    | 98.40 %             | —               |
| **3‑Model VGG Ensemble**         | **98.61 %**         | 0.0473          |
| 4‑Model Ensemble (3 VGG + LeNet) | 98.34 %             | 0.0511          |
| 5‑Model Ensemble (3 VGG + LeNet + AlexNet) | 98.50 % | 0.0487          |

The final **3‑Model VGG** ensemble also achieves **98.62 %** accuracy on the  test set 

