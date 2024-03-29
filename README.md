# Business Understanding

   Neural networks, particularly convolutional neural networks (CNNs), have revolutionized the field of medical image analysis due to their ability to learn complex patterns in data. In the context of diagnosing pneumonia from X-ray scans, CNNs can be trained on large datasets of chest X-rays that have been labeled as showing signs of pneumonia or not. These networks learn to identify the subtle features and patterns that differentiate pneumonia-infected lungs from healthy ones. For instance, they can detect the presence of opacities or consolidation in the lungs, which are signs of pneumonia. This capability is especially valuable because pneumonia can present with a wide variety of ways, making it challenging for even experienced radiologists to diagnose accurately. By providing consistent and quick assessments, neural networks can assist healthcare professionals in making more accurate diagnoses, potentially leading to earlier and more effective treatment for patients.
    
   Additionally, neural networks can help mitigate the shortage of expert radiologists, especially in under-resourced or rural areas. By integrating neural network-based diagnostic systems into the clinical workflow, hospitals can ensure that every X-ray is analyzed with a level of detail and accuracy that matches that of a specialist. This not only helps in preliminary assessment of cases and prioritizing those that require urgent attention but also serves as a second opinion to reduce the likelihood of misdiagnosis. These systems can be continuously improved as they learn from new data, leading to even better performance over time. The use of neural networks for pneumonia diagnosis via X-ray scans is a prime example of how AI can enhance healthcare delivery and patient outcomes. In this project, we will be attempting to create a model that can accurately predict the diagnoses based on the images presented.
   

# Data Understanding

The dataset is organized into 3 folders (train, test, val) and contains subfolders for each image category (Pneumonia/Normal). There are 5,863 X-Ray images (JPEG) and 2 categories (Pneumonia/Normal).

Chest X-ray images (anterior-posterior) were selected from retrospective cohorts of pediatric patients of one to five years old from Guangzhou Women and Children’s Medical Center, Guangzhou. All chest X-ray imaging was performed as part of patients’ routine clinical care.

For the analysis of chest x-ray images, all chest radiographs were initially screened for quality control by removing all low quality or unreadable scans. The diagnoses for the images were then graded by two expert physicians before being cleared for training the AI system. In order to account for any grading errors, the evaluation set was also checked by a third expert.

Data Source: https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia

![doctor](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/doctor.JPG)


## Data Preparation

After defining all of the variable names for each folder and getting the image count in those folders, I'm going to prep the data by first normalizing and resizing the images. The model will only run if the images are the same shape, so once that is done then I will go in to creating my first baseline model.

![xrays](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/xrays.JPG)

# Modeling

Now that the dataset has been prepped, I started the modeling by first running a baseline vanilla neural network. I wanted to see how the data performed before making any significant changes to the images. I then created a baseline CNN to see how I could improve after data augmentation and prepping for the final model. I metric I felt that was import to use in this study was recall because of the fact that a high recall indicates a low false negative rate, meaning the model is good at catching positive cases, also because of the class imbalanced within the dataset. So for the final model, while looking at the accuracy and the loss rate, recall will also help determine how efficiently the model ran.

## Baseline Neural Network

The first model I created was a vanilla neural network that used both relu and sigmoid activation. Due to the randomness of neural networks the results varied each time I ran the model but were typically around 70% accuracy and 60% loss. In this case the accuracy was 73% and the loss rate was 61%.

![model1summary](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/model1summary.JPG)


![model1](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/model1.JPG)



## Baseline CNN

My second model was a baseline CNN to see how I can improve for the final CNN model. I introduced more layers to the model that ultimately improved the accuracy score. The accuracy for the training set increased to 80%, while the loss also decreased to 42%. On the test set, the accuracy increased to 81% and the loss decreased to 37%. Overall, this model performed much better than the original, so I then moved to data augmentation to further improve the model.


![model2summary](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/model2summary.JPG)

![model2](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/model2.JPG)


## Data Augmentation

In order to avoid overfitting the model, we need to artificially expand the dataset. We can make the dataset larger by altering the training data with small transformations to reproduce the variations. The data was adjusted by a rotation range of 40, width shift of 0.2, height shift of 0.2, shear range of 0.3, and a zoom range of 0.1. Once the new data has been created, I ran the new dataset in the finall CNN model.

![dataaug](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/dataaug.JPG)


## Final Model

After artifically expanding the dataset during data augmentation, I fit the dataset to the final model and got the best results so far. Even though the loss rate increase to 39%, the accuracy increased significantly to 88%. The weighted average recall score for this model 89%, which means it detected the postive images very well. In the confusion matrix, it's clear to see where it made the prediction and when it was correct. Recall is not only a good metric to use for identifying positive images but also because of the class imbalance in the dataset.

![modelsummary](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/modelsummary.JPG)


![model3](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/model3.JPG)


![classificationreport](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/classificationreport.JPG)


![confusionmatrix](https://github.com/lpb3393/predicting_pneumonia/blob/main/photos/confusionmatrix.JPG)



# Conclusion

The significant improvement in the CNN accuracy ranged from 83% to 88% after data augmentation indicates a substantial enhancement in the model’s diagnostic capabilities for pneumonia from X-ray images. However, the increase in loss from 37% to 39% suggests that while the model is correctly identifying more cases, it is also making more errors on individual predictions. This could be due to the model becoming more sensitive and thus, more prone to false positives, or it may reflect the increased complexity of the augmented dataset. It’s crucial to analyze the types of errors contributing to the loss to ensure that the model’s improved accuracy translates into reliable and clinically useful predictions. But due to the nature of neural networks, the randomness will cause different results each time the model is run. The range of accuracy for the final model has been between 83-88%, while the loss has been ranging from 35-50%.

 
## Limitations

While convolutional neural networks have shown promise in predicting pneumonia from X-ray images, they do have limitations. One major challenge is the need for large and diverse datasets to train the models effectively; without them, CNNs can suffer from overfitting and may not generalize well to new data. Additionally, CNNs can struggle with subtle features of pneumonia that are not easily distinguishable from other lung conditions, leading to potential misdiagnoses. The interpretation of X-ray images by CNNs also lacks the nuanced understanding that a trained radiologist brings, particularly in complex cases where multiple factors must be considered3. These limitations highlight the importance of using much larger dataset, combining CNNs with expert human analysis and ensuring that the training data is as comprehensive and unbiased as possible.

## Next Staps

While chest X-rays are clearly a great way to predict pneumonia, they are not the only data type that can be used. CNNs can also be trained on a variety of other data types. For instance, computed tomography (CT) scans provide a more detailed view of the lungs and can potentially reveal more subtle features indicative of pneumonia. Patient metadata, such as age, gender, and underlying health conditions, can also be incorporated into the model to improve its predictive power. Furthermore, audio data from a patient’s cough or breathing can be analyzed using a CNN for pneumonia detection. Therefore, while chest X-rays play a crucial role, the application of CNNs in pneumonia prediction can leverage a wide array of data types for more comprehensive and accurate predictions and in the future, it could be beneficial to use all methods.



## For More Information
See the full analysis in the [Jupyter Notebook](https://github.com/lpb3393/predicting_pneumonia/blob/main/predicting_pneumonia.ipynb) or review the [presentation](https://github.com/lpb3393/predicting_pneumonia/blob/main/predicting-pneumonia-presentation.pdf)




```
├── data
├── photos
├── .gitignore
├── README.md
├── predicting-pneumonia-presentation.pdf
└── predicting_pneumonia.ipynb
```
