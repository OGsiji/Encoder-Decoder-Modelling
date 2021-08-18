# Encoder-Decoder-Modelling
Understanding how to use Deep Learning for Seq to Seq Networks


## Introduction:
**Sequence to Sequence (often abbreviated to seq2seq) models is a special class of Recurrent Neural Network architectures that we typically use (but not restricted) to solve complex Language problems like Machine Translation, Question Answering, creating Chatbots, Text Summarization, etc.

Encoder-Decoder Sequence to Sequence: 
![Image of Yaktocat](https://cdn.analyticsvidhya.com/wp-content/uploads/2020/08/Introduction-to-Sequence-to-Sequence-Models.jpg)
 

Use Cases of the Sequence to Sequence Models
Sequence to sequence models lies behind numerous systems that you face on a daily basis. For instance, seq2seq model powers applications like Google Translate, voice-enabled devices, and online chatbots. The following are some of the applications:

Machine translation — a 2016 paper from Google shows how the seq2seq model’s translation quality “approaches or surpasses all currently published results”.
Encoder-Decoder Sequence to Sequence : Translation

![Image of Yaktocat](https://miro.medium.com/max/638/1*s2qQ9RM27O4sa2gC1dJ0fg.png)

Speech recognition — another Google paper that compares the existing seq2seq models on the speech recognition task.
Encoder-Decoder Sequence to Sequence : Speech Recognition

![Image of Yaktocat](https://miro.medium.com/max/1000/0*QsbCJ3lGfcaBlCJf.jpg)

These are only some applications where seq2seq is seen as the best solution. This model can be used as a solution to any sequence-based problem, especially ones where the inputs and outputs have different sizes and categories.

![Image of Yaktocat](https://miro.medium.com/max/669/0*iDgmgGnrzq65dPXy.jpg)


Encoder-Decoder Architecture:
The most common architecture used to build Seq2Seq models is Encoder-Decoder architecture.

Encoder-Decoder Sequence to Sequence : Architecture

Ilya Sutskever model for Sequence to Sequence Learning with Neural Networks
As the name implies, there are two components — an encoder and a decoder.

Encoder :
Both encoder and the decoder are LSTM models (or sometimes GRU models)
Encoder reads the input sequence and summarizes the information in something called the internal state vectors or context vector (in case of LSTM these are called the hidden state and cell state vectors). We discard the outputs of the encoder and only preserve the internal states. This context vector aims to encapsulate the information for all input elements in order to help the decoder make accurate predictions.
The hidden states h_i are computed using the formula:
Encoder-Decoder Sequence to Sequence : Encoder formula

Encoder-Decoder Sequence to Sequence : Encoder

The LSTM reads the data, one sequence after the other. Thus if the input is a sequence of length ‘t’, we say that LSTM reads it in ‘t’ time steps.

1. Xi = Input sequence at time step i.

2. hi and ci = LSTM maintains two states (‘h’ for hidden state and ‘c’ for cell state) at each time step. Combined together these are internal state of the LSTM at time step i.

3. Yi = Output sequence at time step i. Yi is actually a probability distribution over the entire vocabulary which is generated by using a softmax activation. Thus each Yi is a vector of size “vocab_size” representing a probability distribution.



Decoder :
The decoder is an LSTM whose initial states are initialized to the final states of the Encoder LSTM, i.e. the context vector of the encoder’s final cell is input to the first cell of the decoder network. Using these initial states, the decoder starts generating the output sequence, and these outputs are also taken into consideration for future outputs.
A stack of several LSTM units where each predicts an output y_t at a time step t.
Each recurrent unit accepts a hidden state from the previous unit and produces and output as well as its own hidden state.
Any hidden state h_i is computed using the formula:
Encoder-Decoder Sequence to Sequence : Decoder formula

The output y_t at time step t is computed using the formula:
Encoder-Decoder Sequence to Sequence : Softmax
![Image of Yaktocat](https://miro.medium.com/max/700/1*KtWwvLK-jpGPSnj3tStg-Q.png)

We calculate the outputs using the hidden state at the current time step together with the respective weight W(S). Softmax is used to create a probability vector which will help us determine the final output (e.g. word in the question-answering problem).

We will add two tokens in the output sequence as follows:

Example:
“START_ John is hard working _END”.

The most important point is that the initial states (h0, c0) of the decoder are set to the final states of the encoder. This intuitively means that the decoder is trained to start generating the output sequence depending on the information encoded by the encoder.

Finally, the loss is calculated on the predicted outputs from each time step and the errors are backpropagated through time in order to update the parameters of the network. Training the network over a longer period with a sufficiently large amount of data results in pretty good predictions.
