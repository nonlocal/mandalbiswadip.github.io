# Neural Machine Translation by Jointly Learning to Align and Translate

Review of the Attention paper.

1. TOC
{:toc}

## Goals

  1. what is attention
  2. Why attention
  3. Why is it better than LSTM
  4. Is attention the go-to architecture for seq2seq models
  5. What attention can't do
  6. Where, when, how
  7. What are "long sequences" in general? 10 elements? where does it break exactly (for rnn and for attention)? how does this threshold depend on largest sequence length in training data? 
  8. Is attention really necessary for short sequences? 
  9. Does it solve larger sequence length issue at prod?
  
  

## Introduction

Why is this different/better than tranditional translation systems? 1. end-to-end framework 2. don't need to train modules to handle different settings/contexts/conditions.

Enter encoder-decoder network



## NMT or seq2seq in general

## Leaning to align and translate : attention

## Experiment

## Results

## Discussion

## Future

  1. You are given two MT tasks: `en -> de` and `fr -> es`. Without training a model, is it possible to know, which language pair model will be able to handle larger input sequences?
  
  2. If I train any rnn on large sequences as well, will it be able to handle inputs in the similar length range?
  
  3. Can I use a single attention layer after each feature extraction layer?
    
    1. A, BiLSTM ==> [BiLSTM1, A, BiLSTM2, A, BiLSTM3, A, BiLSTM4, A] # W = lower
    
    2. A, BiLSTM ==> [BiLSTM1, A1, BiLSTM2, A2, BiLSTM3, A3, BiLSTM4, A4]  # W = higher
