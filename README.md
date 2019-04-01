# Keras implementation of Siamese Recurrent Architectures for Learning Sentence SimilarityThe Keras implementation for the paper [Siamese Recurrent Architectures for Learning Sentence Similarity](http://www.mit.edu/~jonasm/info/MuellerThyagarajan_AAAI16.pdf) which implements Siamese Architecture using LSTM to provide a state-of-the-art yet simpler model for Semantic Textual Similarity (STS) task.## Architecture:- Input: Two sentences.- Output: Semantic similarity between the input two sentences.- Sentences encoded using Word2Vec (download from [here](https://code.google.com/archive/p/word2vec/))- Siamese network.- Use one LSTM.- Distance: Manhattan distance.- Both left LSTM and right LSTM have the same weights.## Implementation Details:- The LSTM learns a mapping from the space of variable length sequences of 300 dimensional vectors into 50- Optimization of the parameters using Adadelta.- Use L1 (Manhattan distance).- LSTM takes as input embeddings of 300-dimensional word2vec.- This method do not require extensive manual feature generation beyond the separately trained word2vec vectors.- The siamese network is trained using backpropagation-through-time under the mean squared error (MSE) loss function (after rescaling the training-set relatedness labels to lie in [0, 1]).- LSTM weights initialized  with small random Gaussian entries.- Pre-training on separate sentence-pair data is provided for the earlier SemEval 2013 Semantic Textual Similarity task.## TODO:- Dataset thesaurus-based augmentation.- Learned weights visualization as provided in the paper.- We plan to provide Pytorch implementation.## Keras Implementation Notes:- Although we provide a Keras correct backend implementation to `pearson_correlation`, You shouldn't rely on `pearson_correlation` result that is returned from `evaluate`  function unless you specify a `batch_size` >= the testing set size. This is because Keras apply metrics in batchs and don't apply the metric for the whole set!- We provided implementation to `pearson_correlation` using Keras backend in order to visualize the learning curves. It gives only indications not the correct `pearson_correlation` measures. ## Training the model with SICK-like data:### Required Parameters:- ```--word2vec``` or ```-w``` Path to word2vec .bin file with 300 dims.- ```--data``` or ```-d``` Path to SICK data used for training.### Optional Parameters:- ```--pretrained``` or ```-p``` Path to pre-trained weights.- ```--epochs``` or ```-e``` Number of epochs.- ```--save``` or ```-s``` Folder path to save both the trained model and its weights.```python train.py \  --word2vec=/path/to/word2vec/GoogleNews-vectors-negative300.bin \  --data=/path/to/sick/SICK.txt \  --epochs=50```