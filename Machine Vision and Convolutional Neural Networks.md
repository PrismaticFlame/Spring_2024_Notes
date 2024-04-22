# [Machine Vision](../Spring_24/machine_vision.pdf)
1. Basics
2. Machine Vision Pipeline
3. Machine Vision Features
4. Convolutional Neural Networks

# The Basics
What is an image? What is an image filter?

## Convolution (Image Filtering)
- We can define operations on images in terms of convolution
- A filter defines some mathematic operation which computes a new pixel value based on surrounding pixel values
- We represent the mathematical operation as a matrix
- For example: 

| 1/9 | 1/9 | 1/9 |
| --- | --- | --- |
| 1/9 | 1/9 | 1/9 |
| 1/9 | 1/9 | 1/9 |
An averaging filter - computes the value of the pixel at the center as the sum of all values in the matrix times 1/9

## Linear filters: 
### Mean Filter
![[mean_filter.png]]

### Identity
![[linear_filter_identity.png]]

### Shift Left
![[linear_filter_shiftLeft.png]]

### Sharpening
![[linear_filter_sharpening.png]]

# Machine Vision Pipeline
![[machine_vision_pipelline.png]]

## ROI Detection
- Often in machine vision, we are only analyzing a subset of an entire image
- ROI Detection focuses on identifying that image subset
	- Manually – crop all images at the same point (point is pre-defined)
	- Automatically - detect the ROI using machine vision

## Geometric Manipulation
Apply a geometric manipulation to an image to get it to a standardized size and orientation

Determining how to shift, rotate, etc. may be simple (e.g. check image dimensions and up-sample or down-sample to a standard size), or complicated (e.g. detect orientation and rotate to correct orientation)

- Shifting
- Rotating
- Mirroring
- Inverting
- Sampling
	- Reduce/increase image size
- Etc.

## Image Enhancement
Apply filters or operations to change pixel values
- Mean filters to reduce noise
- Sharpening filters to create better contrast
- Minimum Thresholds - Eliminate pixels which are too dim
- Maximum Thresholds - Eliminate pixels which are too bright

Remove noise by applying mean filters. Remove gray pixels with minimum thresholds Enhance contrast with a sharpening filter

### Edge Detection
- Type of image enhancement
- Example of edge detection is the Sobel filter
	- Sobel filter calculates the derivative at each pixel resulting in edges being detected
	- To calculate a horizontal and a vertical is convolved with the original image
![[sobel_filter.png]]

- There are other, more sophisticated edge detection techniques
- Use according to your needs

### Pixel Histogram Statistics
- A plot of pixel intensity
- A variety of useful features can be extracted depending on the application
- For example:
	- Average image brightness
	- Count of green pixels

### Template Matching
- Design a template for features you are interested in
- Templates are typically manually selected from images
- Center the template at each pixel and compute the similarity between the pixel in the image and the pixels in the template
- Threshold to determine if it’s a match

### Blob Detection
- Detect "blobs" = regions of an image that differ from its surroundings by some property
- Suitable for High Contrast Images
	- Or edge detection
- Many different blob detection algorithms
	- Mathematical - based on convolutions
	- Graph based - based on graph theory

#### Graph Theory - Blob Detection
- Filter an image to assign each pixel binary values 
	- e.g. apply thresholding
- Treat connected pixels as a graph
	- Pixels are connected if they are both 0 or both 1
- For each pixel, traverse the graph to find its blob

#### Statistics
- Once you have a collection of blobs in an image
- You can filter them based on templates
- Presence/absence of blob-types
- Take counts of blobs or counts of blobs that match specific templates
- Calculate blob statistics, for example:
	- average blob size, average "circular" blob size
	- Bounding box size
	- Average Blob Height

## Machine Vision Features

### Haar Features
- So far, these features have been really knowledge-based
	- Requires a lot of human thought into what features we are looking for
- Haar features compute the difference in pixel intensity in the white box vs. the black box
- This indicates the presence or absence of a feature

- Problem is, we must design the Haar features (and where they are positioned on an image)
- Haar features are automatically learned by:
	- Created low resolution images
	- Trying all combinations of features and iteratively selecting the one that gives best separation performance using a weak learning (decision stump)

- End result is a set of automatically learned features for a task
- These features compute difference in one area to difference in another

## Classification
- After all this processing and feature extraction, we should have a good set of descriptive features
	- We could create a simple rule based system:
		- e.g. If image contains this template, then it is this item
- The world isn't perfect
	- Machine learning helps us deal with variability and uncertainty
	- We know the item should contain a certain template, but what if there are imperfections in its production, problems with lighting, dirt on the item, etc..
- Items may be vary similar to one another, and single template or color match can't tell them apart
	- Detect beans from rocks - both are roundish and kind of brown. It is hard to devise an exact set of rules to tell them apart

### Example
Detect rocks in a bean processing conveyor belt

#### Processing
- Blurring to remove noise
- Sharpening to increase contrast
- Edge Detection
- Blob Detection: detect circular objects
#### Featurize
- (Histogram statistic)Average ROI color
- (Edge Detection) Smoothness (number of edges in ROI)
- (Template Matching) Bean template match percent
#### Classifier of your choice
Either
- Yes, it's a rock, eject it
- No, not a rock, keep it

# Question
- What features could we use for a face detection algorithm?
	- Blur, sharpen, edge detection
	- "eye" template
		- Maximum eye template match
	- "mouth" template
		- Maximum mouth template match
	- "face" template
		- Maximum face template match
	- Haar features

# Convolutional Neural Networks
- Haar features worked really well
	- At least for people looking directly at the camera
- We manually or automatically create image filters which create features on a certain region of the image
What if we could automatically learn informative filters and apply them to the entire image?

- **A CNN is a multilayer neural network that was biologically inspired by the animal visual cortex. **
- Early layers recognize features (such as edges), and later layers recombine these features into higher-level attributes of the input.
- LeNet = First CNN, made in 1989 by Yann LeCun
- The LeNet CNN architecture is made up of several layers that implement feature extraction and then classification (see the following image). 
	- LeNet is trained using back-propagation

- The image is divided into “receptive fields” that feed into a convolutional layer, which then extracts features from the input image. 
- The next step is pooling, which reduces the dimensionality of the extracted features (through down-sampling) while retaining the most important information (typically, through max pooling). 
- Another convolution and pooling step is then performed that feeds into a fully connected multilayer perceptron. The final output layer of this network is a set of nodes that identify features of the image (in this case, a node per identified number). 

Multi-dimensional filter?
- Remember, a filter just multiples pixel value by a weight, then takes their sum
	- So we can define filters of arbitrary size

```Python
# CNN Implementation
num_filters = 8
filter_size = 3
pool_size = 2
cnn = Sequential()
cnn.add(Conv2D(num_filters, filter_size, input_shape=(28, 28, 1)))
cnn.add(MaxPooling2D(pool_size=pool_size))
cnn.add(Flatten())
cnn.add(Dense(10,activation='softmax'))
```


# State of the art in Machine Vision
- AlexNet
- VGGNet
	- ![[vggNet.png]]
- ResNet
	- Residual connections increase performance!
- GoogLeNet
	- New state of the art


## Residual Neural Networks
- Vanishing Gradient
	- Adding more layers alone caused rapid degradation
- Solution
	- Skip (residual) connection to pass forward identity mappings
	- Add this to the weights produced from convolution layers