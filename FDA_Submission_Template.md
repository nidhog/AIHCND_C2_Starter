# FDA  Submission

**Your Name:** Ismail Elouafiq

**Name of your Device:** Xhale-001

## Algorithm Description 

### 1. General Information

**Intended Use Statement:** 
The Xhale-001 system is intended to be used in a clinical setting to prioritize the workflow of chest X-rays to be reviewd by the hospital's radiologists. The Xhale-001 uses a machine learning algorithm to analyze chest X-ray images for features suggestive of Pneumonia. 

The Xhale-001 is intended to be used on digital X-ray chest images. The result of the Xhale-001 is not conclusive, the identification of cases of Pneumonia is not intended for diagnostic use, the result is intended to be used to notify. Thus Xhale-001 should not be used to replace a patient's evaluation, nor to make, confirm or reject diagnoses.

**Indications for Use:**
Xhale-001 is indicated for detecting pneumonia in chest X-ray images for males and females between the ages of and .
**Device Limitations:**
* This algorithm must be run with a computer that meet minimum GPU and RAM requirements.
* Chest X-ray data.
* Can be highly confused with Infiltration. Can be slightly confused with Edema, Effusion and Atelectasis.
* Unknowns such as persons in pregnancy or with conditions that may impact the X-ray chest image reading
**Clinical Impact of Performance:**


### 2. Algorithm Design and Function


![Algorithm](img/flowchart.jpg "Algorithm Flow Chart")
*Figure 1 - Xhale-001 Algorithm Flow Chart.*

**DICOM Checking Steps:**

Check DICOM Headers for:
Modality == 'DX'
BodyPartExamined=='CHEST'
PatientPosition in 'PA' or'AP' Position

**Preprocessing Steps:**
* The pixel array in the DICOM file is used.
* The pixel array is rescaled by a factor of 1/255
* The pixel array is normalized
* The pixel array is resized to a width of 224 and a height of 224.

**CNN Architecture:**
We use a pretrained VGG16 model and we fine-tune it for our use case. 
* We used a pretrained VGG16 model where freeze the first 17 layers.
* We add a BatchNormalizer
* We add a convolution
* We add a 


### 3. Algorithm Training

**Parameters:**
* Types of augmentation used during training
* Batch size
* Optimizer learning rate
* Layers of pre-existing architecture that were frozen
* Layers of pre-existing architecture that were fine-tuned
* Layers added to pre-existing architecture

<< Insert algorithm training performance visualization >> 

<< Insert P-R curve >>

**Final Threshold and Explanation:**

### 4. Databases
 (For the below, include visualizations as they are useful and relevant)

**Description of Training Dataset:** 
* The prevalence of Pneumonia is very low in the dataset. Only <TODO> of the images are positive cases of pneumonia. For this reason, we select all positive pneumonia cases and we randomly select an equal number of negative pneumonia cases. This means we are excluding <TODO>. The reason for this is to make sure there is an equal amount of positive and negative pneumonia cases.

**Description of Validation Dataset:** 
The prevalence of positive cases of pneumonia in the validation set must be representative of the real world. We verify that the amount of postivie cases in the validation set is: <TODO>

### 5. Ground Truth
The ground truth for the existence of pneumonia was obtained from a labeled dataset of X-Ray images provided by the NIH that can be found here: https://www.kaggle.com/nih-chest-xrays/data . 

* The dataset contains in total 112120 images.
* There are 30805 unique patient IDs in the dataset.
* The disease labels were obtained through the use of Natural Language Processing to text-mine disease classifications from the radiologist reports of the X-ray images.
* This implies that it's possible not all disease labels are correct and thus pneumonia labels may not be correct. However, the labels are expected to be >90% accurate and suitable for weakly-supervised learning. 
* Even with the last constraint this dataset contains more than previous initiatives such as https://openi.nlm.nih.gov/
* The original reports from which the labels were created are however not available and thus cannot be verified.


### 6. FDA Validation Plan

**Patient Population Description for FDA Validation Dataset:**

**Ground Truth Acquisition Methodology:**

**Algorithm Performance Standard:**
