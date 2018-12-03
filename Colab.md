
# Using Google Colaboratory

**Q1: How do I clone repo in my drive?**

Mount the drive using:

    from google.colab import drive
    drive.mount('/content/drive/')

  Clone the repo in your drive

    %cd /content/drive/`
    !`git clone <github repo url>


**Q2: How do I use Colab?**

Resource:
-    [Google Colab Free GPU Tutorial](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)


**Q3: I am trying to run the codes on Colab but got `AttributeError: module 'PIL.Image' has no attribute 'register_decoder'`.**

Execute `!pip install Pillow==4.1.1` and restart your notebook.


**Q4: In Colab do I need to write the lines related to cuda?**
Yes.

**Q5: How can I get the cat-dog dataset?**
Run the following commands:

    !wget "https://s3.amazonaws.com/content.udacity-data.com/nd089/Cat_Dog_data.zip" -P "pytorch_challenge/transfer_learning"

    !unzip -qq -o "pytorch_challenge/transfer_learning/Cat_Dog_data.zip" -d "pytorch_challenge/transfer_learning"`

    !ls "/content/pytorch_challenge/transfer_learning/Cat_Dog_data"

    data_dir = "/content/pytorch_challenge/transfer_learning/Cat_Dog_data"

**Q6: How can I save bandwidth at the expense of drive Storage when training my model?**

From `@ecdrid`

With your filename as `xyz.pth`, after some training:

```# Install the PyDrive wrapper & import libraries.
# This only needs to be done once in a notebook.
!pip install -U -q PyDrive

from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials

# Which file to send?
file_name = "xyz.pth" #make sure you always change this..

from googleapiclient.http import MediaFileUpload
from googleapiclient.discovery import build

auth.authenticate_user()
drive_service = build('drive', 'v3')

def save_file_to_drive(name, path):
  file_metadata = {'name': name, 'mimeType': 'application/octet-stream'}
  media = MediaFileUpload(path, mimetype='application/octet-stream', resumable=True)
  created = drive_service.files().create(body=file_metadata, media_body=media, fields='id').execute()
  return created

save_file_to_drive(file_name, file_name)
```

Now you can just connect your drive and start training further if you wish.
