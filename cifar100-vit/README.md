---
license: apache-2.0
base_model: google/vit-base-patch16-224-in21k
tags:
- image-classification
- vision
- generated_from_trainer
metrics:
- accuracy
model-index:
- name: cifar100-vit-base-patch16-224-in21k
  results: []
---

<!-- This model card has been generated automatically according to the information the Trainer had access to. You
should probably proofread and complete it, then remove this comment. -->

# cifar100-vit-base-patch16-224-in21k

This model is a fine-tuned version of [google/vit-base-patch16-224-in21k](https://huggingface.co/google/vit-base-patch16-224-in21k) on the cifar100 dataset.
It achieves the following results on the evaluation set:
- Loss: 0.2945
- Accuracy: 0.926

## Model description

More information needed

## Intended uses & limitations

More information needed

## Training and evaluation data

More information needed

## Training procedure

### Training hyperparameters

The following hyperparameters were used during training:
- learning_rate: 2e-05
- train_batch_size: 8
- eval_batch_size: 8
- seed: 1337
- optimizer: Adam with betas=(0.9,0.999) and epsilon=1e-08
- lr_scheduler_type: linear
- num_epochs: 10.0

### Training results

| Training Loss | Epoch | Step  | Validation Loss | Accuracy |
|:-------------:|:-----:|:-----:|:---------------:|:--------:|
| 1.3866        | 1.0   | 5313  | 1.0968          | 0.8747   |
| 0.6479        | 2.0   | 10626 | 0.4377          | 0.9004   |
| 0.6092        | 3.0   | 15939 | 0.3439          | 0.9081   |
| 0.4173        | 4.0   | 21252 | 0.3205          | 0.9169   |
| 0.4665        | 5.0   | 26565 | 0.3039          | 0.9175   |
| 0.3944        | 6.0   | 31878 | 0.3082          | 0.9201   |
| 0.303         | 7.0   | 37191 | 0.3011          | 0.9241   |
| 0.6128        | 8.0   | 42504 | 0.2983          | 0.9261   |
| 0.3794        | 9.0   | 47817 | 0.2945          | 0.926    |
| 0.3274        | 10.0  | 53130 | 0.3032          | 0.9269   |


### Framework versions

- Transformers 4.38.0
- Pytorch 2.1.2+cu118
- Datasets 2.19.1
- Tokenizers 0.15.2
