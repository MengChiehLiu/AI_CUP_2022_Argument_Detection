# AI CUP 2022: Argument Detection

* [GitHub link](https://github.com/MengChiehLiu/AI_CUP_2022)
* [AI CUP info](https://tbrain.trendmicro.com.tw/Competitions/Details/26)

## Task Description

### Input data
* q: An English discourse.
* r: An English text that responds to q.
* s: The discussion relationship between r and q.
### Output data
* 𝒒′ & 𝒓′: Subsequences of q and r respectively, and 𝑞′ and 𝑟′provides key information, enough to judge the relationship between q and r presenting s.

See more task description [here](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/data/dataset%20and%20information/%E7%AB%B6%E8%B3%BD%E4%BB%BB%E5%8B%99%E8%88%87%E8%B3%87%E6%96%99%E8%AA%AA%E6%98%8E_v2.pdf).

## Introduction

* We redefine this task into an **extractive summarization** task, which can also be regarded as a **sentence classification** task. By calculating scores for each sentence, we decompose sentences and recompose sentences with high scores into the arguments.


## Core Model Structure

![Core Model Structure](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/data/images/model_structure.jpg)

* We concat sequence with q and r into two sequences. For the maximum token length for BERT input is 512, we summarized q and r into 450 tokens at most first, which is made by using pretrained **bert-extractive-summarization** library.
After that, we feed the sequences into BERTs and get thier pooler outputs **sq** and **sr**, concating them with their inner dot production **sq*sr**. 
Finally, we connect the concated result with dense layers and get the score. Besides the main task for sequence classification, we also design a **co-task** for s(relationship) classification to help.



## Usuage
### Requirements
```
pip install -q torch pytorch-lightning
pip install -q transformers
pip install -q bert-extractive-summarizer
pip install -q nltk==3.7
```

### Model Path
https://drive.google.com/file/d/1-QVxqGodzD0FEQNVOqDsWsgHfu9fkHwO/view?usp=share_link


### Train
(Remember to change all file paths into yours!!!)

1. Download train data [here](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/data/dataset%20and%20information/Batch_answers%20-%20train_data%20(no-blank).csv).
2. Run [utils/preprocessing.ipynb](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/utils/preprocessing.ipynb) for data preprocessing. You may also just use processed data [here](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/tree/main/data/processed%20data%20(v8)).
6. Run [train.ipynb](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/train.ipynb) to start training.



### Predict
(Remember to change all file paths into yours!!!)

1. Download test data [here](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/data/dataset%20and%20information/Batch_answers%20-%20test_data(no_label).csv).
2. Download pretrained model [here](https://drive.google.com/file/d/1-QVxqGodzD0FEQNVOqDsWsgHfu9fkHwO/view?usp=share_link) or from link above.
3. Run [predict.ipynb](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/predict.ipynb) to start predicting.

## Final Scores
Our best answer is [here](https://github.com/MengChiehLiu/AI_CUP_2022_Argument_Detection/blob/main/data/answer/model_v8_old_threshold25.csv).

* Public Score: 0.815819	
* Private Score: 0.867684
