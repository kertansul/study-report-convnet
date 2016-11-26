# study-report-convnet

## Components in ConvNet

### Why Convolution Layer
 - Motivations: Sparse connectivity, Parameter Sharing, Equivariance to translation
 - Stided convolution = Convolution + downsampling
 - Special type: Locally connected convolutions (unshared convolution)

### non-linear Layer
 - Of course the most important, provides kernel trick
 - With conv+non-linear => exponential growth on linear regions

### Why Pooling Layer
 - Max pooling: 
   - Care more about whether some feature is present than exactly where it is
   - Invariant to small translations
   - Enlarges the maximum value's receptive field
 - Average pooling:
   - To reduce variance between hypothesys
 - Pooling over spatial vs. Pooling over features (may learn transformations)
 - Pooling is also useful for handling inputs of varying size

### Why Normalization Layer
 - Re-arrange features in order to have better activations on non-linear layer


## AlexNet
### Innovations
 - 8-layer convnet
    - Use ReLU nonlinearity
    - Training on 2 GPUs
    - Local Response Normalization (contrast normalization) => not used recently
 - Regularization
    - Data augmentation
    - Dropout

## ZFNet
### Innovations
 - Tried to visualize what AlexNet is actually learning => DeConv
 - Observing First layer problems
    - Few features dominates => renormalize weights with RMS exceeding 0.1
    - Aliasing and lack of mid-level features of AlexNet => Use a smaller filter size (11->7) and smaller stride (4->2)

### Experiments
 - Feature invariance (to translation, scaling, rotation)
 - Occlusion Sensitivity (see if the machine is learning the object or its surroundings)
 - Correspondence Analysis (check whether network can learn a hierarchy structure)
 - Varying ImageNet model size and placing SVM on top => we must have a minimum depth

## Overfeat
### Innovations
 - More about object detection (sliding window)
 - Shows the meaning of 1x1 conv 

## VGG
### Innovations
 - Investigate the effect of the convolutional network depth on its accuracy
 - Increase depth (16-19) with only 3x3 + 1x1 conv

### Conclusions
 - Stacking 3x3 convs is better than single 7x7
    - faster computation
    - more non-linearity
 - Adding 1x1 conv in between may be useful => adding a non-linear layer (NIN has a better explanasion)
 - LRN is useless
 - Initialization is important (use Xavier init)
 - Add scaling to data augmentation

## Network in Network
### Concept 
 - having too many filters for a single concept imposes extra burden on the next layer, which needs to consider all combinations of variations from the previous layer

### Innovations
 - Represents MLP (multi-layer perceptron) Layers = larger conv + 1x1 conv
 - Global average pooling before fully connected rather than pure concatenate
 - MLP can implement dropouts on top

## GoogLeNet
### Concept
 - Improved utilization of the computing resources inside the network
 - Extend a network's width + depth instead of just depth
 - Based on Hebbian principle (sparsity + clustering): neurons that fires together, wires together
    - Want to create a somewhat non-uniform sparse model for each layer
    - Use concatenate of ConvNets => small dense matrices
    - Wires together => Clustering => use 1x1 Conv
    - Think convnets in another aspect: as clustering methods rather than feature extraction

### Innovations
 - Inception module (1x1, 3x3, 5x5, 3x3 max)
 - Use 1x1 conv as a parameter reduction method (before 3x3, 5x5 conv; after 3x3 max as a clustering method)

### Architecture
 - Use avg pooling at last
 - Tried to modify features produced in the middle of the network

## ResNet
### Innovations
 - Observed the problem of training error saturation (problems brought out by ReLU)
 - Use a Residual network 
    - Gradients flow back from top
    - While network want an identity matrix, just set the non-linear functions to 0
 - Start using batch normalization

### Architecture
 - Bottleneck architecture for speed up => reading squeezenet

## Future
 - Try different non-linear function methods
 - Think about bottleneck architecture
 - Track about GoogLeNet's spare representation
