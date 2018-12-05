# Lab challenge

**Q1: What are the tips and tricks that could be helpful in the Lab challenge?**
- This is a useful resource created by @mhendri : [Google doc](https://docs.google.com/document/d/1-MCDPOejsn2hq9EoBzMpzGv9jEdtMWoIwjkAa1cVbSM/edit#heading=h.nj23sjpj5u97)

For example, run all the Test code in a single cell.

**Q2: Is there any Colab setup that I can use for the Lab challenge?**

- Have a look at this [awesome setup](https://colab.research.google.com/drive/1N7r7HJ4ImgZNLXsSiuwCadVVwsGjLmFy) created by @avinash


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

**Q5: After submission of the Final Project will there be a second chance if I don’t pass?**
- You can submit as many times as you like. The best result will be considered for your final score.

**Q6: Can I see my accuracy on the test set after passing?**
- No, there is no further information available.

**Q7: I got this error: `"RuntimeError: cuda runtime error (2) : out of memory`**
- Restart your kernel and try decreasing your batch size and/or using a simpler model.

**Q8: Will I have to save my model in CPU instead of GPU to load it properly?**
- Answered by @Vittorio Nardone

  >If you have already saved model checkpoint from GPU, you can try this to load it in CPU env: 
  `checkpoint = torch.load(filename, map_location=lambda storage, loc: storage)`
  
Alternatively, you can put your model onto the CPU before saving by using `model.cpu()`

**Q9: Will I have to train my model on pytorch 0.4.0 to pass the test?**
- No, if you train your model on a later version of pytorch then to pass you should include `strict=False` when loading the `state_dict`,
i.e. `model.load_state_dict(checkpoint[‘state_dict’], strict=False)`. This ignores items added in later versions, e.g. 
`num_batches_tracked`.

**Q10: Is it possible to see how the test-set accuracy is being calculated (not the value)? There's a lot of confusion if someone uses a non-convential way to do the assignments...**
- Unfortunately, these details cannot be shared. 

**Q11: How can I use ResNet given that it does not have a classifier?**
- Put your classifier on the final layer of the model (the fully connected layer) `model.fc = classifier`

**Q12: Why don’t my image labels match the names of the flowers?**
- Note that when using `ImageFolder`the folder names are treated as character strings, so their order is 1, 10, 100, 101, 102, 11, 
12, … and the images in these respective folders are given labels 0, 1, 2, 3, 4, 5, 6, … The folder names (which here happen to be 
numbers) are treated as characters. The code in the notebook creates a `cat_to_name` dictionary of folder names and flower names. We 
then need a look-up from categories/folder names to labels, for example, by using `your_dataset.classes`.

  `class_to_idx = {sorted(your_dataset.classes)[i]: i for i in range(len(your_dataset.classes))}`

  `{k: class_to_idx[k] for k in list(class_to_idx)[:7]}`

  `{'1': 0, '10': 1, '100': 2, '101': 3, '102': 4, '11': 5, '12': 6}`


**Q13: How can I save bandwidth at the expense of drive storage when training my model using Google Colab?**

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

**Q14: In case we want to see the feedback from the evaluation of the project , will be a problem if we upload the project to get feedback from the evaluator/ mentor?**
- You are welcome to receive feedback from your classmates and Alumni Volunteers. Mentors per say are only available in the full ND program. Nonetheless, our alumni volunteers have the skills to help to out, so don't hesistate.

**Q15: Is there a public leaderboard where I can compare my final score?**

There is no official leaderboard but some students have create a [public spreadsheet](https://docs.google.com/spreadsheets/d/1eVqdzQtS4xJDO-nZB8E3PvhpSgYML5dR7Mdh5CCtt-E/edit?usp=sharing) where students can enter their scores and comapre model architectures and validation scores.  

