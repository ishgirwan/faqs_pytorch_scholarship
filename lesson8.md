# Sentiment Prediction with RNNs
## Introduction about the lesson 08
## What is embedding layer?
 Explanation by @Clement:
 I have a nice explanation about embeddings! But first, let me talk about why there is a need for it, and how is it different from one-hot-encoding methods!
 Usually, the issue with sentiment analysis not being able to contextually understand words that follow one after another, results in us not using the One-Hot-Encoding technique as well. There are quite a few reasons why One-Hot-Encoding isn't use, e.g. Because it's a high dimensional sparse matrix - 5 words = 5x5 Matrix, 10000 words = 10000x10000 matrix - Each row of the matrix contains a vector of only one non-zero value. Also, encoding it with one-hot-encoding does not consider words that come one after another.

But there is a pre-processing step called "Embeddings". The embeds convert words into ids and then a vector is assigned to the individual words. And the closer words that come one after another are grouped together closely. This vector size can be chosen and is usually called the Embedding Size. Quite an interesting concept regarding text classification and sentiment analysis. It's also used in collaborative filtering, e.g. Netflix is using it to gather user preferences based on other user preference. Performance improvements are seen with this method for such problem domains.

Colaboration by @Mohamed Shawhy:
This video explains it in detail and how it:
works
https://www.youtube.com/watch?v=ERibwqs9p38

### Q1: CUDA error: out of memory. What should I do?

 A: Alternatives:
 
   a. Restart your kernel (jupyter notebook) and try decreasing your batch size and/or using a simpler model.
   
   b. Reduce batch size and if you are using this for NLP project, try to reduce the size of your embedding vocabulary.
   
### Q2: Explanation of the operation of the embedding layer.

 A: Explanation by @Slawek. 
 
We need to somehow numericalize our input to feed it into the network. one-hot encoding is one way of doing that, but if your vocabulary space is large as here that's super wasteful, you'd basically have a vector with a single 1 and 50000 zeroes for each word.
Instead the common practice is encode your input with so called embedding matrix - each word is represented as a vector of 300 numbers (or however many you choose) initially those vectors are initialized at random but as you train the backpropagation will change them in a way that helps with the problem you are solving. For example in this excercise you can imagine vectors for 'movie' and 'film' being similar but vectors for 'good' and 'bad' far from one another.
This technique is used not only for words, but whenever you have data that isn't numerical.

 ### Q3: In the forward function why do we reshape the output from the sigmoid function?
         # reshape to be batch_size first
        sig_out = sig_out.view(batch_size, -1)
        sig_out = sig_out[:, -1] # get last batch of labels
        
A: The output of the RNN is 3d tensor in shape of (batch_size,sequence_length,hidden_size)  so we convert it to a 2d tensor with (batch_size,sequence_length*hidden_dim) then get the last batch (the output of the last LSTM block).

 ### Q4: Explanation about comment Lesson8-11. The output tensor contains any dim of 1, how do those dim of 1 relate to empty dimension ? i.e. what do the dim 1s in the tensor represent ?
Comment: 'Output, target format 
You should also notice that, in the training loop, we are making sure that our outputs are squeezed so that they do not have an empty dimension output.squeeze()'

 A: Verifing question! Still no answer.
 
 ### Q5: Why does the following error occur?
RuntimeError: Expected tensor for argument #1 'indices' to have scalar type Long; but got CPUIntTensor insted (while checking for embedding).

 A: Check this out. See more explanations on the link below:
 https://pytorchfbchallenge.slack.com/messages/CDB3N8Q7J/convo/CE39Z196J-1544794090.207600/
 
 ### Q6: In the first notebook of lesson 8, it seems that we are removing punctuations in order to process stuff like periods and commas, but I can help and wonder whether exclamation and questions marks could be useful to indicate whether the review is useful. For example, consider something like 'this movie was sick!!'
 
 A: Verifing question! Still no answer.
 
 ### Q7: Why does the following error occur?
Unique words: 70072
Tokenized review:
IOPut data rate exceeded.

 A: You're trying to print too many items and jupyter notebook. Might be something wrong with your `reviews_ints`.
 
  ### Q8 How to decide seq_length during padding and truncating: In lesson 8.10?

 A: In the notebook "Sentiment_RNN_Exercise" Cezanne mentions that the maximum review length  was about 2500 words and that's going to be too many steps for our RNN.
Then it's necessary to truncate this data to a reasonable size and number of steps.
Cezanne mentions that a good sequence length to be around 200.
I think we should look at each situation. For this case the size of 200 looked good. In other cases an analysis should be done.

 ### Q9 In 8-3 why does  encoded_labels is of type array (np.array) and not a 'simple' list?
 A: It is easier to do this 
train_data = TensorDataset(torch.from_numpy(train_x), torch.from_numpy(train_y))

 ### Q10 Expected tensor for argument #1 'indices' to have scalar type Long; but got CPUIntTensor instead (while checking arguments for embedding). I got this error during training process. What does this error mean?
 A: You need to typecast all y/target with .long(). For example: yourTensor = yourTensor.long()

 ### Q11 I don't understand why if we don't create new variables means it will go through the whole history in training.
 A: More explanations below: 
    https://discuss.pytorch.org/t/solved-why-we-need-to-detach-variable-which-contains-hidden-representation/1426/3

 ### Q12 What is the size of lstm_out?
 A: The output of lstm is given as
output =  (h_n, c_n).
    where h_n of shape (num_layers * num_directions, batch, hidden_size)
    c_n (num_layers * num_directions, batch, hidden_size) 
    
h_n is the hidden state and c_n is the cell state

 ### Q13 In RNN why do we need to define init_hidden function here?
 
 A: the init_hidden() initializes the weights for every new batch to.

 ### Q14 What self.parameters will return?
 
 A: self.parameters returns a generator object. Therefore you use next() to iterate through the parameter weights.

 ### Q15 What is the need for a tuple of hidden layer carrying same data?
 A: In LSTM, the hidden state returns a tuple (hidden_state, cell_state)

 ### Q16 why this conditional doesnt work for me? It only enters one time and not iterational.
 A: Verify len(label_list). 
    You probably ended up with a one-element list there, maybe even a one-row matrix.

 ### Q17 what is the significance of particular embedding size?
 A: Explanation by @Rusty:
Before we discuss about what embedding layer is, let's recall first what one-hot encoding is. We use `one-hot encoding` for our labels when working with models that have more than 2 outputs. In our dataset, we have around `70000+ words`. Representing a word with a vector with size 70000 would be `computationally and memory inefficient` for us.

So we need to find a way to represent each word without using one-hot encoding. Google introduced the idea of using smaller-sized vectors to represent a word, which is now what we call `Word Embedding`. The embedding size is the size of the vector representing each word.

 ### Q18 How does the size of the embedding vector matter I mean does taking size of bigger length indicate any relevance?
 A: Explanation by @Rusty:
Bigger embedding size should result to more distinct representation of each word. Kinda like how more numbers can be represented by using more bits.
