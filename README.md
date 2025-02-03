# Obliviate

Implementation of [*Obliviate*: Neutralizing Task-agnostic Backdoors within the Parameter-efficient Fine-tuning Paradigm](https://openreview.net/pdf?id=8xBMLAOZxq), 2025 NAACL (Findings)

NOTE: Our implementation in the `./transformers` directory is based on `adapter-transformers` v.3.2.1 (https://github.com/adapter-hub/adapter-transformers-legacy).

## Requirements

First, install [anaconda](https://www.anaconda.com/download)

Install python environments.
```bash
conda env create -f environments.yml -n obliviate
conda activate obliviate
```

## Download backdoored models.
Download models from this link: https://github.com/obliviateARR/Obliviate/releases/download/model/model.tar.gz

Decompress the file.
```bash
tar -zxvf model.tar.gz
```
## Run
Train and evalute PEFT models without defense
```bash
./run.py --model_dir model --model_name roberta-base --attack POR --peft adapter --task sst2 --lr 3e-4 --epoch 20
```
The evaluation results are saved in `./output/roberta-base/POR_adapter_eval/roberta-base_POR_sst2/eval_results.json`

Train and evalute PEFT models with defense
```bash
./run.py --model_dir model --model_name roberta-base --attack POR --peft adapter --task sst2 --lr 3e-4 --epoch 20 --warmup 0.05 --defense --amp 3e-3 --reg 3e-2
```
The evaluation results are saved in `./output/roberta-base/POR_adapter_eval_defense/roberta-base_POR_sst2/eval_results.json`
