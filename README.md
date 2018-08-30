# Direct Output Connection for a High-Rank Language Model

This repository contains source files we used in our paper
>Direct Output Connection for a High-Rank Language Model

>Sho Takase, Jun Suzuki, Masaaki Nagata

>Preprint 2018

## Requirements

Python 3.5, PyTorch 0.2.0

## Download the data

```./get_data.sh```

## Train the models (to reproduce our results)

### Penn Treebank

First, train the model

```python main.py --data data/penn --dropouti 0.4 --dropoutl 0.6 --dropouth 0.225 --seed 28 --batch_size 12 --lr 20.0 --epoch 500 --nhid 960 --nhidlast 620 --emsize 280 --n_experts 15 --num4second 5 --var 0.001 --nonmono 60 --save PTB --single_gpu```

Second, finetune the model

```python finetune.py --data data/penn --dropouti 0.4 --dropoutl 0.6 --dropouth 0.225 --seed 28 --batch_size 12 --lr 20.0 --epoch 500 --var 0.001 --nonmono 60 --save PATH_TO_FOLDER --single_gpu```

where `PATH_TO_FOLDER` is the folder created by the first step (concatenation of PTB with a timestamp).

Third, run evaluation

```python cal_ppl.py  --data data/penn --save PATH_TO_FOLDER/finetune_model.pt --bptt 1000```

### WikiText-2 (Single GPU)

First, train the model

```python main.py --epochs 500 --data data/wikitext-2 --save WT2 --dropouth 0.2 --seed 1882 --n_experts 15 --num4second 5 --var 0.001 --nhid 1150 --nhidlast 650 --emsize 300 --batch_size 15 --lr 15.0 --dropoutl 0.6 --small_batch_size 5 --max_seq_len_delta 20 --dropouti 0.55 --nonmono 60 --single_gpu```

Second, finetune the model

```python finetune.py --epochs 500 --data data/wikitext-2 --save PATH_TO_FOLDER --dropouth 0.2 --seed 1882 --var 0.001 --batch_size 15 --lr 15.0 --dropoutl 0.6 --small_batch_size 5 --max_seq_len_delta 20 --dropouti 0.55 --nonmono 60 --single_gpu```

Third, run evaluation

```python cal_ppl.py --data data/wikitext-2 --save PATH_TO_FOLDER/finetune_model.pt --bptt 1000```


## Licenses

Files listed in NTT_LICENSE's EXHIBIT A are applied the NTT_LICENSE.

Other files are applied the LICENSE in this repository.

