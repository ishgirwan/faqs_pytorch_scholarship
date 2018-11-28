# Introduction to Neural Networks

**Q: I am having some trouble understanding backpropagation when training the neural net.**

Resources:

- http://neuralnetworksanddeeplearning.com/chap2.html
- https://towardsdatascience.com/getting-started-with-pytorch-part-1-understanding-how-automatic-differentiation-works-5008282073ec

**Q: What's the perceptron algorithm?**

Resources:

- https://towardsdatascience.com/what-the-hell-is-perceptron-626217814f53

**Q: How to find the optimal learning rate?**

This paper by Leslie Smith is a great resource in finding the optimal learning rate: https://arxiv.org/abs/1803.09820 . You can find implementation of this paper in this blog:https://towardsdatascience.com/estimating-optimal-learning-rate-for-a-deep-neural-network-ce32f2556ce0

**Q: What is cross entropy Loss?**

Resources:

-https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a

**Q: What is bias?**

Resources:

-https://stackoverflow.com/questions/2480650/role-of-bias-in-neural-networks
-https://www.youtube.com/watch?v=aircAruvnKk

**Q: What is Gradient Descent?**

Resources:

-https://www.youtube.com/watch?v=IHZwWFHWa-w&t=2s

**Q: In softmax function why do we take exponential?**

Resources:

-https://datascience.stackexchange.com/questions/23159/in-softmax-classifier-why-use-exp-function-to-do-normalization

**Q: When and why is One-Hot-Encoding used?**

Ressources: 

-Quick answer: Used for multi-class-non-linear-classification. 
Essentially the error function of a multi-class-classifier can be viewed as the sum of the errors of all the seperate classifieres (= potential classes). 
That means I want the error of each data-example from each classifier. 
Thats also means I need a given true output value for each datapoint for each classifier, meaning the given output point per data-example has to transformed from a scalar containing the number of the correct class to a vector whitch one entry for each classifier (potential class). 
I.e.: if y1 = 3 and there would be 5 different possible classes it has to be converted to y1 = [0, 0, 1, 0, 0]; 

-Additional Ressources: 
https://towardsdatascience.com/smarter-ways-to-encode-categorical-data-for-machine-learning-part-1-of-3-6dca2f71b159


        
