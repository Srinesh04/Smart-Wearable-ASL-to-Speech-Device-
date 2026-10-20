# LEXORA — Wearable Sign Language Recognition Device

## Overview

LEXORA is a wearable assistive device designed to make communication easier for people with speech disabilities. The system uses an ESP32-CAM with an OV2640 camera to capture hand signs and an on-device machine learning model to recognize them in real time. The recognized sign is then converted into text and displayed on an LCD.

## Problem Statement

People with speech disabilities can face difficulties communicating with people who do not understand sign language. Although assistive communication devices are available, many existing solutions can be expensive, bulky, or dependent on glove-based systems, which may not be practical for everyday use.

LEXORA was developed to address this gap by exploring a low-cost, wearable, and natural way of recognizing hand signs. Instead of requiring the user to wear a sensor-filled glove, the system uses a camera attached to a harness with the clothing to observe hand gestures and performs the recognition directly on the ESP32-CAM.

This approach aims to make the device more portable and allow users to communicate using their normal hand movements.

## Key Features

- Wearable & Compact Design
- Real-Time Sign Recognition
- On-Device Machine Learning (not dependent on PC or cloud)
- Camera-Based Gesture Detection
- Offline Functionality
- Low-Cost Hardware
- Edge AI Processing
- Expandable Sign Vocabulary

## System Architecture

![LEXORA system architecture](images/system-architecture.png)

*Figure: Overview of the LEXORA system, from camera input and on-device gesture recognition to text output on the LCD.*

## Hardware Components

| Component | Usage in LEXORA |
|---|---|
| ESP32-CAM | Main controller that processes camera frames and runs the deployed ML model. |
| OV2640 Camera | Captures live images of the user's hand gestures. |
| LCD Display | Displays the recognized hand sign as text. |
| LiPo Battery | Provides portable power for the wearable device. |
| BMS Module | Manages and protects the LiPo battery during operation. |
| LM2596 Buck Converter | Steps down the battery voltage to a suitable level for the ESP32-CAM. |

## Software Components

| Software / Technology | Usage in LEXORA |
|---|---|
| Arduino IDE | Used for programming and deploying firmware to the ESP32-CAM. |
| Edge Impulse | Used for preparing the dataset, training, evaluating, and deploying the gesture recognition model. |
| TensorFlow | Used for training the CNN-based hand sign recognition model. |
| TensorFlow Lite Micro | Used to deploy the optimized ML model for inference on the ESP32-CAM. |
| Embedded C/C++ | Used to implement the embedded system logic and hardware control. |

## Dataset

The dataset was prepared to train the model to recognize a set of predefined hand signs. The images were collected and organized into separate classes based on the gesture being performed.

### Gesture Classes

The current dataset contains 6 hand-sign classes:

- `AGAIN`
- `FINE`
- `HELP`
- `LIKE`
- `MORE`
- `WASHROOM`

Each image is labelled according to its corresponding gesture, allowing the model to learn the visual differences between the signs.

### Dataset Preparation

- Hand gesture images were collected for each class using the OV2640 camera instead of an online dataset.
- Images were organized and labelled according to the corresponding sign.
- The dataset was uploaded to Edge Impulse for further processing and model development.
- The images were prepared for the selected image-processing pipeline before training.

## Edge Impulse Workflow

### 1. Data Collection & Upload

- Collected hand-sign images for the six target gesture classes.
- Uploaded and organized the images in Edge Impulse.

### 2. Create Impulse

- Defined the image input and processing pipeline for the gesture recognition model.
- Used a `96 × 96` pixel image input for the model.

### 3. Image Preprocessing

- Converted the input images to grayscale to simplify the image data.
- Prepared the images for feature extraction and model training.

### 4. Feature Extraction

- Extracted useful visual features from the processed hand-sign images.
- Generated feature representations that could be used by the learning model.

### 5. Model Training

- Trained the model using the prepared gesture dataset.
- The model learned to distinguish between the six different hand-sign classes.

### 6. Model Evaluation

- Evaluated the trained model using validation data.
- Checked how well the model classified the different gesture classes.

### 7. Model Testing

- Tested the trained model on previously unseen gesture samples.
- Verified whether the predicted class matched the actual gesture.

### 8. Model Deployment

- Prepared the trained model for deployment on the ESP32-CAM.
- Optimized the model for embedded inference with limited memory and processing resources.
- The final model can perform inference directly on the device without relying on a PC or cloud.
