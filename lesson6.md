# Style Transfer

**Q1: What does Content Representation mean?**

Answered by @e0lithic:
>When you go to deeper layers of a convolution network then these layers represent high level features, for example at the initial layers you would have edges, however the later layers would make use of these edge to recognize shapes in the images. Hence, the layers deeper in the network usually have more precision at recognizing content rather than the background. That is what you mean by content representation. So now if you take the output of a different image from the same layer then the layer would have tried to also find similar content in the other image, and hence reducing the loss between these would result in the content of the two images becoming similar.

**Q2: What does tensor.to("cpu").clone().detach() mean?**

Answered by @shangeth:
>tensor.detach() creates a tensor that shares storage with tensor that does not require grad. 
tensor.clone() creates a copy of tensor that imitates the original tensor's requires_grad field.
You should use detach() when attempting to remove a tensor from a computation graph, and clone() as a way to copy the tensor while still keeping the copy as a part of the computation graph it came from.

**Q3: Whats the point of style transfer in relation to image classification ?**
-   Style transfer is another method other than classification. You get a stylistic ai- designed image with style transfer  whereas you can predict which class a photo belongs to with classification. Use case for style transfer could be for aesthetics reasons.

**Q4: If you are facing this error ```AttributeError: module 'PIL.Image' has no attribute 'register_extensions'```?**
-   Make sure to insall pillow, you can use this command ```!pip3 install Pillow==4.1.1```.


