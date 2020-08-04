# Benign v Malignant Melanoma and Lesion Classification

## Introduction: 

Melanoma is the deadliest form of skin cancer in the world. Even with an ~91% survival rate, dermalogists maintain a relatively low rate of proper identification of cancerous lessions with a relatively high chance of false-negative diagnosis. The goal of this project is to build and train a Convolutional Neural Network (CNN) which can classify different forms of melanoma, and other lesions, as benign or malignant as well, if not better, than current visual exams.

## Data:

The data was sourced directly from the <a href='https://www.isic-archive.com/'>International Skin Imaging Collaboration (ISIC)</a> as well as the <a href='https://www.kaggle.com/c/siim-isic-melanoma-classification'>2020 Kaggle Melanoma Classification Challenge</a>. Kaggle sources their data from ISIC though their dataset does differ in size than what is available via the ISIC Archive, likely including images not yet submitted to the archive's gallery.


![Dataset Breakdown](https://github.com/nlnlvlc/melanoma_classification/blob/master/Screen%20Shot%202020-08-04%20at%201.37.03%20PM.png)

## Method:

Images were resized to 224 x 224 pixels for Keras models and 256 x 256 pixels for PyTorch models. Images were augmented to further diversify the images as they passed through the models. Models using ResNet34 were tuned and tested in two variations: with manipulation to the Fully Connected Layer, only; unfreezing and optimizer interal ResNet34 layers.

A basic CNN was used as the baseline model for Keras and Pytorch. In order to further improve the PyTorch model, two models using the pretrained Resnet34 network were used in. Due to complexities with PyTorch Binary and Multicategorical functions, the PyTorch ResNet Model will be used for analysis.

**Update Aug 4, 20202** Alternative models were ran got each base model adjusting the size and color (grayscale) to check impact of parameters, viewable under the ***Additional Models*** directory of this repository. For the person of this ReadMe, the results will focus solely on the original models.


## Results:

The second Keras model performed that best with a 76% accuracy and ~.59 Loss. The model showed some improvement from 73% and an ~.65 Loss from the first model. Both models with a batch size of 32. The first model ran through 10 epochs and the second through 40 epochs, suggesting this model can perform well with significantly more epochs with the same datasets. A pretrained ResNet50 model was attempted though the memory necessary for the model to run was not available.

The ResNet34 PyTorch Models performed similarly to the first Keras model though only on 6 epochs and smaller batch size. The base PyTorch method varied greatly, with the most recent model producing inconsistent accuracies of 50% or 100%. The base PyTorch did not produce adequate results do to the limitations in batch size and GPU usage, so training was only able to happen on a small number of batches at a time, limiting how much the model could learn.

## Conclusion & Future Work:

<a href='https://www.sciencedaily.com/releases/2018/05/180528190839.htm#:~:text=In%20level%20I%2C%20the%20dermatologists,CNN%20detected%2095%25%20of%20melanomas'>Per a study published in the European Society for Medical Oncology</a> "In level I, the dermatologists accurately detected an average of 86.6% of melanomas, and correctly identified an average of 71.3% of lesions that were not malignant." This suggests that both pretrained and new CNNs can performed on the same level, if not slightly better than, dermatologist and oncologists currently do with visual exams, only. Given the spead and accuracy, further classification with ResNet34, or other versions of ResNet, with higher epochs might produce even better results without the heavy memory load that comes with Keras.

As seen in this <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6936633/">study</a>, rates of indentification by medical professionals can differ as much as 10%. These models could be used for supplementary purposes in aiding medical professionals to make more educated decisions in diagnosing benign and malignant lesions.

Though these models might be effective in identifying benign and malignant lesions based off of our training data, it is important to note that the dataset did not include any non-White patients, meaning this model is likely to be ineffective in classifying lesions on darker skin tones. That presents a huge problem, considering that most people in the world are darker than patients in datasets and also suffer from a significantly lower survival rate, as evidences by the CDC's Cancer and Lesion Database. A more consistent dataset might also play a part in improving these models. The ISIC has conflicting datasets in their archive as well as publically available data such as the Kaggle dataset. It <m>is</m> possible that our malignant datasets were containmenated by benign images, skewing the results, due to the archive including additional images not including in the parameters set.
