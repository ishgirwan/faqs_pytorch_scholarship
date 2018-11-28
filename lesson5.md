
**What is the use of pooling layer?**

Resource:
-http://cs231n.github.io/convolutional-networks/#pool

**When trying to run the conv_visualization in my notebook, I'm getting the error `ModuleNotFoundError: No module named 'cv2'`**

Possible solutions:
`pip install opencv-python`
or 
`conda install -c conda-forge opencv`

**Getting this error: `Invalid argument 0: Sizes of tensors must match except in dimension 0. Got 499 and 442 in dimension 2 at...`**

Possible solutions:

`transforms.RandomCrop(224)`
or
`transforms.RandomResizedCrop(224)`

**While using transforms.Normalize, we pass in al list of means and a list of standard deviation (std) to normalize the input color channels, how do we define means and std values and why it's 0.5 in some cases?**

Ideally you should use mean and standard deviation for each channel. In case of Imagenet, you would have different values `normalize = transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])`. The reason for using 0.5 in case mnist is to reduce complexity for the readers. Check Soumith Chintala’s comment over here https://discuss.pytorch.org/t/normalization-in-the-mnist-example/457/7

**`weight=torch.from_numpy(filters).unsqueeze(1).type(torch.FloatTensor)`What is the significance of unsqueeze(1).**

Answered by @clement:

>The reason why we do it is because, we often work with 4 dimensional tensors in CNNs. And is usually in format as shown below, where N is Batch Size, Cin is the number of channels in this case as it is grayscale it is 1. That's the reason why we use unsqueeze which introduces the dimension of 1 at the second axis. Hope this helps.




