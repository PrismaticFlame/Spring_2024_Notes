# [Deep Learning](../Spring_24/deep_learning.pdf)
- Deep learning accepts raw data as input and automatically learns features
- Deep learning does this using deep (3+ layers) neural networks
- The actual classifier used can be any that we have learned about, but differentiable classifiers are usually used because this allows back-propagation through the entire network
- Deep learning typically requires a massive amount of data (millions of samples) to effectively learn these features (big data)
- There are various configurations of the deep neural networks used for feature engineering – this is the variety of deep learning methods we will learn

If I create a neural network that has 100 hidden layers am I doing deep learning?

Technically, but really deep learning's goal is for feature engineering
Layers are typically connected in specific configurations to encourage the learning of features

## Popularity
- Works really well
- The rise of Big Data - storage is cheap, and we can record and save everything
- Efficient back propagation, GPUs and Tensor cores

# Encoder-Decoder
Encoder-Decoder consist of two components
1. Encoder – transforms the input into a reduced dimensionality encoded representation
2. Decoder – uses the encoded representation as input and produces some output
3. The whole system is set up as a single neural network and the encoder learns efficient encodings for the task via back-propagation
4. The encoder can be removed and used for other tasks (**transfer learning**)

# Autoencoders
One example of an Encoder-Decoder Architecture are Autoencoders
- The first known usage of autoencoders was LeCun in 1987. 
- ANNcomposed of 3 layers: input, hidden, and output
- The goal is to find a compressed data representation that minimizes data loss.
	- These are essentially compression algorithms

- Autoencoders are mainly compression algorithms
- Example applications:
	- Data Compression - for transmitting or storing data
	- Data Interpolation - if a dataset or image has some missing values, the autoencoder will likely fill in those values
	- Dimensionality reduction - for feature reduction, or even visualizing data

# Self Supervised Learning
- Auto-encoders self-supervised algorithms
- Self-supervised algorithms fall somewhere between unsupervised and supervised learning
	- Unsupervised learning – learns patterns in data without labels (input is just the data, X)
	- Supervised learning – learns to assign labels to data with labels (input is data, X and labels, Y)
- **Self-supervised algorithms** automatically generate labels (Y) from the input data (X), then learn using supervised learning methods.
	- Autoencoders learn using backward propagation. 

```Python
input_size = 784 
hidden_size = 128 
code_size = 32 
input_img = Input(shape=(input_size,)) 
hidden_1 = Dense(hidden_size, activation='relu’)(input_img) 
code = Dense(code_size, activation='relu')(hidden_1) 
hidden_2 = Dense(hidden_size, activation='relu')(code) 
output_img = Dense(input_size, activation='sigmoid')(hidden_2) 
autoencoder = Model(input_img, output_img) autoencoder.compile(optimizer='adam', loss='binary_crossentropy’)
autoencoder.fit(x_train, x_train, epochs=5)
```

## Potential Problems with this code
- Goal of the network is to minimize the error between the input and output layers
- Applying a sigmoid means that the output will be between 0 and 1
	- This implies that the input must be scaled between 0 and 1 too
		- In the article they briefly mention that they do scale their input between 0 and 1. 
		- But, this is a pretty weird thing to do. Why scale pixel values between 0 and 1?
- Using BCE as a loss function isn't really appropriate either
	- It may work, but again, its weird. 
	- You are minimizing the error between the input and output pixels
	- Do we expect the pixels to have values either 0 and 1?
	- Do the pixel values indicate any kind of probability of belonging to a class?
- This is really a regression tasks, so use Mean Squared Error (MSE) or something similar

# Encoder-Decoders
- Encoder-Decoders have two parts
	1. Encoder - represent input in some encoded (typically compressed format)
	2. Decoder - use the encoded representation as input for some task

## Encoder
- The encoder encodes data by finding weights that map it to a compressed format
- The idea is that the compression removes variation in the input to a more general representation
- The removed variation can be thought of as noise
## Decoder
- The decoder decodes the compressed format by finding weights that minimize loss
- Since the encoded representation reduces noise, ideally it makes the task of the decoder easier

# Transfer Learning
- Encoder-Decoder architectures are often used to facilitate transfer learning
- **Transfer learning** – using the weights of a model trained for one task as the starting point of the weights of a network for another task

