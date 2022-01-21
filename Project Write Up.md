## Overview of Project
This assignment was a culmination of everything we've learned in this course. The overall goal was to use a Kaggle dataset and build a classfier in the form of a deep neural network. To accomplish this goal, I used convolution layers, max pooling, batch normalizaiton, Keras' functional API, data augmentation, and transfer learning to construct my model. I then trained it on validation data and evaluated the model on test data. After testing, I observed some of the model's incorrect classifications. My best model achieved a highest result of 96.29%.

## Description of Data
For this assignment, I chose to classify fruit varieties using the 'Fruits 360' dataset on Kaggle. This dataset contains 90,483 images of fruits and vegetables. Of the total, 67,692 images are the training set and 22,688 images are in the test set. The data doesn't come with validation data, so I separated some out using Keras' ImageDataGenerator. These images encompass 131 different variets of fruits and vegetables and are 100 x 100 pixels in size each.

The images were taken by a webcam in front of a white background. The images contain different angles and rotations of each fruit. Files are named according to what variety of fruit or vegetable they are, and at what rotation they were placed for the photo.

## Summary of Methods
I began the assignment by downloading the dataset from Kaggle and then loading it into Google Colab. I used ImageDataGenerator() to create the test, train, and validation set.

Next, I displayed 15 of the test images with labels to confirm that the data loaded correctly as well as to get an idea of what the images of the dataset were like.

Third, I constructed a baseline model. This model used the functional API to create three tiers of a Conv2D layer, a MaxPooling layer, and a BatchNorm layer. These tiers were stacked on top of each other. Then I included a Flatten layer, a Dense layer, and a Dropout layer before the classification layer which had size of 131 for the different classes and used a softmax activation. Next, I trained the model, plotted the accuracy and loss, and evaluated the model on the test data. The model achieved an accuracy of 84.10%.

Next, I performed data augmentation using the ImageDataGenerator(). I made several adjustments including ratations, shifts, zooms, cropping, and flips of the image.

I then trained the baseline model on the augmented data. With more data, the model achieved an accuracy of 90.50%.

Having this baseline, I then turned to Transfer Learning to try and improve my model even more. I decided to use the Xception pretrained model on my dataset. I unfroze the last 6 layers of the model, which represented the last tier of convolution layers. Training this new model on the augmented data produced an accuracy of 89.00%.

Seeing that the model which used transfer learning had a lower accuracy than the base model, I decided to combine the two methods and see if I could achieve a higher accuracy overall. I used some of the base model's structure on top of the Xception model (explained more in depth below) and trained it on the augmented data. This model achieved accuracies between 94.60% and 96.29%.

Finally, I plotted some of the images that the model was predicting incorrectly to see what fruit and vegetable varieties the model was having difficulty identifying.

## Summary of Model
My best model was a mixture of transfer learning using the Xception pre-trained model and my baseline model. I utilized Xception and unfroze the last 15 layers, which represented the last 3 tiers of convolution layers in the network. I then added one tier of the baseline model (Conv2d, MaxPooling, BatchNormaliztion) before adding a flatten layer, a dense layer, and the classification output layer for the 131 different types of fruits and vegetables. This model trained for 28 epochs before stopping due to failing to improve on its maximum for 5 epochs (patience=5). I evaluated the model two times after training, getting accuracies of 94.60% and 96.29%. This model was an improvement over the baseline and over using transfer learning only.

## Analysis of Results
As stated, my best model produced a highest accuracy of 96.29%. I was impressed by this model because at the begining of the assignment when I looked at some of the images, many looked very similar. For example, there are several different varieties of apples in the dataset, many of which I'm not sure I could identify with high accuracy. But the model does.

At the end of the assignment, I display 15 of the incorrect predictions. Some of the mistakes are surprising - classifying corn as white onion - and some are understandable due to lack of scale - classifying cantaloupe as a kiwi. I only chose a random 15 errors, but I was surprised that the vast majority of the errors were ones that I could have classified correctly. I did not see errors of confusing differnt types of apples (one error involved pears) but the model classified ginger as pears two times in the 15. It seemed like the model performed well in some areas I consider nuanced, and poorly in some areas I considered obvious.

However, it is hard to look down on an accuracy of 96% and I'd guess that with some refinement the model could be improved to closer to 99%.

Overall this was a really interesting assignment and dataset to analyze. I was impressed with my model's performance and it was satisfying to apply so many topics here that I have learned throughout the course.
