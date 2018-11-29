# LAB

**Q: What are the tips and tricks that could be helpful in the Lab challenge**

  Here are some created by @mhendri:
    
-   https://docs.google.com/document/d/1-MCDPOejsn2hq9EoBzMpzGv9jEdtMWoIwjkAa1cVbSM/edit#heading=h.nj23sjpj5u97

**Q: After submission of the Final Project will there be a second chance if I don’t pass?**

  You can submit as many times as you like. Only the best result would be considered for your final score.

**Q: I got this error: `"RuntimeError: cuda runtime error (2) : out of memory`**

  Decrease your batch size.

**Q: Will I have to save my model in CPU instead of GPU to load it properly?**

  Answered by @Vittorio Nardone

  >If you have already saved model checkpoint from GPU, you can try this to load it in CPU env: checkpoint = torch.load(filename, map_location=lambda storage, loc: storage)

**Q: Will I have to train my model on pytorch 0.4.0 to pass the test?**

No, if you train your model on a later version of pytorch then to pass you should include strict=False when loading the state_dict, i.e. 
model.load_state_dict(checkpoint[‘state_dict’], strict=False)

