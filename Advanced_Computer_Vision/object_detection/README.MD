# Object Detection

&nbsp;&nbsp;&nbsp;&nbsp; Object detection is one of computer vision methods that used to detect objects on image or video. Object detection example is facial detection / recognition, counting vehicles on video and analyzing aerial imagery. Some methodologies that used to detect objects within an image:

1. Sliding Windows

&nbsp;&nbsp;&nbsp;&nbsp; sliding windows make use of rectangles that pass across the image and for each position of the sliding window, the model will classify the object in the window and ignore the rest.

2. Selective Search

&nbsp;&nbsp;&nbsp;&nbsp; The algorithm of selective search makes a number of proposals about what might contain the particular object of interest, then when an object of interest is detected, the groups where it's detected are merged until we have a single group that should bound our object pretty well.

&nbsp;&nbsp;&nbsp;&nbsp; Select the bounding box based on best IoU is called non-maximum supression. There are two stages to object detection:

1. Region proposal (sliding windows, or something else)
2. Object detection and classification

## Object Detection Architecture

### R-CNN

&nbsp;&nbsp;&nbsp;&nbsp; R-CNN is a method of using a region based CNN to implement selective search with neural networks. R-CNN works like this: 
1. first input the image, 
2. second extract region proposals (each region proposal is a grouping of smaller segments using the selective search method) the model will then propose about 2000 of these regions, 
3. third the model extracts features from each of these 2000 region proposals using pre-trained convolutional neural network and in this case using AlexNet architecture,
4. In order to adjust each region proposal to fit as the input to the R-CNN, work the image dimensions to fit the AlexNet input dimensions and this called as warped regions.
5. Classify the region, R-CNN uses support vector machine as opposed to dense layers.

### Fast R-CNN

&nbsp;&nbsp;&nbsp;&nbsp; Original R-CNN has a disadvantages like slow to running because using selective search to find the areas up to 2000 regions and this is will take more of memory because will need to have multiple classifier for each class of objects and computational expensive. 

&nbsp;&nbsp;&nbsp;&nbsp; Then fast R-CNN will change the architecture by removing selective search. The architecture of fast R-CNN:

1. first an image is fed to the network along with a set of region proposals, instead of using selective search to generate several region proposals for each image, Fast R-CNN expects these region proposals as inputs and it doesn't generate them itself.
2. The CNN processes the image and output a set of features which we call the **feature map**. It's called the feature map because the detected features are stored relative to where they're detected in the original image
3. Use the input region proposals and extract the region of interest from this feature map and create what we'll call a region proposal feature map this is called as **RoI projection**
4. Then down-sample this feature map with the help of a region of interest pooling layer to get a fixed length feature map of a consistent height and width.
5. We can then flatten the fixed size feature map into a one-dimensional vector which we call as the region of interest feature vector and create this region of interest vectory using a few fully connection layer.
6. Then we can generate the output using 2 fully connection layer which for classify the object using softmax or sigmoid and for region proposals using bbox regressor.