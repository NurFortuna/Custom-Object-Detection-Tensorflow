# Custom-Object-Detection-Tensorflow :sparkling_heart:

#### I explain train your custom object detection with Tensorflow 2. I used Chess Pieces Dataset from Roboflow. In this project, I will use the ssd_mobilenet_v2 320x320 pretrained model. [others](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md)

:pushpin: [Chess Pieces Dataset](https://public.roboflow.com/object-detection/chess-full)

![image](https://user-images.githubusercontent.com/89857618/191898953-ccde6732-d47a-4a8f-98bb-3e9509cc77da.png)

## Installation :woman_technologist:

| -| Windows |
| --- | --- |
|Python| 3.8 |
|TensorFlow | 2.2.0|
| CUDA Toolkit |10.1 |
| CuDNN | 7.6.5 |

#### I created an environment for the required libraries using Anaconda. 

- Type the following command:

```
conda create -n tensorflow pip python=3.8

```
#### The above will create a new virtual environment with name tensorflow. After that Activate the Anaconda virtual environmen and install TensorFlow

```
conda activate tensorflow

pip install --ignore-installed --upgrade tensorflow==2.2.0

```

## TensorFlow Object Detection API Installation 

 Install the TensorFlow Object Detection API.
:pushpin: [TensorFlow Object Detection API ](https://github.com/tensorflow/models/tree/master/research/object_detection)
 ##### The TensorFlow Object Detection API is an open source framework built on top of TensorFlow that makes it easy to construct, train and deploy object detection models.

## Protobuf Installation/Compilation

In a new Terminal, cd into **TensorFlow/models/research/** directory and run the following command:
```
# From within TensorFlow/models/research/
protoc object_detection/protos/*.proto --python_out=.

```
### Install the Object Detection API

Installation of the Object Detection API is achieved by installing the object_detection package. This is done by running the following commands from within Tensorflow\models\research:

```
# From within TensorFlow/models/research/
cp object_detection/packages/tf2/setup.py .
python -m pip install .

```
### Preparing the Dataset :heart_eyes_cat:

As I said at the beginning, I used Chess Pieces Dataset from roboflow for the dataset. You can collect images yourself and use the labelImg package to label images. If you haven't installed the package yet, have a look at the LabelImg Installation.
[labelImg](https://github.com/heartexlabs/labelImg)

 The number of classes is eleven thus it looks like this.
 
 ![image](https://user-images.githubusercontent.com/89857618/191905574-11a98328-7829-4569-a489-1a518b689319.png)

 
 ```
  id: 3
  name: 'white-bishop'
}

item {
  id: 4
  name: 'white-knight'
}

item {
  id: 5
  name: 'white-rook'
}

item {
  id: 6
  name: 'white-pawn'
}

item {
  id: 7
  name: 'black-king'
}

item {
  id: 8
  name: 'black-bishop'
}

item {
  id: 9
  name: 'black-knight'
}

item {
  id: 10
  name: 'black-rook'
}

item {
  id: 11
  name: 'black-pawn'
}


```
 
 ### Create TensorFlow Records 
 
 Convert *.xml to *.record
 
 ![image](https://user-images.githubusercontent.com/89857618/191904381-ce04140a-742d-47a1-8ab1-e7f2aa5b550b.png)
 
  ```
 # Create train data:
python generate_tfrecord.py -x [PATH_TO_IMAGES_FOLDER]/train -l [PATH_TO_ANNOTATIONS_FOLDER]/label_map.pbtxt -o [PATH_TO_ANNOTATIONS_FOLDER]/train.record

# Create test data:
python generate_tfrecord.py -x [PATH_TO_IMAGES_FOLDER]/test -l [PATH_TO_ANNOTATIONS_FOLDER]/label_map.pbtxt -o [PATH_TO_ANNOTATIONS_FOLDER]/test.record
```

### Configure the Training Pipeline
The TensorFlow Object Recognition API provides model configuration through the pipeline.config file that comes with the pre-trained model.


```
training/
├─ ..
│ ---ssd_mobilenet_v2_320x320_coco17_tpu-8/
|     └─ pipeline.config
└─ ...
```
![image](https://user-images.githubusercontent.com/89857618/191906263-15d989da-56ec-4c63-8392-2700b76d2338.png)


### Training the Model :muscle:

I used the following command:
```
python exporter_main_v2.py --trained_checkpoint_dir=training --output_directory=modelim --pipeline_config_path=training/config.config
```

