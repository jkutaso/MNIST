# MNIST
MNIST digit classification is a pretty basic problem that neural nets can be applied to, so I tried to do this one as well, with a bit less help from ChatGPT. It was quite straightforward. One issue that it took me a while to notice was that the final layer of my CNN was not using softmax activation (I believe it defaults to Tanh instead). This was outputting values that just aren't probabilities, so it is not answering the question it's being asked. 

It was also surprising to see that flattening the image and just using a dense model was sufficient for achieving very good results. My big fancy convolutional neural net doesn't even outperform it by much!

# How is it doing this so well?

Both of the neural nets I made are exceptional at this classification, which is crazy. To figure out how it is doing such a good job, I looked at which nodes get activated the most on average by each digit. This section is using the neural net with two intermediate layers. For each such node, I looked at the weight connecting that node to the input image and plotted the image showing the weights. 

Honestly, it is hard to interpret these images. Looking at the ones in row 0, they do in fact look like they're emphasizing a general circle around the middle. Row 23 especially seems to be highlighting the top right and bottom left quadrants of the circle. Maybe since having both of those things narrows it down to 0 or 8 and then it just needs to check the middle? Indeed two of the top three nodes are also in the top three for identifying 8. 

There's an overlapping node that is important for 2 and for 3. It sort of draws the top of a 2 (or a 3) which makes sense since the top part is similar and different from other numbers.

There is also an overlap between 0 and 3. This one seems to emphasize an area in the top right. I'm guessing it's just a quirk in the dataset that this happens to predict 0s and 3s well? 

Node 22 is important for predicting both 4s and 9s. It's unclear how it is achieving this, but it makes sense to group these together given how similar they are when handwritten. 

When looking at the net weight connecting the image to the second layer, we see a big more of a clear signal in node 66, which essentially draws a thick 3, and is indeed important for predicting 2 and 3. The other important node for predicting 2 is node 69 which seems important for distinguishing those that pass through node 66 successfully. 

The nodes that are important for predicting 5s are pretty nicely looking like a big 5. 

# Let's instead look at the weights in a one layer net 

Hopefully a simpler neural net will be more interpretable. Indeed, when removing the hidden layers we still get pretty good performance and the images of the weights represent a more intuitive representation of what the model is doing. Some of the numbers still use surprisingly vague weight images. It is possible that, for example, the images for 8 and 9 are showing us that this model is overly focused on some details that must be showing up in the training set. The top right curve appears in both 8 and 9, but it has very different weights there for the two numbers. 

