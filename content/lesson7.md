# Recurrent Neural Networks

**Q: Please explain the significance of n_hidden in `nn.LSTM(input_size, n_hidden, n_layers, dropout=drop_prob, batch_first=True)`**

Answered by @José Fernández Portal:

>n_hidden defines the size of your hidden state. The hidden state is a tensor that RNN outputs in every sequence step (t) and is the input for the next sequence step (t+1). In your diagram, it is represented by the right arrows. Basically, the hidden state carry information along the sequence. Regarding its size (n_hidden), I think that a bigger hidden state will allow to transfer more information along the sequence, but it becomes harder to train.


