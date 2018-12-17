# Introduction to PyTorch

**Q1: What is the use of Transfrom in dataloader?**

  Resource:
-  [torchvision.transforms](https://pytorch.org/docs/stable/torchvision/transforms.html)

**Q2: Why I'm getting this error: `AttributeError: module 'helper' has no attribute 'view_classify'`**

  You need to get helper.py file in your repository.You can get this file using following command:

    `!wget -c https://raw.githubusercontent.com/udacity/deep-learning-v2-pytorch/master/intro-to-pytorch/helper.py`


**Q3: What is the difference between: Output = model(images) and Output = model.forward(images)**

  The difference is that all the hooks are dispatched in the __call__ function, so if you call .forward and have hooks in your model, the hooks won’t have any effect. Check this discussion: [Any difference between model(input) and model.forward(input)](https://discuss.pytorch.org/t/any-different-between-model-input-and-model-forward-input/3690)

**Q4: I need help regarding transfer learning using PyTorch**

  Resource:
-  [Transfer Learning Tutorial](https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html)

**Q5: We are taking the log_softmax in forward function, so why do you compute torch.exp(model(images))**

  Answered by @Oleksandra
  > We need probabilities to pick the most probable class, for that we apply Softmax. However, because of the [computational reasons](https://docs.python.org/3/tutorial/floatingpoint.html) when dealing with probabilities, we want to deal with their Log instead. So, instead of outputting Softmax, we output LogSoftmax. The output is no longer in a probability space, but since Log is a monotonic function, we do not really care - still just picking the biggest number. Outputting LogSoftmax also works seamlessly when using NLLLoss: since NLLLoss expects scores per classes, rather than their probabilities, we wouldn’t be able to use the output of Softmax (which outputs probabilities) directly, but fortunately, we already got scores in the form of LogSoftmax! Now, to get the probabilities of the classes rather than their scores, we need to undo the Log operation on Softmax — so, we need to apply Exp.

**Q6: Could anyone tell me what is `Top-1 error` and `Top-5 error` of pre-trained networks in torchvision.models?**

Answered by @Sushil

>First, you make a prediction using the CNN and obtain the predicted class multinomial distribution (∑pclass=1).
Now, in the case of top-1 score, you check if the top class (the one having the highest probability) is the same as the target label.
In the case of top-5 score, you check if the target label is one of your top 5 predictions (the 5 ones with the highest probabilities).
In both cases, the top score is computed as the times a predicted label matched the target label, divided by the number of data-points evaluated.
Finally, when 5-CNNs are used, you first average their predictions and follow the same procedure for calculating the top-1 and top-5 scores.
Suppose your classifier gives you a probability for each class. Lets say we had only "cat", "dog", "house", "mouse" as classes (in this order). Then the classifier gives something like
0.1; 0.2; 0.0; 0.7 as a result. The Top-1 class is "mouse". The top-2 classes are {mouse, dog}. If the correct class was "dog", it would be counted as "correct" for the Top-2 accuracy, but as wrong for the Top-1 accuracy.
Hence, in a classification problem with k possible classes, every classifier has 100% top-k accuracy. The "normal" accuracy is top-1.


**Q7: What is the difference between model.fc1.weight and model.fc1.weight.data?**

Answered by @mhendri

>Both are actual weight. the difference is the data type, `fc1.weight` is an instance of `Parameter` where `fc1.weight.data` is a `Tensor`. `Parameter` is subtype/subclass of `Tensor`.

**Q8: Why have we used 256 hidden units?**

Answered by @sundeep

>There is no mathematical logic behind this number; it is just convention. You can pick your own number, or treat it as a hyperparameter and find out what is an optimal number of hidden units.

Resource:
-  [How to choose the number of hidden layers and nodes in a feedforward neural network?](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw)

**Q9: How do we determine the number of hidden layers?**

Resource:
-  [Multi-layer perceptron (MLP) architecture: criteria for choosing number of hidden layers and size of the hidden layer?](https://stackoverflow.com/questions/10565868/multi-layer-perceptron-mlp-architecture-criteria-for-choosing-number-of-hidde)

**Q10: Is there any difference between using nn.CrossEntropyLoss and the combination of nn.LogSoftmax() and nn.NLLLoss()?**

As per the [PyTorch docs](https://pytorch.org/docs/stable/nn.html?highlight=crossentropy#torch.nn.CrossEntropyLoss), there is no difference. You could also refer to this [discussion](https://discuss.pytorch.org/t/what-is-the-difference-between-using-the-cross-entropy-loss-and-using-log-softmax-followed-by-nll-loss/14825) on the Pytorch forum.


**Q11: What are PyTorch tensors?**

As per [Pytorch docs](https://pytorch.org/docs/stable/tensors.html#torch-tensor), 
>A torch.Tensor is a multi-dimensional matrix containing elements of a single data type.

If you want to know more about tensors, you could also refer to slides or handouts of 1.4, 1.5 and 1.6 of this [Deep Learning course at EPFL](https://fleuret.org/ee559/). 

**Q12: When I tried to run the model on GPU in my local machine it gave CUDA Driver Error/RuntimeError**

 Most ML Libraries require Nvidia GPU with Compute Capability 3.0 or higher. Same is for PyTorch. GoTo following link and take a look at your GPU Model Number under category, if the compute capability is less than 3.0 then you can't run on GPU. 
    Link :  https://developer.nvidia.com/cuda-gpus
    But if you want you can build PyTorch from source if you really want to run on an old GPU: https://discuss.pytorch.org/t/pytorch-version-for-cuda-compute-capability-3-0-gtx-780m/15889 . But this will not give you a high speedup due to less CUDA Cores and memory bandwidth of those old GPUs
    
**Q13: Hello, can someone explain to me what is "batch" size?**

- it is the number of samples that going to be propagated through the network. For instance, let’s say you have 1000 training samples and you want to set up batch_size equal to 100. Algorithm takes first 100 samples (from 1st to 100th) from the training dataset and trains network. Next it takes second 100 samples (from 101st to 200th) and train network again. We can keep doing this procedure until we will propagate through the networks all samples,

**Q14: After definig my classifier for transfer learning i got error when i ran the training loop 'loss.backward()' - (RuntimeError: element 0 of tensors does not require grad and does not have a grad_fn)** 

 - First make sure you attached the classifer after freezing the parameters of pretrained model, so that your classifier didn't got freezed as well.
   Second your optimizer should be something like this 
              
              optimizer = optim.SGD(model.classifier.parameters(), lr=0.01)
              
   Third problem might be that the model you are using doesn't had any classifier layer, for example resnet model have the linear layer named 'fc' in that case you need to first take a look at the layer name, then attach the classifier to that layer, so for example in case of 'fc' you should attach the classifier and define optimizer as: 
            
            model.fc=classifier
            optimizer = optim.SGD(model.fc.parameters(), lr=0.01)
 
 **Q15:transform = transforms.Compose([transforms.ToTensor(),
                               transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))])
Why do we need it, and what it do?**

Answer by: @Carlo David

Transforms are image transformations and helps us preprocess our data. They can be chained together using Compose().

Using the value 0.5 will transform it in the range of (-1,1) which helps the model learn faster, If you don't normalize your inputs between (0,1) or (-1,1) you could not equally distribute importance of each input,  thus naturally  large values become dominant according to less values during neural network training,

transforms.Normalize(mean, std)

mean=(0.5, 0.5, 0.5), std=(0.5, 0.5, 0.5), we have 3 values since its RGB 

since we used transforms.ToTensor() it will convert our input data from 0-255 to 0-1 range

we normalize it using the formula: `input = (input - mean) / std`

minimum value for input which is 0 will be converted to  (0-0.5)/0.5=-1

maximum value for input which is 1 will be converted to (1-0.5)/0.5=1



