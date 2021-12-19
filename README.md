# Talking-Face-Generation-Using-Deformable-Models
This project was done as part of course CS269 at UCLA
Team Members:
1) Parth Shettiwar
2) Satvik Mashkaria
3) Lalit Bhagat
4) Pranjal Jain
5) Sahil Bansal

## Abstract
Talking face generation is the process of generatinga video of a person saying the input audio with appropriate lip and 
facial features synced at each time step. In audiovisual speechcommunication, visual emotion expression is crucial. 
Using deeplearning, researchers have been able to make considerableprogress in tackling this computer vision task. 
CNNs are designed to model big, unknown transformations, however they have limitations. In this work, we propose a hybrid approach by 
adding deformable layers and attention modules. We further compare our approach to purely deep learning based approaches and contrast them 
using the structural similarity (SSIM) andpeak signal-to-noise ratio (PSNR) metrics. 

## Architecture
![.](https://github.com/parth-shettiwar/Talking-Face-Generation-Using-Deformable-Models/blob/main/Diagram/diagram.png)

## Results
Given input image, speech sample, and emotion, we generate the video of the person with lip and facial features synced with the video
Following is the sample video we generated on our team members  
![.](https://github.com/parth-shettiwar/Talking-Face-Generation-Using-Deformable-Models/blob/main/Diagram/1HAP_generated.mp4_.gif)
![.](https://github.com/parth-shettiwar/Talking-Face-Generation-Using-Deformable-Models/blob/main/Diagram/2HAP_generated.mp4_.gif)
![.](https://github.com/parth-shettiwar/Talking-Face-Generation-Using-Deformable-Models/blob/main/Diagram/HAP_generated.mp4_.gif)
![.](https://github.com/parth-shettiwar/Talking-Face-Generation-Using-Deformable-Models/blob/main/Diagram/3HAP_generated.mp4_.gif)

## How to Run
Find the pretrained models [here](https://drive.google.com/drive/folders/1wjqLrdf82E-qv6CXcwk9fC_dVnEP6PLN?usp=sharing)
Also download the preprocessed dataset from here. We have considered 2 emotions : Happy and Sad subsampled from [CREM-D Dataset](https://github.com/CheyneyComputerScience/CREMA-D). 
Now download all libraires given in requirements.txt as 
```
pip install -r requirements.txt

```
#### For Training
First pretrain the discriminitor

```
!python train.py -i ./Final_Dataset/ -v ./Eval_set/ -o ./Final_Models/Disc_pre/mde --pre_train 1 --disc_emo 1 --lr_emo 1e-4
```
Then pretrain the generator 
```
python train.py -i /Final_Dataset/ -v /Eval_set/ -o ./model --lr_g 1e-4
```
Then do the joint training
```
!python train.py -i ./Final_Dataset/ -v ./Eval_set/ -o ./Final_Models/Orig -m ./model -mde ./Final_Models/Disc_pre/mde --disc_frame 0.01 --disc_emo 0.001 --deform 1

```

#### For Inference
To generate happy and sad videos for all images in eval dataset:
```
!python generate_all_emotions.py -ih ./Eval_set -m ./Final_Models/Ours -o ./results/Ours --deform 1
```
To generate happy and sad video for any random given image and speech sample
```
!python generate.py -im ./data/image_samples/img09.png -is ./data/speech_samples/speech01.wav -m ./Final_Models/Orig -o ./custom_results/
```




