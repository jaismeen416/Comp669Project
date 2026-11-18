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

The model has a CIFAR-100 accuracy of approximately **92.62%**.

## Dataset

We evaluate on CIFAR-100-C, which contains corrupted versions of CIFAR-100 images at five severity levels.

Ground-truth labels are hidden during adaptation and are used only for evaluation.

## Baseline Results

Mean CIFAR-100-C accuracy: **79.08%**

Gaussian noise results:

| Severity | Original ViT |
|----------|--------------|
| 4 | 51.34% |
| 5 | 44.99% |

Supervised Gaussian-noise reference:

| Severity | Original ViT | Supervised Adaptation |
|----------|--------------|-----------------------|
| 4 | 51.34% | 78.65% |
| 5 | 44.99% | 76.00% |

The supervised Gaussian-noise experiment is used only as a reference to show how much recovery may be possible when labels are available. It is not the proposed unsupervised method.

## PatchStop Method

For each corrupted test image:

1. Generate multiple masked views.
2. Predict a class for each masked view.
3. Calculate prediction agreement.
4. Use the majority prediction as a pseudo-label when agreement is sufficiently high.
5. Perform one test-time adaptation update without using the ground-truth label.
6. Measure agreement again using the same evaluation masks.
7. Continue while agreement improves.
8. Stop when agreement decreases, stops improving, or the maximum adaptation budget is reached.

The key idea is that agreement is not treated as the final answer. It is used as a label-free signal for whether adaptation appears stable.

## Experimental Comparisons

We compare PatchStop against:

- Frozen ViT with no adaptation
- Single-prediction pseudo-labeling
- Masked-view adaptation with 1 update
- Masked-view adaptation with 4 updates
- Masked-view adaptation with 8 updates
- Masked-view adaptation with 16 updates
- Confidence-based stopping
- PatchStop dynamic stopping

A teacher-student baseline may also be included if feasible.

## Evaluation Metrics

We evaluate:

- Classification accuracy before and after adaptation
- Masked-view agreement
- Agreement versus correctness
- Average number of adaptation updates
- Actual runtime
- Adaptation coverage
- Failure cases
- Cases where agreement increases while the prediction remains wrong

## Main Research Questions

### RQ1
Does masked-view agreement predict whether the ViT prediction is correct?

### RQ2
Can masked-view agreement choose a better stopping point than fixed adaptation budgets such as 1, 4, 8, or 16 updates?

### RQ3
Can PatchStop maintain or improve classification accuracy while reducing unnecessary adaptation steps?

## Current Repository

- `cifar100c.ipynb` - CIFAR-100-C baseline evaluation
- `cifar100-vit/` - CIFAR-100 ViT model files
- `vit-gaussian-noise/` - supervised Gaussian-noise adapted model
- `data/` - project data
- `docs/` - research and project documentation

## Related Work

The project is informed by research on:

- **TENT** - fully test-time adaptation using entropy minimization
- **TTT-MIM** - test-time training using masked image modeling
- **AdaContrast** - pseudo-label refinement and contrastive test-time adaptation
- **Teacher-student TTA** - stability and error accumulation during adaptation
- **CIFAR-C** - evaluation of robustness under common image corruptions

## Important Failure Case

Patch agreement may increase even when the prediction is wrong.

For example, a model may initially predict the wrong class on 6 of 8 masked views and later predict that same wrong class on all 8 views.

This would mean agreement increased even though correctness did not.

Therefore, the final project explicitly studies whether agreement measures correctness or only consistency.

## Status

Completed:

- Pretrained CIFAR-100 ViT evaluation
- CIFAR-100-C baseline evaluation
- Gaussian-noise severity analysis
- Supervised Gaussian-noise reference experiment
- Related-work review
- Final experiment design

In progress:

- Single-prediction pseudo-label baseline
- Fixed 1 / 4 / 8 / 16 adaptation baselines
- PatchStop dynamic stopping
- Agreement-versus-correctness analysis
- Runtime analysis
- Failure-case analysis

## Repository

Original project repository:

`https://github.com/sathvik1808/Comp669Project`

## Authors

**Jaismeen Kaur**  
**Sathvik Reddy**
