# Introduction to PyTorch

**Q: What is the use of Transfrom in dataloader?**

  Resource:
-  https://pytorch.org/docs/stable/torchvision/transforms.html

**Q: Why I'm getting this error: `AttributeError: module 'helper' has no attribute 'view_classify'`**

  You need to get helper.py file in your repository.You can get this file using following command:

    `!wget -c https://raw.githubusercontent.com/udacity/deep-learning-v2-pytorch/master/intro-to-pytorch/helper.py`


**Q: What is the difference between: Output = model(images) and Output = model.forward(images)**

  The difference is that all the hooks are dispatched in the __call__ function, so if you call .forward and have hooks in your model, the hooks won’t have any effect. Check this discussion: https://discuss.pytorch.org/t/any-different-between-model-input-and-model-forward-input/3690

**Q: I need help regarding transfer learning using PyTorch**

  Resource:
-  https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html

**Q: We are taking the log_softmax in forward function, so why do you compute torch.exp(model(images))**

  Answered by @e0lithic
  >We already had probabilities from the softmax on top of which we used a log function to undo the log operation and get back the probabilities.
`exp(log(softmax)) = softmax` So, as soon as your took the softmax you got the probabilities. But we took logsoftmax , so that we could get better optmization using the error function, which was needed for backprop.But for making predictions we only needed the probabilities. Since, our networks output layer was outputting log(softmax), while we needed simply the softmax( the probablities), hence we used exp(log(softmax)) = probablities.

**Q: Could anyone tell me what is `Top-1 error` and `Top-5 error` of pre-trained networks in torchvision.models?**

Answered by @Sushil

>First, you make a prediction using the CNN and obtain the predicted class multinomial distribution (∑pclass=1).
Now, in the case of top-1 score, you check if the top class (the one having the highest probability) is the same as the target label.
In the case of top-5 score, you check if the target label is one of your top 5 predictions (the 5 ones with the highest probabilities).
In both cases, the top score is computed as the times a predicted label matched the target label, divided by the number of data-points evaluated.
Finally, when 5-CNNs are used, you first average their predictions and follow the same procedure for calculating the top-1 and top-5 scores.
Suppose your classifier gives you a probability for each class. Lets say we had only "cat", "dog", "house", "mouse" as classes (in this order). Then the classifier gives something like
0.1; 0.2; 0.0; 0.7 as a result. The Top-1 class is "mouse". The top-2 classes are {mouse, dog}. If the correct class was "dog", it would be counted as "correct" for the Top-2 accuracy, but as wrong for the Top-1 accuracy.
Hence, in a classification problem with k possible classes, every classifier has 100% top-k accuracy. The "normal" accuracy is top-1.


**Q: What is the difference between model.fc1.weight and model.fc1.weight.data?**

Answered by @mhendri

>Both are actual weight. the difference is the data type, `fc1.weight` is an instance of `Parameter` where `fc1.weight.data` is a `Tensor`. `Parameter` is subtype/subclass of `Tensor`.

**Q: Why have we used 256 hidden units**

Answered by @sundeep

>There is no mathematical logic behind this number; it is just convention. You can pick your own number, or treat it as a hyperparameter and find out what is an optimal number of hidden units.

Resource:
-  https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw

**Q: How do we determine the number of hidden layers?**

Resource:
-  https://stackoverflow.com/questions/10565868/multi-layer-perceptron-mlp-architecture-criteria-for-choosing-number-of-hidde


