# KelpNet

## Background
[CoralNet](https://coralnet.ucsd.edu/) is currently being used to assess the percent cover of aggregate taxa [categories](https://www.dropbox.com/scl/fi/7qcjzz3jmnt1oug8k8nrf/CoralNet_Classifications.xlsx?rlkey=wfkhvexu40cqyzs463r8yuxu4&dl=0) documented via the downward facing camera during ROV surveys.

## The Problem
CoralNet is an open-access platform designed to aid in the classification and annotation of underwater images. It leverages machine learning to automate the identification of various species and other substrates. Training a classifier in CoralNet involves feeding the system a large number of labeled images, enabling the machine learning model to learn and distinguish between different categories based on the visual features of 224x224 pixel image patches.

CoralNet utilizes a deep learning architecture to enhance its performance. The system's backbone is based on a [pre-trained convolutional neural network (CNN) model](chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/https://openaccess.thecvf.com/content/ICCV2021W/OceanVision/papers/Chen_A_New_Deep_Learning_Engine_for_CoralNet_ICCVW_2021_paper.pdf), which serves as the foundational structure for extracting image features. The combination of a robust backbone and meticulous fine-tuning allows CoralNet to effectively classify and annotate coral reef images. However, when applied to temperate waters for labeling understory algae and substrate types, the **model's accuracy faces challenges** due to differences in visual features and environmental conditions, necessitating additional adaptation and fine-tuning.

We have a dedicated group of volunteers who have donated hundreds of hours to the painstaking task of labeling over 40,000 points on 1,450 images to train the classifier. An additional issue affecting the accuracy of the classifier is the labeling variation between annotators. Although volunteers underwent a training process, errors still occur. Furthermore, CoralNet does not facilitate easy cleaning of image patches for **quality control**.

We also aim to **share a trained classifier** with other interested parties so they can annotate their own imagery. Currently, CoralNet lacks a pipeline for sharing trained classifiers.


## The Proposed Solution
We think creating an offshoot of CoralNet (called KelpNet) that is fine-tuned to temperate waters to identify algae species of interest would be a great solution. Considering we have thousands of image patches labeled by volunteers, it would be beneficial to leverage this existing dataset.

To support the development of KelpNet, we have found an unofficial codebase called [CoralNet-Toobox](https://github.com/Jordan-Pierce/CoralNet-Toolbox) that allows users to use processes associated with CoralNet. While this toolbox is a valuable resource, it is not very user-friendly.

To address this, we propose the following enhancements:

1. User Interface Improvements: Develop a more intuitive and accessible user interface for the CoralNet-Toolbox to lower the barrier for new users and streamline the workflow for existing users.

2. Automated Quality Assurance: Implement automated quality assurance processes to clean and validate labeled image patches, reducing the impact of labeling variations and errors.

3. Pipeline for Sharing Trained Classifiers: Establish a robust pipeline for sharing trained classifiers with other interested parties. This will enable collaborative efforts and ensure that advancements in KelpNet can be utilized by researchers and conservationists globally.

4. Community Support and Documentation: Create comprehensive documentation and provide community support channels to assist users in adopting and utilizing KelpNet effectively.

By addressing these key areas, KelpNet can become a powerful tool for the scientific community, enhancing the accuracy of algae species identification in temperate waters and contributing to the broader understanding and conservation of these vital ecosystems.

## Next Steps
Dig into [CoralNet](https://coralnet.ucsd.edu/) and [CoralNet-Toobox](https://github.com/Jordan-Pierce/CoralNet-Toolbox). 

## Caveats

## Extra credit 
Utilize the SAM (Segment Anthing Model) tool from the CoralNet-Toolbox to create segmentation masks from a trained classifier. To goal would be for these classified masks to provide more accurate percent coverage statistics.  
