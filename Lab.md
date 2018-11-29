# LAB

**Q: What are the tips and tricks that could be helpful in the Lab challenge**

Here are some created by @mhendri:
-https://docs.google.com/document/d/1-MCDPOejsn2hq9EoBzMpzGv9jEdtMWoIwjkAa1cVbSM/edit#heading=h.nj23sjpj5u97

**Q: After submission of the Final Project will there be a second chance if I don’t pass?**

You can submit as many times as you like. Only the best result would be considered for your final score.

**Q: I got this error: `"RuntimeError: cuda runtime error (2) : out of memory`**

Decrease your batch size.

**Q: Will I have to save my model in CPU instead of GPU to load it properly?**

Answered by @Vittorio Nardone

>If you have already saved model checkpoint from GPU, you can try this to load it in CPU env: checkpoint = torch.load(filename, map_location=lambda storage, loc: storage)

**Q: Is it possible to see how the test-set accuracy is being calculated (not the value) There's a lot of confusion if someone uses a non-convential way to do the assignments...**
-   Unfortunately, these details can not be shared. 


