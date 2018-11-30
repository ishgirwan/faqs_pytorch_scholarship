# Convolutional Neural Networks

**Q: Why use a pooling layer?**

To progressively reduce the spatial size of the representation to reduce the amount of parameters and computation in the network, and hence to also control overfitting.

Resource:

-  [cs231n - Pooling layer](http://cs231n.github.io/convolutional-networks/#pool)

**Q: When trying to run the conv_visualization in my notebook, I'm getting the error `ModuleNotFoundError: No module named 'cv2'`**

Possible solutions:

-  `pip install opencv-python`

-  `conda install -c conda-forge opencv`

**Q: Why am I getting this error: `Invalid argument 0: Sizes of tensors must match except in dimension 0. Got 499 and 442 in dimension 2 at...` ?**

Your images are not all the same size.

Possible solutions:

-  `transforms.RandomCrop(224)`

-  `transforms.RandomResizedCrop(224)`

- `transforms.Resize(224)`

- `transforms.CenterCrop(224)`

**Q: While using `transforms.Normalize`, we pass in a list of means and a list of standard deviations (std) to normalize the input color channels. How do we define means and std values and why is it 0.5 in some cases?**

Ideally, you should use the mean and standard deviation for each channel. In the case of Imagenet, you use these precalculated values `normalize = transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])`. The reason for using 0.5 in the case of mnist is to reduce complexity for the readers. Check Soumith Chintala’s comment [here]( https://discuss.pytorch.org/t/normalization-in-the-mnist-example/457/7)

**Q: In `weight=torch.from_numpy(filters).unsqueeze(1).type(torch.FloatTensor)` what does `unsqueeze(1)` mean?**

Answered by @clement:

>The reason why we do it is because we often work with 4 dimensional tensors in CNNs. And usually in the format where N 
is Batch Size and Cin is the number of channels, in this case as it is grayscale it is 1. That's the reason why we use `unsqueeze(1)` 
which introduces the dimension of 1 at the second axis. Hope this helps.

