# Indoor-Scene-Recognition
The dataset has a collection of about 15000+ labeled images belonging to 67 categories. I am selecting only below 10 categories :

airport_inside, auditorium, bakery, bathroom, bookstore, casino, church_inside, grocerystore, operating_room, warehouse  Objective is to create a model that will able to classify images into these 10 categories.

# Approach:
- Created training and validation dataset with required preprocessing and vizualized training dataset.
![download (1)](https://user-images.githubusercontent.com/77941537/150504708-3871e63f-9471-4524-8542-b8c7e84551fe.png)

- Created Data Augmentationlayer using appropiate augmentation techniques and vizualized the augmented data.
![download](https://user-images.githubusercontent.com/77941537/150504696-4805eccf-ab48-42c5-a84f-83369afa7d41.png)


- Loaded data into cache to overcome data bottleneck during training. Also Shuffed data before starting of each epoch.

- First trying transfer learning using InceptionV3 architecture with imagenet pretrained weights. I have removed the default output softmax layer of InceptionV3. I have kept First 249 layers weights as it is. Trained layer 249 to last layer on training dataset. Added a Flatten layer, Dropout layers, 2 hidden dense layers and output dense layer with 10 neurons and softmax as activation.
I will use label encoding instead of one hot encoding to optimize memory utilization. So my loss function will be: sparse_categorical_entropy and my metric will be sparse_categorical_accuracy.
![download (2)](https://user-images.githubusercontent.com/77941537/150504661-7782fea2-85a6-45af-b749-7df6fbf98ecf.png)

  -Best Epoch: 109 (model-00109-0.08159-0.99170-0.67942-0.85068.h5)
  -**Training: loss: .08 - categorical_accuracy: 0.99**
  -**Validation: val_loss: .68 - val_sparse_categorical_accuracy: 0.85**


- Used almost same architecture as previous one, only used Xception as our cnn architecture instead of InceptionV3. Removed output softmax layer of Xception architecture and finetunned Xception from layer 114 to end layer. Then I have added custom layers as previous.
![download3](https://user-images.githubusercontent.com/77941537/150505012-13c48a5f-2e79-4914-b623-84a7976f7606.png)


  - Best Epoch: 88 (model-00088-0.07750-0.99321-0.49403-0.89140.h5)
  - **Training: loss: .775 - categorical_accuracy: 0.993**
  - **Validation: val_loss: .494 - val_sparse_categorical_accuracy: 0.891**


# Inference
Created inference function and used both the models wioth best weights and calculated average probability value for all 10 classes from these 2 models and that average probability is used for final classification.
![image](https://user-images.githubusercontent.com/77941537/150505450-9fd7fa38-345b-4b8f-872c-3c88f920c9e5.png)


![image](https://user-images.githubusercontent.com/77941537/150505484-fc3f1e49-4808-4605-bfdb-2d489ca30306.png)


![image](https://user-images.githubusercontent.com/77941537/150505530-853cbc41-c91e-48cd-a2c3-f38da37fd892.png)

![image](https://user-images.githubusercontent.com/77941537/150505558-16c21d13-721f-40fd-93d5-2dd426a3b9bf.png)

# Final Model files:

Model1: https://drive.google.com/file/d/18KDv8_qoJDI0osEiuqaOlYZbQe1oKptn/view?usp=sharing   (390 MB)

Model2: https://drive.google.com/file/d/18mtLaKrAA2Dthas2k6hnkjjJXYPPbRMV/view?usp=sharing  (737 MB)


