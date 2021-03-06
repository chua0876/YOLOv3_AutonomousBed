# YOLOv3_AutonomousBed

This file contains my scripts to work with **YOLOv3** (neural network for object detection).

# Setup

## How to install YOLO:
1. Run these in the terminal accordingly:

>git clone https://github.com/pjreddie/darknet

>cd darknet

>make
2. Check whether the system is installed correctly by running these in the **darknet** directory:
>wget https://pjreddie.com/media/files/yolov3.weights

>./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg

Then you will see something like this: 
>layer     filters    size              input                output

> 0 conv     32  3 x 3 / 1   416 x 416 x   3   ->   416 x 416 x  32  0.299 BFLOPs

> 1 conv     64  3 x 3 / 2   416 x 416 x  32   ->   208 x 208 x  64  1.595 BFLOPs

> .......

> 105 conv    255  1 x 1 / 1    52 x  52 x 256   ->    52 x  52 x 255  0.353 BFLOPs

> 106 detection

> truth_thresh: Using default '1.000000'

> Loading weights from yolov3.weights...Done!

> data/dog.jpg: Predicted in 0.029329 seconds.

> dog: 99%

> truck: 93%

> bicycle: 99%

# Autonomous Hospital Bed Path Detection model:

## How to use the custom path detection model?
1. Download and put the required files for the path detection in the **darknet** directory:
> cd darknet

> git clone https://github.com/chua0876/YOLOv3_AutonomousBed.git

2. Download the path detection weights file and put it in the **darknet** directory.
> https://drive.google.com/file/d/1ca-NcQEHWHXCmkGO6kbLxTRF8CNHdpph/view?usp=sharing

### Test on image file:
1. Run this command in the terminal to test the weights file:
> ./darknet detector test YOLOv3_AutonomousBed/obj.data YOLOv3_AutonomousBed/yolov3-tiny-obj.cfg yolov3-tiny-obj_final.weights YOLOv3_AutonomousBed/Sample.jpg

2. Then you will see the result of the detection like **Result.jpg** in the **YOLOv3_AutonomousBed** folder!

### Test on video file: (Require compiling with CUDA and OpenCV - https://pjreddie.com/darknet/install/#cuda)
1. Test the model on a recorded hospital-like corridor video file:
> ./darknet detector demo YOLOv3_AutonomousBed/obj.data YOLOv3_AutonomousBed/yolov3-tiny-obj.cfg yolov3-tiny-obj_final.weights YOLOv3_AutonomousBed/NorthSpine.mp4

2. To use the model in real-time condition:
> ./darknet detector demo YOLOv3_AutonomousBed/obj.data YOLOv3_AutonomousBed/yolov3-tiny-obj.cfg yolov3-tiny-obj_final.weights -c 0

## Training Custom YOLOv3 (New version YOLOv4 is available now)
Highly recommend referring to https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects

1. Marking detection boxes:
- Download the images required to be the training set from Google or wherever source
- On Linux terminal, run these commands:
> git clone https://github.com/AlexeyAB/Yolo_mark.git

> cd Yolo_mark

> cmake .

> make

> ./linux_mark.sh
- After installing Yolo_Mark, follow the steps provided in https://github.com/AlexeyAB/Yolo_mark

2. Prepare config. and other required files by referring to https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects
- Focus on steps 1,2,3 and 6.
- Download pre-trained weights in Step 7

3. Start training by using command
> ./darknet detector train data/obj.data yolo-obj.cfg yolov4.conv.137 (change to corrent path and files)

For more details:
https://pjreddie.com/darknet/yolo/ and https://github.com/AlexeyAB/darknet
