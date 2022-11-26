# AI_CUP_2022

## base line
0.729603  

## Structure  
### Preprocess  
1. retain longest answer for every id  
2. sentencize with spacy  
3. label target sentence with LCS rate above 50%  
4. extractive summarization for string length above 2000  

### Model
We put three string into one shared bert encoder and get their pooler output,  concat their combination and connect the output to differnnt tasks.

1. input string  
sentence, q(summarized), r(summarized)  
2. input features  
q_length, r_length, is_q  
3. output  
label, s  


## To be done
1. Fine-tune model  
architecture: q+r encoder?  
batch size: smaller batch size? (now 16)  
loss weight: increase weight on main task? (now 1.5)
