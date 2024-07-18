# MNIST
MNIST digit classification is a pretty basic problem that neural nets can be applied to, so I tried to do this one as well, with a bit less help from ChatGPT. It was quite straightforward. One issue that it took me a while to notice was that the final layer of my CNN was not using softmax activation (I believe it defaults to Tanh instead). This was outputting values that just aren't probabilities, so it is not answering the question it's being asked. 

It was also surprising to see that flattening the image and just using a dense model was sufficient for achieving very good results. My big fancy convolutional neural net doesn't even outperform it by much!
