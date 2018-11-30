# Deploying PyTorch Models
### Q:  How do I get PyTorch 1.0 for windows?

A:  On the site ( https://pytorch.org/ ) the Preview version is not available for Windows.   
You can check the discussion at the link below.  
[Pytorch](https://discuss.pytorch.org/t/installing-pytorch-nightly/29284/5)

### Q:  How to upload the model.pt for getting the test score ?

A: Click on the Upload button in the Workspace section of the lab. You can upload your file there, and then access it by name in the Test Score.ipynb file using:
torch.load('checkpoint.pt', map_location = "cpu")


