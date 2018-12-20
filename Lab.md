# Lab challenge

**Q1: What are the tips and tricks that could be helpful in the Lab challenge?**
- This is a super useful resource created by @mhendri : [FINAL LAB CHALLENGE - Tips, Model Performance, Submission Troubleshooting, etc](https://docs.google.com/document/d/1-MCDPOejsn2hq9EoBzMpzGv9jEdtMWoIwjkAa1cVbSM/edit#heading=h.nj23sjpj5u97). For example, a simple tip is to run all the Test code in a single cell.

- Super fast method to upload your checkpoint in Udacity's workspace create by @avinashss: [How to move our model from Google Colab to Udacity’s Workspace (final lab project)](https://medium.com/@ml_kid/how-to-move-our-model-from-google-colab-to-udacitys-workspace-final-lab-project-88e1a0b7d6ab)

- Colab notebook which shows the application of transforms, created by @ecdrid : [How transforms work](https://colab.research.google.com/drive/1iDwVOoVBkuljUadRSCChs33iNtbrI6Wv). 

- You can also refer to the medium article published by José Nieto who is a Content Developer at Udacity: [Implementing an Image Classifier with PyTorch](https://medium.com/udacity/implementing-an-image-classifier-with-pytorch-part-1-cf5444b8e9c9). 

- Applying the following methods can also help in achieving a decent validation loss:
  
  - Trying different learning rate schedulers as mentioned in the [PyTorch docs](https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate).
  - Once the network is trained, try unfreezing the weights of the complete network, then train it further for some more epochs at a very
  low learning rate.
  - Image transformations can also help in achieving a slightly higher accuracy. Refer to the [PyTorch docs](https://pytorch.org/docs/stable/torchvision/transforms.html?highlight=transforms).
  
**Q2: Is there any Google Colab setup that I can use for the Lab challenge?**

- Have a look at this [awesome setup](https://colab.research.google.com/drive/1N7r7HJ4ImgZNLXsSiuwCadVVwsGjLmFy) created by @avinash.

**Q3: Can I use transfer learning?**
- This is the recommended approach. The supplied notebook `Image Classifier Project.ipynb` states “you should use one of the pretrained
models from `torchvision.models` to get the image features.”

**Q4: How do I get the best possible model?**
- You need to select:
  *  model for transfer learning
  *  definition of your classifier
  *  batch size
  *  optimizer
  *  learning rate(s)
  *  epochs.
  
Completing the course, reading the Slack channels and reading around the subject will help with these decisions. Note the accuracy and 
loss results you get when varying these parameters and choose a combination that works well.

**Q5: What is the deadline for submission of the project? The Udacity page for this program says "This term ends on Jan 23rd".**
- The deadline is **Jan 9th**.

**Q6: What does "Duration 1 hour" mean on the Final Challenge page?**
- This is simply an estimate of the time needed to load and test your model. There is no limit on duration; you can start the lab and test
your model as many times as you wish.

**Q7: After submission of the Final Project will there be a second chance if I don’t pass?**
- You can submit as many times as you like. The best result will be considered for your final score.

**Q8: Can I see my accuracy on the test set after passing?**
- No, there is no further information available.

**Q9: I got this error: `"RuntimeError: cuda runtime error (2) : out of memory`**
- Restart your kernel and try decreasing your batch size and/or using a simpler model.

**Q10: Will I have to save my model in CPU instead of GPU to load it properly?**
- Answered by @Vittorio Nardone

  >If you have already saved model checkpoint from GPU, you can try this to load it in CPU env: 
  `checkpoint = torch.load(filename, map_location=lambda storage, loc: storage)`
  
Alternatively, you can put your model onto the CPU before saving by using `model.cpu()`

**Q11: Will I have to train my model on pytorch 0.4.0 to pass the test?**
- No, if you train your model on a later version of pytorch then to pass you should include `strict=False` when loading the `state_dict`,
i.e. `model.load_state_dict(checkpoint[‘state_dict’], strict=False)`. This ignores items added in later versions, e.g. 
`num_batches_tracked`.

**Q12: Is it possible to see how the test set accuracy is being calculated (not the value)? There's a lot of confusion if someone uses a non-convential way to do the assignments...**
- Unfortunately, these details cannot be shared. 

**Q13: How can I use ResNet given that it does not have a classifier?**
- Put your classifier on the final layer of the model (the fully connected layer) `model.fc = classifier`

**Q14: Why don’t my image labels match the names of the flowers?**
- Note that when using `ImageFolder`the folder names are treated as character strings, so their order is 1, 10, 100, 101, 102, 11, 
12, … and the images in these respective folders are given labels 0, 1, 2, 3, 4, 5, 6, … The folder names (which here happen to be 
numbers) are treated as characters. The code in the notebook creates a `cat_to_name` dictionary of folder names and flower names. We 
then need a look-up from categories/folder names to labels, for example, by using `your_dataset.classes`.

  `class_to_idx = {sorted(your_dataset.classes)[i]: i for i in range(len(your_dataset.classes))}`

  `{k: class_to_idx[k] for k in list(class_to_idx)[:7]}`

  `{'1': 0, '10': 1, '100': 2, '101': 3, '102': 4, '11': 5, '12': 6}`


**Q15: How can I save bandwidth at the expense of drive storage when training my model using Google Colab?**

- From `@ecdrid`

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

**Q16: In case we want to see the feedback from the evaluation of the project, will it be a problem if we upload the project to get feedback from the evaluator/mentor?**
- You are welcome to receive feedback from your classmates and alumni volunteers. Mentors _per se_ are only available in the full ND program. Nonetheless, our alumni volunteers have the skills to help to out, so don't hesistate.

**Q17: Is there a public leaderboard where I can compare my final score?**
- There is no official leaderboard but some students have created a [public spreadsheet](https://docs.google.com/spreadsheets/d/1eVqdzQtS4xJDO-nZB8E3PvhpSgYML5dR7Mdh5CCtt-E/edit?usp=sharing) where students can enter their scores and compare model architectures and validation scores.  

**Q18: In the final project, it says: `Here, you'll build an image classifier from scratch that will identify different species of flowers`. So, do I have to build a classifier or I can use `Transfer Learning`?**
- You can use Transfer Learning. It is stated in the Jupyter notebook of lab project that you can start with VGG.

**Q19: Since the model will run on CPUs on the Udacity server, is there any technique that we can exploit to optimize the model for CPUs instead of GPUs?**
- You could train your model faster on GPU on Colab or Kaggle or another account. Training on CPU will be very slow and boring. Then, when you want to use the same model on CPU, you will need some variable casting like `checkpoint = torch.load(filepath, map_location='cpu')`.

**Q20: How could I run my model on Google Colab, and leave it running for hours without bothering about terminations?**
- You can save checkpoints to Google Drive and load them back to continue the model training later. 

**Q21: Even with GPU, my model is taking more than 3 hours to train. Did anyone's model take longer?**
- It depends on the GPU being used and yes, this lab is a relatively computationally expensive problem in the first place. You can also check this [page](https://datascience.stackexchange.com/questions/26209/why-is-training-take-so-long-on-my-gpu) for some info.


**Q22:  Anyone encountered this error when running the assessment code for the final challenge?
```RuntimeError: cuda runtime error (35) : CUDA driver version is insufficient for CUDA runtime version at torch/csrc/cuda/Module.cpp:51```**

answer by @Clement
- This happens because the checkpoint file you saved contains parameters that was on the GPU. Udacity workspace does not allow the usage of GPU!

  To resolve this issue: In the torch.load function add an additional parameter, map_location=“cpu”.

  In other words,

  torch.load(“filepath”, map_location=“cpu”) 

