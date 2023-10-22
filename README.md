# Goal Line Detection

## Dataset

The goal of this project is to use models such as Linear Discriminant Analysis, Artificial Neural Networks and Convolutional Neural Networks for Binary Image Classification.

The models will be used to find whether a football near a goal line is in goal or not.


![Screenshot 2023-10-22 182700](https://github.com/akshayravi13/Goal-Line-Detection-Football/assets/85955796/6f0875cd-4c3a-49be-851a-41674a49037b)


The dataset contains 40 images which were clicked manually.

There are 20 cases of goal and 20 cases of no goal.

Although the dataset is small, the aim of this project is not to create a high-performance model, but rather to study how these models work and what features they extract from an image for predicting their class.

The dataset is split into two sets - 32 images for training and 8 images for testing.
The models read the data as flattened numpy arrays.

## Models

### Linear Discriminant Analysis
LDA can classify the given data into two classes by finding an axis to which maximizes separability between classes and minimizes variance within a class.
Find out more about LDA [here](https://www.youtube.com/watch?v=azXCzI57Yfc&t=536s) 

Each pixel of the image is considered as a feature. With each feature as an axis, LDA will project these features onto a single axis which will help to separate the two classes in the best way. The great thing about LDA is that it brings the information from these thousands of features onto a single axis and hence it’s a dimensionality reduction technique as well as a supervised learning method for classification tasks.

Sklearn library is used for this model. After fitting the model on the training data, it provides the option of getting the coefficients (weights) assigned to each feature/pixel. The linear composite of these weights will form the axis which separates the two classes. By visualizing these coefficients as a heatmap, we can observe how the model sees the images.


![Screenshot 2023-10-22 182837](https://github.com/akshayravi13/Goal-Line-Detection-Football/assets/85955796/db77f653-f525-4428-93c0-d33d67f9125e)



The LDA model is generally able to see the placement where the football and goal-line are present. The accuracy of this model is 75%, but that isn’t the concern of this project.

### Artificial Neural Network

The ANN is created with 4 dense layers and the last layer has 1 neuron with sigmoid activation for the purpose of binary classification. If you are not familiar with ANN architecture, find out more about it [here](https://www.youtube.com/watch?v=CqOfi41LfDw&t=6s)

The input features are very high since they are the flattened image array. There are 256*256 = 65536 features which means the number of parameters in the ANN is also very high.


![Screenshot 2023-10-22 173006](https://github.com/akshayravi13/Goal-Line-Detection-Football/assets/85955796/e8306b56-4c2b-450e-84b9-94482fe08b99)



The ANN model is giving an accuracy of only 50%, which means its guessing the same output for all images.

Even with this dense architecture and huge number of parameters, the ANN fails to perform well since the high dimensionality is preventing it from finding relevant features, or patterns in the image data.
This is why CNNs were invented!

### Convolutional Neural Networks

CNNs have filters to scan small regions of the input data to finding patterns such as edges and shapes. 

Along with this, the same set of parameters/weights for a kernel is applied to all the different parts of the input as the kernel slides along. This enables parameter sharing and reduces total number of parameters without any loss of information.

Pooling layers help to down-sample the feature maps while preserving important features.

All these benefits of CNNs allow them to perform well for image data even when the dataset is small like in this case.

We can visualize what the CNN is seeing by making use of GRAD CAM. 
This is a technique which calculates the gradient of the output with respect to the feature map given by the last convolutional layer of the network. It finds how sensitive the prediction is to different locations on the feature maps.

After finding the gradients, we average them which gives us a weight for different locations on the feature map. We then take the linear combination of these weights with the output. The end product is a heatmap showing the most important features seen by the CNN for our task of goal line prediction.


![Screenshot 2023-10-22 183309](https://github.com/akshayravi13/Goal-Line-Detection-Football/assets/85955796/daada758-71e4-4631-be72-56c8a7012cf9)


This project helps us to understand how different models can be used for binary image classification for predicting goal or not goal. 

We see that LDA does a decent, sub-par job at dealing with this high dimensional image data, while ANN struggles with huge number of parameters and no good feature extraction

CNNs are the best for this task as they have the best output. They can specifically find patterns like edges, shapes in the input image data. 


