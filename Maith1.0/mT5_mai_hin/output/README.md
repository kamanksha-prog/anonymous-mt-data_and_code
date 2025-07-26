---
library_name: transformers
language:
- ma
- hi
base_model: /media/kpdubey/43a28c87-1876-4ae5-a360-9029ca34f6cd/nmt/hgftransformer/checkpoints_new/mT5_mahi
tags:
- generated_from_trainer
model-index:
- name: output22
  results: []
---

<!-- This model card has been generated automatically according to the information the Trainer had access to. You
should probably proofread and complete it, then remove this comment. -->

# output22

This model is a fine-tuned version of [/media/kpdubey/43a28c87-1876-4ae5-a360-9029ca34f6cd/nmt/hgftransformer/checkpoints_new/mT5_mahi](https://huggingface.co//media/kpdubey/43a28c87-1876-4ae5-a360-9029ca34f6cd/nmt/hgftransformer/checkpoints_new/mT5_mahi) on an unknown dataset.

## Model description

More information needed

## Intended uses & limitations

More information needed

## Training and evaluation data

More information needed

## Training procedure

### Training hyperparameters

The following hyperparameters were used during training:
- learning_rate: 5e-05
- train_batch_size: 8
- eval_batch_size: 8
- seed: 42
- optimizer: Use adamw_torch with betas=(0.9,0.999) and epsilon=1e-08 and optimizer_args=No additional optimizer arguments
- lr_scheduler_type: linear
- num_epochs: 3.0

### Framework versions

- Transformers 4.53.2
- Pytorch 2.6.0+cu118
- Datasets 4.0.0
- Tokenizers 0.21.2
