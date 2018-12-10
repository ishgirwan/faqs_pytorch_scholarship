# Recurrent Neural Networks

**Q: Please explain the significance of n_hidden in `nn.LSTM(input_size, n_hidden, n_layers, dropout=drop_prob, batch_first=True)`**
- Answered by @José Fernández Portal:

>n_hidden defines the size of your hidden state. The hidden state is a tensor that RNN outputs in every sequence step (t) and is the input for the next sequence step (t+1). In your diagram, it is represented by the right arrows. Basically, the hidden state carry information along the sequence. Regarding its size (n_hidden), I think that a bigger hidden state will allow to transfer more information along the sequence, but it becomes harder to train.

**Q: Are there any resources to help in the understanding of LSTM batches and sequences?**
- Answered by @sundeep:

>A helpful [video](https://slack-files.com/T3Q738VV1-F4P1VE8SY-6f4e7770d0) from course instructor Mat.

**Q: In `get_batches` is there a more elegant way of creating `y`?** 
`Character_Level_RNN_Solution.ipynb`
``` 
# The targets, shifted by one
        y = np.zeros_like(x)
        try:
            y[:, :-1], y[:, -1] = x[:, 1:], arr[:, n+seq_length]
        except IndexError:
            y[:, :-1], y[:, -1] = x[:, 1:], arr[:, 0]
```
- Try the numpy command to roll array elements along an axis `numpy.roll(a, shift, axis=None)`
```
# The targets, shifted by one
        y = np.roll(x,-1)
```
    
