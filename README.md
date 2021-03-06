# IW276SS20P1: Activity Recognition in Real-Time (Jetson Nano)


In diesem Projekt werden zwei verschiedenen Möglichkeiten zur Darstellung von Skeletten/Posen auf einem Video verglichen. Die erste Variante beinhaltet mithilfe von Openpose Skeleton Keypoints eines Videos in Form von Json-Dateien zu extrahieren und dann zur Laufzeit über das entsprechend Video zu legen. In der zweiten Variante wird trt_pose verwendet. Zunächst wir von trt_pose eine JSON-Datei geladen, die die Human Pose beschreibt und anschlißend werden trt_pose Model und Modelgewicht geladen. Um das Model zu optimiren wird torch2trt verwendet. Nach dem Benchmarking des Models in FPS wurden zwei Klassen definiert, die zum Parsen der Objekte dem neuronalen Netzwer sowie zum Zeichnen der analysierten Objekte auf einem Bild verwendet werden. Bei der Definition der Hauptausführungsschleife wurden folgende Schrittte durchgeführt.



English description: <br />
In this project we were tasked with comparing the performance of two different ways of overlaying/recognizing skeletons in a video.
One way was to extract the skeleton keypoints to a json file via OpenPose which were then overlayed on the video at runtime.
The other way was to use trt_pose ...
Below you'll find a video demonstrating the two ways. <br />
<br />

**Result image from openpose** <br />
![result from trt_pose](/images/1.PNG)<br />
<br />
**Result image from trt_pose** <br />
![result from openpose](/images/trt_image.jpeg)



  [Link to Demo Video](https://youtu.be/xZj7YrHmFSA)


> This work was done by Jingye Zhang, Janika Finken, Ga Young Volk and M. Bielawski during the IW276 Autonome Systeme Labor at the Karlsruhe University of Applied Sciences (Hochschule Karlruhe - Technik und Wirtschaft) in SS 2020.

## Table of Contents

* [Requirements](#requirements)
* [Prerequisites](#prerequisites)
* [Running](#running)
* [Acknowledgments](#acknowledgments)

## Requirements
* Python 3.7 (or above)
* OpenCV 4.0 (or above)
* Jetson Nano
* [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)
* [trt_pose](https://github.com/NVIDIA-AI-IOT/trt_pose)
* [PyTorch](https://pytorch.org)
* [torchvision](https://pypi.org/project/torchvision/0.1.8)

## Prerequisites
1. Install requirements:
```
pip install -r requirements.txt
```

## Running

To run the demo,<br />
**openpose**<br />
convert the MPII Dataset to csv via MATConverter.py,
```
python MATConverter.py
```
<br />download the Youtube videos via YoutubeDownloader.py
```
python YoutubeDownloader.py
```
<br />and then extract skeleton keypoints via OpenPose and getJson.py.
```
python getJson.py
```

<br />Afterwards, you can run json_to_video.py to paint scelettons on video.
```
python json_to_video.py
```

**trt-pose**

With detect_image.py show pose on images and with detect_video.py show pose on video.<br />

Argumente:<br />
--video Videoname (default=video.avi)<br />
--model Modeltyp (resnet oder densenet. default=resnet)<br />
--path Pfad (default=/home/p1/Downloads/)<br />

Usage Bsp: <br />
For Resnet <br />
```
pip3 detect_video --path /your/path/ --video video.mp4
```
For densenet <br />
```
pip3 detect_video --path /your/path/ --video video.mp4 --model densenet
```
Default: Output Video with skeleton<br />
If you want to get output with keypoints, then should enable the line 120-128 and disable the line 130.

> Make sure the .py files are using correct paths.

## Acknowledgments

This repo is based on
  - [MPII Dataset](http://human-pose.mpi-inf.mpg.de/)
  - [OpenCV](https://github.com/opencv/opencv/)  
  - [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)

Thanks to the original authors for their work!

## Contact
Please email `mickael.cormier AT iosb.fraunhofer.de` for further questions.
