# Model-Training-DOCS

# Transfer Learning model for Mathematical expressions recognition using Tensorflow 2.x and YOLOv3

## Installation

1. Open a terminal and start a virtual environment by using `virtualenv venv`
2. Activate the virtual environment by `source venv/bin/activate`
3. Clone the repository and install the dependencies by executing command:

```
pip3 install -r ./requirements.txt
```

# Get YOLOv3 weights

Already done for you.

```
wget -P model_data https://pjreddie.com/media/files/yolov3.weights
```

# Get YOLOv3-tiny weights(optional)

It will give faster performance. More useful in real-time applications.

```
wget -P model_data https://pjreddie.com/media/files/yolov3-tiny.weights
```

## Steps to run

1. Change the directory: `cd transferlearningmodelYOLO`
2. Now put the following command in the terminal

```
python3 detection_custom.py
```

## For custom input

1. Open the file `detection_custom.py`
2. Change the value of the variable `image_path` to path of the source image.
3. Change the `output_path` where you want the resultant image to be stored.
4. The detect_image function will return a string which can be used for further calculations.
5. After making the changes run

```
python3 detection_custom.py
```

## Steps to Model Training

1. Change the directory: `cd transferlearningmodelYOLO`
2. Open  `yolov3/config.py` 
3. Provide the path to Training data, Testing Data and names
4. Then configure the Epochs and Batch Size in same file (`yolov3/config.py`)
5. Change the directory: `cd transferlearningmodelYOLO`
6. Now put the following command in the terminal

```
python3 train.py
```

1. While Training you can run tensor board 

```
tensorboard --logdir ./log
```

# Credits:

https://github.com/pythonlessons/TensorFlow-2.x-YOLOv3