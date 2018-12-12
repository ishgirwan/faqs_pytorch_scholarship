# Introduction to Neural Networks

**Q1: I am having some trouble understanding backpropagation when training the neural net.**

  Resource:

-   [Michael Nielsen: Neural Networks and Deep Learning - Chapter 2](http://neuralnetworksanddeeplearning.com/chap2.html)
-   [Getting Started with PyTorch Part 1: Understanding how Automatic Differentiation works](https://towardsdatascience.com/getting-started-with-pytorch-part-1-understanding-how-automatic-differentiation-works-5008282073ec)

**Q2: What's the perceptron algorithm?**

  Resource:

-   [What the Hell is Perceptron?](https://towardsdatascience.com/what-the-hell-is-perceptron-626217814f53)

**Q3: How to find the optimal learning rate?**

  This paper by Leslie Smith is a great resource in finding the optimal learning rate: [A disciplined approach to neural network hyper-parameters: Part 1 -- learning rate, batch size, momentum, and weight decay](https://arxiv.org/abs/1803.09820) . You can find implementation of this paper in this blog: [Estimating an Optimal Learning Rate For a Deep Neural Network](https://towardsdatascience.com/estimating-optimal-learning-rate-for-a-deep-neural-network-ce32f2556ce0)

**Q4: What is cross entropy Loss?**

  Resource:

-   [Understanding binary cross-entropy / log loss: a visual explanation](https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a)

**Q5: What is bias?**

  Resource:

-  [Role of Bias in Neural Networks](https://stackoverflow.com/questions/2480650/role-of-bias-in-neural-networks)
-  [But what *is* a Neural Network? | Deep learning, chapter 1](https://www.youtube.com/watch?v=aircAruvnKk)

**Q6: What is Gradient Descent?**

Answered by @Clement:
>Batch Gradient Descent also just known as Gradient Descent usually loads in the entire training examples (dataset) into the network at one go and update the weights based on all the training examples. Stochastic Gradient Descent loads 1 training example at one go and update the weights using only that training example. Lastly, Mini-Batch Gradient Descent is a combination of the two. Mini-Batch Gradient descent instead of taking the entire dataset takes in N batch size. Where N is the number of training examples you can choose. These N training examples are loaded into the network and are used to update the weights once. And subsequent N batches will continue to update the weights until the entire data has been seen.


  Resource:

-  [Gradient descent, how neural networks learn | Deep learning, chapter 2](https://www.youtube.com/watch?v=IHZwWFHWa-w&t=2s)

**Q7: In softmax function why do we take exponential?**

  Resource:

-  [In softmax classifier, why use exp function to do normalization?](https://datascience.stackexchange.com/questions/23159/in-softmax-classifier-why-use-exp-function-to-do-normalization)

**Q8: Why do we need activation function?**

Answered by @Clement:
>Hi, the purpose of an activation is to introduce non-linearity into the neural network. Essentially, when we are first building Neural Networks, the formula where, y = w1x1 + w2x2 + b is a linear function, this means that it can only linearly separate data points using a line. Adding the non-linearity i.e. activation function allows the model to form different boundary instead of it just being a line.
  
  Resource:
  
-  [Activation functions and it’s types-Which is better?](https://towardsdatascience.com/activation-functions-and-its-types-which-is-better-a9a5310cc8f)

**Q9: What's the difference between np.dot() and np.matmul(),for matrix multilication and when to use them?**
  Resource: [numpy.dot vs numpy.matmul](https://stackoverflow.com/questions/34142485/difference-between-numpy-dot-and-python-3-5-matrix-multiplication)

**Q10: Having a problem with gradient descent ?**
- Here is a [tutorial](https://github.com/bhargitay/Facebook-Pytorch-Challenge-Notes/blob/master/Gradient%20Descent/Gradient_Descent.ipynb) on Gradient Descent with numpy (using the notebook provided by Udacity). *Created by @Beata.*


**Q11: Are there any notes for these lessons?**

There are notes created by our fellow scholars. You can refer to these notes through [this spreadsheet](https://docs.google.com/spreadsheets/d/1b7eD6dgWXgFuFpbWHImC5lovWLBfPR_zgaedBRA_21s/edit?usp=sharing) created and maintained by @DylanGoh.

**Q12: For the second example, where the line is described by 3x1+ 4x2 - 10 = 0, if the learning rate was set to 0.1, how many times would you have to apply the perceptron trick to move the line to a position where the blue point, at (1, 1), is correctly classified?**

Answered by: @Carlo David

-you need to apply the perceptron trick to shift it in the positive area, and count how many steps it will take,

1st step:

3(1) + 4(1) - 10 = 0

3 + 0.1 = 3.1

4 + 0.1 = 4.1

-10 + 0.1 = 9.9

then:

3.1 + 4.1 - 9.9 = -2.7, it's still negative so apply the trick again

2nd step:

3.1 + 0.1 = 3.2

4.1 + 0.1 = 4.2

-9.9 + 0.1 = 9.8

3.2 + 4.2 - 9.8 = -2.4,  it's still negative so apply the trick again

repeat the trick until it is equal or greater than 0 and count how many steps you did

**Q13: what is the functionality of dropout and how it prevents overfitting? please help me to understand the intuition of using dropout.**

Answered by: @Carlo David
- Imagine a scenario, in a classroom, a teacher asks some questions but always same two students are answering, now, the teacher asks them to stay quiet for some time and let other students participate. This way other students get to learn better. Maybe they answer wrong, but the teacher can correct them(update weights). This way the whole class(layer) learn about a topic better


- To put it loosely, dropout randomly select neurons to ignore during training, because the neurons aren't always present during training, the layer learns to use all of its inputs, improving generalization


**Q14: Why is that we can’t use values such as *0, 1* and *2* for classifying the animal as Duck, Walrus or Beaver?
Why does this assume *dependencies* between classes?**

Answered by: @Carlo David
- We can't say 0 = Duck, 1 = Walrus, 2 = Beaver, because our model think that a high number is better than a lower number, its like telling the model Beaver is better than Walrus, and Walrus is better than Duck. So we want to avoid that, instead we perform one hot encoding. It tries to avoid the natural ordered relationships, because our model will naturally give the higher numbers with higher weights.
