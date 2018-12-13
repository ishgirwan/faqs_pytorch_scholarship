# Sentiment Prediction with RNNs
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

 A: Verifing question! Still no answer.
 
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
