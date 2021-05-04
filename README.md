# Image-captioning

Requirements 
1)Jupyter Notebook

DESIGN

Our model to caption images are built on multimodal recurrent and convolutional neural networks. A Convolutional Neural Network is used to extract the features from an image which is then along with the captions is fed into a Recurrent Neural Network. 

This architecture involves two main modules. The first one is image understanding module using CNN and the second one is text understanding module using LSTM. 
 
Model Structure

This may be one of the most important questions whenever developing a neural net. This question is not an easy one and can not easily be answered. A model will always be developed for a specific task, therefore no general answer can be given. However, there is some research about how to come up with a good model structure for a given task. In the field of image captioning Marc Tanti, et al. compared 16 different model architectures and determined the best one. 


This model architecture takes two vectors as inputs:

1.	image feature vector
2.	word sequence vector

As you can see, the vectors get injected into two different parts in the model. Marc Tantie, et al. came to the conclusion, that models, where the text data and the image information are handled exclusively perform better. Later in the model, both vectors get merged. Since models with an LSTM layer performed slightly better than models with RNN layer in their experiments we will go with this approach.
After the LSTM layer processed the word sequence (in the following caption prefix) its output will be merged with the image feature vector. This merge step can be realized in the ways:

1.	merge-concat: Concatenate the image feature vector and the caption prefix to one vector. The resulting vector has the length of the sum of the length of the input vectors.
2.	merge-add: Add elementwise image feature vector and caption prefix vector together. The resulting vector has the same dimensions as the input vectors.
3.	merge-mult: Multiply elementwise the image feature vector and caption prefix together. The resulting vector has the same dimensions as the input vectors.
 
A clear downside of the concatenate approach is the increase of dimensions of the resulting vector, which results in a more complex layer and requires more computational power in the end. In the following, we will go with the merge-add approach.
The last layer of the model, a softmax layer, finally outputs a probability distribution for all words in the vocabulary. In order to get the next word in the caption prefix, we only need to choose the word with the highest probability.
