## Project Background
Vehicle body type classification is an important task in automotive analytics, intelligent transportation systems, fleet management, insurance automation, and car marketplace indexing.
This project develops a machine learning model capable of identifying seven vehicle body types from images:
- Convertible
- Coupe
- Hatchback
- Pick-Up
- SUV
- Sedan
- Van

## Data Sources
Primary Dataset  
Cars Body Type Dataset (Cropped)  
Source: Kaggle  
Direct link: [https://www.kaggle.com/datasets/ademboukhris/cars-body-type-cropped/data](https://www.kaggle.com/datasets/ademboukhris/cars-body-type-cropped/data)

## Methodology
The methodology follows a structured machine-learning workflow:

### 1. Data Acquisition  
The project retrieves the dataset via the Kaggle API:  
```

kaggle datasets download -d ademboukhris/cars-body-type-cropped

```  
Unzipping and restructuring ensure correct directory placement.

### 2. Data Preprocessing  
- Images resized to a standard input size.

- Pixel normalization applied using Keras preprocessing utilities.

- Augmentation applied to training images:
    - Rotation
    - Zoom
    - Horizontal flip
    - Brightness adjustments
    - Rescaling

This increases generalization and robustness.

### 3. Model Design
The classifier is built using a transfer learning approach:

✔ Backbone Model  
A modern CNN architecture pretrained on ImageNet  

✔ Custom Classification Head  
Includes:
- Global Average Pooling
- Dropout for regularization
- Final softmax layer with 7 output classes

✔ Loss Function  
categorical_crossentropy

✔ Optimizer  
Adam (adaptive learning rate)

✔ Callbacks
- EarlyStopping
- ModelCheckpoint

### 4. Training
The model is trained using:
- Training dataset
- Validation dataset to monitor overfitting
- Optional class weights (if class imbalance exists)

### 5. Evaluation & Inference
After training, the model is tested using sample images such as:
```

predict_vehicle_detailed("/content/images/lexus.jpg")
predict_vehicle_detailed("/content/images/mercedes.jpg")
predict_vehicle_detailed("/content/images/pickup.jpeg")

```

The prediction function:
- Preprocesses the image
- Runs inference
- Displays: top prediction, confidence score, probability distribution across all 7 classes

## Results & Conclusion
The model’s performance during evaluation showed low accuracy, and its predictions on test images were frequently incorrect. Despite applying transfer learning and data augmentation, the classifier struggled to distinguish between the seven vehicle body types. This outcome suggests several underlying issues:

- Dataset imbalance may have caused the model to favor certain classes.
- Insufficient visual variance or low-quality images in some categories may have limited generalization.
- Model architecture or hyperparameters may not have been optimal for this task.
- Possible misalignment between dataset content and real-world images used during testing.

These results indicate that the current model is not yet suitable for reliable vehicle body type classification. Further improvements are required, such as exploring stronger architectures, conducting deeper hyperparameter tuning, expanding or re-curating the dataset, and performing more advanced augmentation strategies.
