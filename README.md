# Stereo Object Detection with Disparity Depth Estimation

<img alt="license" src="https://img.shields.io/github/license/mashape/apistatus.svg"/>

<!-- 
This project processes stereo video captured from a ZED camera to perform real-time object detection using a YOLO model, combined with depth estimation using stereo disparity maps. The output includes bounding boxes with estimated distances and an optional video output.
-->

This project focuses on creating object detection models for an aquatic environment. In addition, stereo video is captured and processed with a ZED camera to detect these objects in real time using YOLO models, combined with depth estimation using stereo disparity maps. The output includes bounding boxes with estimated distances and an optional video output.

To validate the proposed neural network models by making inference with the video captured with the ZED camera, the following steps were followed:

## 1. Requirements
To run the code, you will need to install the following dependencies beforehand:

* Ultralytics >=8.3.20
* Python
* Pytorch 
* Clearml 1.18.0 

### 2. Python dependencies
The best way to install python dependencies is by using a virtual environment, to do so:

```bash
$ sudo apt install virtualenv
$ virtualenv -p python3 venv
$ source venv/bin/activate
$ pip install numpy
```
To deactivate virtualenv, do by:

```bash
$ deactivate
```
## 3. Structure and format of the dataset
```
Datasense@CRAS/ │
              ├── train/ │
              │   ├── images/ 
              │   └── labels/ 
              ├── valid/ │
              │   ├── images/ 
              │   └── labels/ 
              ├── test/ │
              │   ├── images/ 
              │   └── labels/ 
              └── data.yaml 
```
### 3.1 Dataset used in this research
* Original dataset: [Datasense@CRAS](https://rdm.inesctec.pt/lv/dataset/nis-2022-001).
* Original dataset: [SeaDroneSee v2](https://cloud.cs.uni-tuebingen.de/index.php/s/ZZxX65FGnQ8zjBP?path=/Compressed%20Version).
* Our dataset as a contribution: [USVDDModel](https://universe.roboflow.com/modelboat/boat-detection-oelpk).

## 4. Train Yolov8 object detection on a custom dataset
To run or launch the training you will need:

```bash
$ yolo detect train data=/path/data.yaml model=yolov8n.pt epochs=150 imgsz=640 batch=16 lr0=0.001 momentum=0.9 weight_decay=0.0005 plots=True save=True amp=True
```

## 5. Neural network models
* Datasense@CRAS  
   [nano model](https://gitlab.com/Ljmn30/tfm/-/raw/main/Datasense@CRAS/Train2/weights/best.pt?ref_type=heads).    
   [small model](https://gitlab.com/Ljmn30/tfm/-/raw/main/Datasense@CRAS/Train3/weights/best.pt?ref_type=heads).   
   [medium model](https://gitlab.com/Ljmn30/tfm/-/raw/main/Datasense@CRAS/Train/weights/best.pt?ref_type=heads).    
   
* SeaDroneSee v2  
   [nano model](https://gitlab.com/Ljmn30/tfm/-/raw/main/SeaDronesSee/Train/weights/best.pt?ref_type=heads).    
   [small model](https://gitlab.com/Ljmn30/tfm/-/raw/main/SeaDronesSee/Train2/weights/best.pt?ref_type=heads).   
   [medium model](https://gitlab.com/Ljmn30/tfm/-/raw/main/SeaDronesSee/Train3/weights/best.pt?ref_type=heads).   
   
* USVDDModel  
   [nano model](https://gitlab.com/Ljmn30/tfm/-/raw/main/USVDDMODEL/Train/weights/best.pt?ref_type=heads).    
   [small model](https://gitlab.com/Ljmn30/tfm/-/raw/main/USVDDMODEL/Train2/weights/best.pt?ref_type=heads).   
   [medium model](https://gitlab.com/Ljmn30/tfm/-/raw/main/USVDDMODEL/Train3/weights/best.pt?ref_type=heads). 
   
## 6. Running inference on Jetson Orin + ZED 2 camera

### 6.1 Intall dependencies
* JetPack SDK
* ZED SDK
* Ultralytics
* CUDA

### 6.2 Run inference
To run inferences with our model and video captured with the ZED camera, we used the example available in the Stereolabs repository: https://github.com/stereolabs/zed-sdk/blob/master/object%20detection/custom%20detector/python/pytorch_yolov8/detector.py

In addition, the inference video is available in the `Postprocessing-CameraStereo/` folder, in which we have used the [medium model](https://gitlab.com/Ljmn30/tfm/-/raw/main/Datasense@CRAS/Train/weights/best.pt?ref_type=heads) of the Datasense@CRAS dataset for object detection.

## 7. Publications

Title: YOLO-Based Power-Efficient Object Detection on Edge Devices for USVs  
Journal: Journal of Real-Time Image Processing  
Submitted

## 8. Acknowledgements
This paper has been partially funded by the EU (FEDER), the Spanish MINECO under grants PID2021-126576NB-I00 and TED2021-130123B-I00 funded by MCIN/AEI/10.13039/501100011033 and by European Union "ERDF A way of making Europe" and the NextGenerationEU/PRT. J.L.M. thanks the National Secretariat of Science, Technology and Innovation (SENACYT) of Panama for financial support during the completion of his PhD.
