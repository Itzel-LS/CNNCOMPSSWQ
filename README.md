CNNCOMPSSWQ

Code repository accompanying the manuscript "Comparative Evaluation of CNN
Architectures for Image-Based Classification of Suspended Solids in Water Under
Controlled Conditions."

This repository contains the code used to train and evaluate four CNN
architectures (AlexNet, SqueezeNet 1.0, MobileNetV2, and EfficientNet-B0) for
image-based classification of total suspended solids (TSS) in water, using a
sample-level, leakage-aware evaluation design.


The dataset comprises 6,515 smartphone-acquired images extracted from videos of
30 physical water samples (4 Low, 10 Medium, 16 High TSS concentration classes;
see Table 1 of the manuscript). All frames extracted from the same physical
sample are visually correlated and are therefore treated as a single grouping
unit throughout the evaluation pipeline, in order to avoid data leakage between
training and validation/holdout partitions.

Methodology overview


grid_search_groupkfold.ipynb
Of the 30 physical samples, 25 were used for a grid search over four
candidate learning rates (2×10⁻⁷, 2×10⁻⁶, 2×10⁻⁵, 2×10⁻⁴), using
GroupKFold cross-validation (k = 3) with the physical sample as the
grouping unit. This ensures that all frames belonging to a given sample
appear exclusively in either the training or the validation partition
within each fold.
final_training_evaluation.ipynb
Each architecture was retrained for 50 epochs on the complete 25-sample
development pool using its selected learning rate, and evaluated
exclusively on the 4 physical samples withheld from all stages of model
development (943 images total). This notebook also generates the
performance metrics (accuracy, precision, recall, F1-score), confusion
matrices, and computational/deployment metrics (MACs, inference latency,
VRAM usage) reported in the manuscript.


Requirements

See requirements.txt for required packages. Key dependencies:


Python 3.12.4
PyTorch
Torchvision
scikit-learn
NumPy
pandas
Pillow
tqdm

Install with:

bashpip install -r requirements.txt
Hardware used

Intel Core i7 (13th generation), 16 GB RAM, NVIDIA GeForce RTX 4060
(8 GB VRAM), CUDA 12.4, cuDNN 9.3.


