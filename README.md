
# NotInject: Evaluating and Mitigating Over-defense in Prompt Guard Models for Robustness against Prompt Injection Attacks
[Hao Li*](https://leolee99.github.io/), [Xiaogeng Liu*](https://sheltonliu-n.github.io/)*, and [Chaowei Xiao<sup>†</sup>](https://xiaocw11.github.io/).

(*Equal Contribution, <sup>†</sup>Correspondence)

**[SaFoLab](https://safolab-wisc.github.io/), University of Wisconsin, Madison**

-----

<a href=''><img src='https://img.shields.io/badge/Paper-PDF-red'></a> 
<a href="https://huggingface.co/leolee99/NotInject"><img src="https://img.shields.io/badge/Dataset-Hugging%20Face-orange" alt="huggingface"/></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue" alt="Github license"/></a>

<!-- <a href="https://huggingface.co/leolee99/InjecGuard"><img src="https://img.shields.io/badge/Demo-%F0%9F%A4%97-yellow" alt="huggingface"/></a> -->

This repository hosts the official code, data and model weights of **InjecGuard**, the first prompt guard model against prompt injection to be built with open-source training data and detailed documentation, consistently achieving remarkable performance in benign, malicious, and over-defense accuracy.

<p align="center" width="100%">
<a target="_blank"><img src="assets/performance.png" alt="Perfomance Comparison" style="width: 60%; min-width: 200px; display: block; margin: auto;"></a>
</p>


## Abstract
Prompt injection attacks pose a critical threat to large language models (LLMs), enabling goal hijacking and data leakage. Prompt guard models, though effective in defense, suffer from over-defense—falsely flagging benign inputs as malicious due to trigger word bias. To address this issue, we introduce ***NotInject***, an evaluation dataset that systematically measures over-defense across various prompt guard models. NotInject contains 339 benign samples enriched with trigger words common in prompt injection attacks, enabling fine-grained evaluation. Our results show that state-of-the-art models suffer from over-defense issues, with accuracy dropping close to random guessing levels (60\%). To mitigate this, we propose ***InjecGuard***, a novel prompt guard model that incorporates a new training strategy, *Mitigating Over-defense for Free* (MOF), which significantly reduces the bias on trigger words. InjecGuard demonstrates state-of-the-art performance on diverse benchmarks including NotInject, surpassing the existing best model by 30.8\%, offering a robust and open-source solution for detecting prompt injection attacks.

## Demos of InjecGuard

https://github.com/user-attachments/assets/450b6176-cd6c-4e04-9a9f-16a7c53557ec


## NotInject Dataset
To address the over-defense issue commonly seen in existing guard models, we introduce the [NotInject](https://huggingface.co/datasets/leolee99/NotInject) dataset, designed to evaluate the extent of over-defense in these models. We identify certain trigger words that may cause defense shortcuts in guard models and use them to construct benign sentences. The dataset is divided into three subsets, each containing sentences with one, two, or three trigger words. For each subset, we create 113 benign sentences across four topics: Common Queries, Technique Queries, Virtual Creation, and Multilingual Queries.

<p align="center" width="100%">
<a target="_blank"><img src="assets/NotInject_distribution.png" alt="Perfomance Comparison" style="width: 90%; min-width: 200px; display: block; margin: auto;"></a>
</p>


## Requirements
We recommend the following dependencies.

* Python 3.10
* [PyTorch](http://pytorch.org/) 2.4.0

Then, please install other environment dependencies through:
```bash
pip install -r requirements.txt
```

## Getting Started

## 💾 Checkpoints

You can directly download our trained checkpoints [here](https://drive.google.com/file/d/1JpiVb_wtnbBLNEjIx1KS7PHuvmARQKTu/view?usp=sharing). 

## ⚙️ Dataset Preparation

- **Train set**: We have provided our training dataset in the path of ```InjecGuard\datasets```, collected from 20 open-source datasets and several of our LLM augmented data.

- **Valid set**: We select several samples (144) from NotInject, BIPIA, Wildguard-Injection, and PINT to conduct validation, which have been provided in the path of ```InjecGuard\datasets```.

- **Test set**: We select [NotInject](https://huggingface.co/datasets/leolee99/NotInject), [BIPIA](https://github.com/microsoft/BIPIA), [Wildguard-Benign](https://github.com/allenai/wildguard), and [PINT](https://github.com/lakeraai/pint-benchmark) to evaluate the benign, malicious, and over-defense of the model. The first three are all provided in the path of ```InjecGuard\datasets```. The benchmark of PINT is not public, but you can request access to it by filling out [here](https://share-eu1.hsforms.com/1TwiBEvLXRrCjJSdnbnHpLwfdfs3).

## 🔥 Train your InjecGuard

There are some of arguments you can set:
- ```--train_set```: the path to the train set file.
- ```--valid_set```: the path to the valid set file.
- ```--dataset_root```: the folder to place test sets.
- ```--batch_size```: you can modify it to fit your GPU memory size.
- ```--epochs```: the number of training iterations for each sample.
- ```--eval_batch_size```: The batch size in the evaluation process.
- ```--save_step```: the step interval to save models.
- ```--checkpoint_path```: you can modify it to fit your GPU memory size.
- ```--logs```: where to store logs.
- ```--max_length```: the maximum length of input tokens.
- ```--resume```: the model you want to load.
- ```--save_thres```: the performance threshold to save models, the model will only be saved when the performance exceeds the threshold.
- ```--resume```: the model you want to load.

Then, you can train InjecGuard by excuting the command:
```
python train.py
```


## 📋 Evaluation

You can evalaute the model on both 4 datasets ***(NotInject, PINT, Wildguard-Benign, BIPIA)*** by excuting the command:
```
python eval.py --resume ${CHECKPOINT}$
```

<p align="center" width="100%">
<a target="_blank"><img src="assets/Results.png" alt="Perfomance Comparison" style="width: 100%; min-width: 200px; display: block; margin: auto;"></a>
</p>

## Citation

If you find this work useful in your research or applications, we appreciate that if you can kindly cite:
```
@articles{InjecGuard,
  title={NotInject: Evaluating and Mitigating Over-defense in Prompt Guard Models for Robustness against Prompt Injection Attacks},
  author={Hao Li and Xiaogeng Liu and Chaowei Xiao},
  journal = {CoRR},
  year={2024}
}
```