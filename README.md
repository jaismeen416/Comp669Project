# PatchStop: Unsupervised Adaptation of Vision Transformers

**COMP 669 Project**

**Authors:** Sathvik Reddy and Jaismeen Kaur

## Research Question

Can prediction agreement across masked views provide a label-free signal for deciding when a Vision Transformer should stop adapting at test time?

## Project Overview

Vision Transformers can lose accuracy when test images differ from the data they were trained on.

This project studies test-time adaptation on corrupted CIFAR-100 images without using ground-truth labels during adaptation.

Our proposed method, PatchStop, creates multiple masked views of the same corrupted image and measures how consistently the Vision Transformer predicts the same class.

The agreement score is used as a label-free signal to determine whether adaptation should continue or stop.

## Model

We use the pretrained Hugging Face model:

`pkr7098/cifar100-vit-base-patch16-224-in21k`

The model has a CIFAR-100 accuracy of approximately 92.62%.

## Dataset

We evaluate on CIFAR-100-C, which contains corrupted versions of CIFAR-100 images at five severity levels.

## Baseline Results

Mean CIFAR-100-C accuracy: **79.08%**

Gaussian noise results:

| Severity | Original ViT |
|---|---:|
| 4 | 51.34% |
| 5 | 44.99% |

Supervised Gaussian-noise reference:

| Severity | Original ViT | Supervised Adaptation |
|---|---:|---:|
| 4 | 51.34% | 78.65% |
| 5 | 44.99% | 76.00% |

The supervised experiment is used only as a reference.

## PatchStop Method

For each corrupted test image:

1. Generate multiple masked views.
2. Predict a class for each masked view.
3. Calculate prediction agreement.
4. Use the majority prediction as a pseudo-label when agreement is high enough.
5. Perform test-time adaptation without ground-truth labels.
6. Measure agreement again using the same evaluation masks.
7. Stop when agreement decreases or stops improving.

Ground-truth labels are used only for evaluation.

## Planned Experiments

We compare:

- Frozen ViT with no adaptation
- Single-prediction pseudo-labeling
- Masked-view adaptation for 1 step
- Masked-view adaptation for 4 steps
- Masked-view adaptation for 8 steps
- Masked-view adaptation for 16 steps
- PatchStop dynamic stopping

## Evaluation

We measure:

- Classification accuracy
- Masked-view agreement
- Agreement versus correctness
- Average adaptation steps
- Runtime
- Adaptation coverage
- Failure cases where agreement increases but accuracy does not

## Current Repository

- `cifar100c.ipynb` — CIFAR-100-C baseline evaluation
- `cifar100-vit/` — CIFAR-100 ViT files
- `vit-gaussian-noise/` — Gaussian-noise adapted model
- `data/` — project data

## Related Work

- TENT: Fully Test-Time Adaptation by Entropy Minimization
- TTT-MIM: Test-Time Training with Masked Image Modeling
- AdaContrast: Contrastive Test-Time Adaptation
- Teacher-student approaches for test-time adaptation
- CIFAR-100-C robustness benchmarks

## Status

Baseline and supervised-reference experiments have been completed.

Current work focuses on implementing and evaluating the proposed unsupervised PatchStop method.