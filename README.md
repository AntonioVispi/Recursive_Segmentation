# Recursive_Segmentation

**This work is the result of participation in the [**KiTS23 Challenge**](https://kits-challenge.org/kits23/#:~:text=The%202023%20Kidney%20and%20Kidney%20Tumor%20Segmentation%20challenge%20(abbreviated%20KiTS23,place%20in%202019%20and%202021.)).**

The following work is an attempt to automate the CT image segmentation process, through a Deep Learning-based approach, with the aim of segmenting the kidney and its possible pathological masses as accurately as possible. It was decided to use a segmentation model of the Encoder-Decoder type, it was decided to use an EfficientNet-B5 as encoder, and an Unet as decoder, suitably set up and modified. It was decided to perform several cascade trainings of the model, which will be called rounds, at the beginning of each of which a refined redefinition of the training and validation images was set up, allowing the model to deal with a large amount of data, increasing its generalisation capacity. Finally, following a careful search for the best training configurations of the models and the various training rounds, good results were obtained on the test set, with a segmentation accuracy of the Kidney + Tumor + Cyst, Tumor + Cyst, Tumor of 97.71 %, 81.39% and 73.81% respectively.
