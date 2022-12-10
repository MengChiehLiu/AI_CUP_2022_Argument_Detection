# AI CUP 2022: Argument Detection


## Task Description

### Input data
* q: An English discourse.
* r: An English text that responds to q.
* s: The discussion relationship between r and q.
### Output data
* 𝒒′ & 𝒓′: Subsequences of q and r respectively, and 𝑞′ and 𝑟′provides key information, enough to judge the relationship between q and r presenting s.

## Introduction

* We redefine this task into an **extractive summarization** task, which can also be regarded as a **sentence classification** task. By calculating scores for each sentence, we decompose sentences and recompose sentences with high scores into the arguments.


## Model Structure
* We concat sequence with q and r into two sequences. For the maximum token length for BERT input is 512, we summarized q and r into 450 tokens at most first, which is made by using pretrained **bert-extractive-summarization** library.
After that, we feed the sequences into BERTs and get thier pooler outputs **sq** and **sr**, concating them with their inner dot production **sq*sr**. 
Finally, we connect the concated result with dense layers and get the score. Besides the main task for sequence classification, we also design a **co-task** for s(relationship) classification to help.

![](https://i.imgur.com/k6wxjup.jpg)


## Model Path
https://drive.google.com/file/d/1-QVxqGodzD0FEQNVOqDsWsgHfu9fkHwO/view?usp=share_link


## Final Scores
* Public Score: 0.815819	
* Private Score: 0.867684