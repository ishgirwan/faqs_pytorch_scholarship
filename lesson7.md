# Recurrent Neural Networks

**Q: I found this lesson difficult to understand.  What additional resources are recommended?**

- At the beginning of the lesson Luis Serrano suggests these resources:
  
  Understanding LSTM Networks blogpost from [Chris Olah]( http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
  
  Exporing LSTMs blogpost from [Edwin Chen]( http://blog.echen.me/2017/05/30/exploring-lstms/)
  
  The  Unreasonable  Effectiveness  of  Recurrent  Neural  Networks  blogpost from [Andrej Karpathy]( http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
  
  Lecture on RNNs and LSTMs from Stanford University’s CS231by [Andrej Karpathy]( https://www.youtube.com/watch?v=iX5V1WpxxkY)

- From @Vlad:

[LSTMs from Richard Socher and Stanford NLP]( https://youtu.be/QuELiw8tbx8) for mathematical but clean explanations.

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
    
**Q: I do not see the significance of using embeddings, why can't we just use one-hot-encoding?**
- Answered by @Clement:
>Usually, the issue with sentiment analysis not being able to contextually understand words that follow one after another, results in us not using the One-Hot-Encoding technique. There are quite a few reasons why One-Hot-Encoding isn't use, e.g. Because it's a high dimensional sparse matrix - 5 words = 5x5 Matrix, 10000 words = 10000x10000 matrix - Each row of the matrix contains a vector of only one non-zero value. Also, encoding it with one-hot-encoding does not consider words that come one after another. I'm not in Lesson 8 yet. But there is a pre-processing step called "Embeddings". The embeds convert words into ids and then a vector is assigned to the individual words. And the closer words that come one after another are grouped together closely. This vector size can be chosen and is usually called the Embedding Size. Quite an interesting concept regarding text classification and sentiment analysis. It's also used in collaborative filtering, e.g. Netflix is using it to gather user preferences based on other user preference. Performance improvements are seen with this method for such problem domains.

