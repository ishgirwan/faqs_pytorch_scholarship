
# Using GOOGLE COLAB

**Q: How to clone repo in my drive?**

    Mount the drive using:

    `from google.colab import drive
    drive.mount('/content/drive/')`

    Clone the repo in your drive

    `%cd /content/drive/`

    !`git clone <github repo url>`


**Q: How to use Colab**

    Resource:
- https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d


**Q: I am trying to run the codes on Colab but got `AttributeError: module 'PIL.Image' has no attribute 'register_decoder'`.**

    Execute `!pip install Pillow==4.1.1` and restart your notebook.


**Q: In colab is it necessary to write the lines related to cuda?**

    Yes.


**Q: How can I get the cat-dog dataset?**

    Run the following commands:

    `!wget "https://s3.amazonaws.com/content.udacity-data.com/nd089/Cat_Dog_data.zip" -P "pytorch_challenge/transfer_learning"`

    `!unzip -qq -o "pytorch_challenge/transfer_learning/Cat_Dog_data.zip" -d "pytorch_challenge/transfer_learning"`

    `!ls "/content/pytorch_challenge/transfer_learning/Cat_Dog_data"`

    `data_dir = "/content/pytorch_challenge/transfer_learning/Cat_Dog_data"`
