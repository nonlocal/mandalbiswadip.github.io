# Neural Machine Translation by Jointly Learning to Align and Translate

Review of the Attention paper.

1. TOC
{:toc}

## Goals

  1. what is attention
  2. Why attention
  3. Why is it better than RNN
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

1) seq2seq, 2) bottleneck

## Leaning to align and translate : attention

As we have seen in the previous section that decoding the whole output sequence from a single fixed-length vector can be problematic, we can provide more info/context about all hiddens states by taking dynamically weighted average of all the hidden states of the encoder, in the following manner known as "attention":

Assume that, $(h_{1}, h_{2}, h_{3},..., h_{T})$ are the hidden states of the encoder layer.

Let the decoder layer be a generic function, 

\begin{equation} 
y_{i} = f(y_{i-1}, c_i, s_i)
\end{equation} 

where 
  
  1. y_{i-1} is the last predicted output by the decoder,
  2. $s_i$ is the current hidden state of the decoder,
  3. $c_i$ is the dynamic context vector.
  

The dynamic context vector $c_i$ is a (learnable) weighted average of all the encoder hidden states as described below:

\begin{equation} 
c_i = \sum_{j=1}^{T_{x}}\alpha_{ij}h_j.
\end{equation}

where $\alpha_{ij}$ are weightss of each hidden state $h_j$ and are given by equation

\begin{equation} 
\alpha_{ij} = \frac{\exp(e_{ij})}{\sum_{k=1}^{T_x}exp(e_ik)}
\end{equation}

where
\begin{equation} 
e_{ij} = a(s_{i-1}, h_j)
\end{equation} 

The function $a$ here is an alignment model. 

One can think of $e_{ij}$ as the unnormalized weight given to $h_j$ while calculating the linear combination of all hidden states to obtain a context vector. The context vector is further used to obtain the decoder output at ith step. So, $a$ is a function which learns how much weightage should be assigned to encoder hidden state $h_j$ when decoding $y_i$.

Let's take an example of Machine Translation from English to Spanish. Let's say we have one input sentence in `en` and the corresponding output sentence in `es`. If we are trying to translate the given input sentence, $e_{ij}$, and in turn $a_{ij}$, will tell us how much the $j_{th}$ input word is important for predicting the $i^{th}$ word in output sentence. The alignment model will learn to calculate the weights or importance from $(i-1)^{th}$ output word and $j^{th}$ input word.


what is does mathematically, graphical representation, how does it help in providing relevant context at the current decoding step, 

## Experiment

## Results

## Discussion

## Future

  1. You are given two MT tasks: `en -> de` and `fr -> es`. Without training a model, is it possible to know, which language pair model will be able to handle larger input sequences?
  
  2. If I train any rnn on large sequences as well, will it be able to handle inputs in the similar length range?
  
  3. Can I use a single attention layer after each feature extraction layer?
    
    1. A, BiLSTM ==> [BiLSTM1, A, BiLSTM2, A, BiLSTM3, A, BiLSTM4, A] # W = lower
    
    2. A, BiLSTM ==> [BiLSTM1, A1, BiLSTM2, A2, BiLSTM3, A3, BiLSTM4, A4]  # W = higher
