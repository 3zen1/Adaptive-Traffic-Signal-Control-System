# Adaptive Traffic Signal Control System


## 1. Abstract :

Traffic congestion has become an increasingly challenging problem with the growing number of vehicles on our roads. As traffic flow surges, the length of vehicle queues at intersections rises dramatically. Traditional traffic signal systems, which rely on fixed timings, struggle to efficiently manage this escalating demand.

To address this issue, we have developed an innovative solution that combines computer vision and machine learning to analyze traffic patterns at signalized road intersections. This analysis is facilitated by a cutting-edge real-time object detection technique utilizing a deep Convolutional Neural Network known as "You Only Look Once" (YOLO). We then optimize traffic signal phases based on real-time data, focusing on queue density and waiting times for individual vehicles, enabling the safe passage of more vehicles with minimal delays. This YOLO-based system can be seamlessly integrated into embedded controllers through transfer learning techniques.

## 2. Problem Statement :

The primary problem we aim to solve is the inefficient management of traffic signals. Different lanes experience varying traffic densities, resulting in underutilized time slots for some lanes, causing slower speeds, longer trip times, and increased vehicle queues. Our objective is to create a system that allows traffic signal management to dynamically allocate time slots to specific lanes based on real-time traffic conditions, as observed through cameras and image processing modules.

## 3. Introduction :

Traffic congestion is a major problem in many cities, and the fixed-cycle light signal controllers are not resolving the high waiting time in the intersection. We see often a policeman managing the movements instead of the traffic light. He sees road status and decides the allowed duration of each direction. This human achievement encourages us to create a smart Traffic light control taking into account the real time traffic condition and smartly manage the intersection. To implement such a system, we need two main parts: eyes to watch the real-time road condition and a brain to process it. A traffic signal system at its core has two major tasks: move as many users through the intersection as possible doing this with as little conflict between these users as possible.

### Literature
The projects is based on [Tensor nets](https://github.com/taehoonlee/tensornets), [keras-yolov3 repository](https://github.com/experiencor/keras-yolo3) - find more detailed read on the [blog](https://towardsdatascience.com/object-detection-using-yolov3-using-keras-80bf35e61ce1).
### Dependencies
Install dependencies via pip specified by requirements.txt file.
The code is tested and run with Python 3.7.4 and Python 3.5.6 on Ubuntu 18.04.3 LTS.
(Windows 10 platforms should also be able to run the project).


## 4. Technology :

### YOLO

You only look once (YOLO) is a state-of-the-art, real-time object detection
systemYOLO, a new approach to object detection. Prior work on object detection
repurposes classifiers to perform detection. Instead, we frame object detection as a
regression problem to spatially separated bounding boxes and associated class
probabilities. A single neural network predicts bounding boxes and class probabilities
directly from full images in one evaluation. Since the whole detection pipeline is a
single network, it can be optimized end-to-end directly on detection performance.


The object detection task consists in determining the location on the image where
certain objects are present, as well as classifying those objects. Previous methods for
this, like R-CNN and its variations, used a pipeline to perform this task in multiple
steps. This can be slow to run and also hard to optimize, because each individual
component must be trained separately. YOLO, does it all with a single neural network.


### YoloV3 Car Counter

This is a demo project that uses YoloV3 neural network to count vehicles on a given video. The detection happens every x frames where x can be specified. Other times the dlib library is used for tracking previously detected vehicles. Furthermore, you can edit confidence detection level, number of frames to count vehicle as detected before removing it from trackable list and the maximum distance from centroid (see CentroidTracker class), number of frames to skip detection (and only use tracking) and the whether to use the original video size as annotations output or the YoloV3 416x416 size.

YoloV3 model is pretrained and downloaded (Internet connection is required for the download process).


## 5. Code :
### Synchronization logic:

    f = open("out.txt", "r")
    no_of_vehicles=[]
    no_of_vehicles.append(int(f.readline()))
    no_of_vehicles.append(int(f.readline()))
    no_of_vehicles.append(int(f.readline()))
    no_of_vehicles.append(int(f.readline()))
    baseTimer = 120 # baseTimer = int(input("Enter the base timer value"))
    timeLimits = [5, 30] # timeLimits = list(map(int,input("Enter the time limits ").split()))
    print("Input no of vehicles : ", *no_of_vehicles)
    
    t = [(i / sum(no_of_vehicles)) * baseTimer if timeLimits[0] < (i / sum(no_of_vehicles)) * baseTimer < timeLimits[1] else min(timeLimits, key=lambda x: abs(x - (i / sum(no_of_vehicles)) * baseTimer)) for i in no_of_vehicles]
    print(t, sum(t))


## 6. Conclusion :

The goal of this work is to improve intelligent transport systems by developing a Self-adaptive
algorithm to control road traffic based on deep Learning. This new system facilitates the
movement of cars in intersections, resulting in reducing congestion, less CO2 emissions, etc.
The richness that video data provides highlights the importance of advancing the state-of-the-art
in object detection, classication and tracking for real-time applications. YOLO provides
extremely fast inference speed with slight compromise in accuracy, especially at lower
resolutions and with smaller objects. While real-time inference is possible, applications that
utilize edge devices still require improvements in either the architecture’s design or edge
device’s hardware.
Finally, we have proposed a new algorithm taking this real-time data from YOLO and
optimizing phases in order to reduce vehicle waiting time.


## 7.Extensibility :
You can easily extend this project by changing the classes you are interested in detecting and tracking (see what classes does YoloV3 support and/or change the neural network used by tensornets for better speed/accuracy.
