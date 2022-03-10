# BERT (KiL)

Pytorch implementation of Google AI's 2018 BERT, with simple annotation

> BERT 2018 BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding
> Paper URL : https://arxiv.org/abs/1810.04805

## Installation
```
pip install bert-pytorch
```

## Quickstart

**NOTICE : Your corpus should be prepared with two sentences in one line with tab(\t) separator**

### 0. Prepare your corpus
```
Welcome to the \t the jungle\n
I can stay \t here all night\n
```

or tokenized corpus (tokenization is not in package)
```
Wel_ _come _to _the \t _the _jungle\n
_I _can _stay \t _here _all _night\n
```


### 1. Building vocab based on your corpus
```shell
bert-vocab -c data/corpus.small -o data/vocab.small
```

### 2. Train your own BERT model
```shell
bert -c data/corpus.small -v data/vocab.small -o output/bert.model
```

## Language Model Pre-training

In the paper, authors shows the new language model training methods, 
which are "masked language model" and "predict next sentence".


### Masked Language Model 

> Original Paper : 3.3.1 Task #1: Masked LM 

```
Input Sequence  : The man went to [MASK] store with [MASK] dog
Target Sequence :                  the                his
```

#### Rules:
Randomly 15% of input token will be changed into something, based on under sub-rules

1. Randomly 80% of tokens, gonna be a `[MASK]` token
2. Randomly 10% of tokens, gonna be a `[RANDOM]` token(another word)
3. Randomly 10% of tokens, will be remain as same. But need to be predicted.

### Predict Next Sentence

> Original Paper : 3.3.2 Task #2: Next Sentence Prediction

```
Input : [CLS] the man went to the store [SEP] he bought a gallon of milk [SEP]
Label : Is Next

Input = [CLS] the man heading to the store [SEP] penguin [MASK] are flight ##less birds [SEP]
Label = NotNext
```

"Is this sentence can be continuously connected?"

 understanding the relationship, between two text sentences, which is
not directly captured by language modeling

#### Rules:

1. Randomly 50% of next sentence, gonna be continuous sentence.
2. Randomly 50% of next sentence, gonna be unrelated sentence.
