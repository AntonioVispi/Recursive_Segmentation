https://github.com/MuhammadMoinFaisal/YOLOv8-DeepSORT-Object-Tracking/assets/102518682/dc7da9fc-7316-4e21-a462-ce36a6d1f990
# Recursive Segmentation (Work in progress...)

**This work is the result of my participation in the [**KiTS23 Challenge**](https://kits-challenge.org/kits23/#:~:text=The%202023%20Kidney%20and%20Kidney%20Tumor%20Segmentation%20challenge%20(abbreviated%20KiTS23,place%20in%202019%20and%202021.)).**

The following work is an attempt to automate the CT image segmentation process, through a Deep Learning-based approach, with the aim of segmenting the kidney and its possible pathological masses as accurately as possible. It was decided to use a segmentation model of the Encoder-Decoder type, it was decided to use an EfficientNet-B5 as encoder, and an Unet as decoder, suitably set up and modified. It was decided to perform several cascade trainings of the model, which will be called rounds, at the beginning of each of which a refined redefinition of the training and validation images was set up, allowing the model to deal with a large amount of data, increasing its generalisation capacity. Finally, following a careful search for the best training configurations of the models and the various training rounds, good results were obtained on the test set, with a segmentation accuracy of the Kidney + Tumor + Cyst, Tumor + Cyst, Tumor of 97.71 %, 81.39% and 73.81% respectively.


## Working Environment

This repository uses the following environment to run the code:

```bash
!pip install -U -q segmentation-models
!pip install tensorflow==2.9.3
!pip install h5py==2.10.0
!pip install plotly==5.3.1
```


## Getting Started

To set up the entire pipeline, the first step is to download the dataset from the [**creators repository**](https://github.com/neheller/kits23.git) in the format suitable for this project. The code responsible for this task is in the Jupyter notebook named 'Get_Dataset_KiTS23.ipynb'.

**Open and run the ```Get_Dataset_KiTS23.ipynb``` notebook using Jupyter or directly Colab so follow the simple instructions within the notebook to download and prepare the dataset.**


## Train Script Introduction

**This Jupyter notebook, named ```Train_Script.ipynb```, is a crucial component of the project's pipeline. Its primary purpose is to facilitate the training of the model on the prepared dataset, ensuring that it learns and generalizes well to perform the segmentation task.**

The notebook begins by loading and preprocessing the dataset, preparing it for the training process. It includes configurations for the model architecture, hyperparameters, and data augmentation. During the training, the notebook evaluates the model's performance, providing insights into its effectiveness.

The training process consists of several successive rounds, each defining new training and validation volumes. At each round, the script will output the model that leads to the best results of that round. At this point, the user should use this model as an initialization for subsequent rounds (by simply entering its model path as written in the train script). In turn, at the end of this second training, a third training can be initialized and so on. This process can be repeated as much as you want; recommend no more than 10 iterations. The process of redefining training data occurs automatically at the beginning of each round.

The best model, because of the way the algorithm was developed, will be the one with the lowest validation loss, shown in the log title, in the folder where model checkpoints are saved during training. This iterative approach ensures continuous improvement, with the final model selected based on the lowest validation loss across all rounds.


