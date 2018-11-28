
**How to clone repo in my drive?**

Mount the drive using:

`from google.colab import drive
drive.mount('/content/drive/')`

Then:

`%cd /content/drive/`

To clone the repo in your drive

!`git clone <github repo url>`

**How to use Colab**

Resource:
- https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d


**I am trying to run the codes on Colab but got `AttributeError: module 'PIL.Image' has no attribute 'register_decoder'`.**
Execute `!pip install Pillow==4.1.1` and restart your notebook.


