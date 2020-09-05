# Ramanujan

PROBLEM STATEMENT 1: HANDWRITTEN MATHEMATICAL EQUATION SOLVER

Solving mathematical equation is tedious task. There are various domains in mathematics which approaches problems in different manner. In this particular application we will be building mobile phone application which will be used to scan handwritten text and get step by step

solution for various mathematical problems.

## Branches:

We have divided the project 3 parts:

- **Pipeline** handled by Akashdeep
- **Open CV / Math’s Problem extraction** handled by Mahij & Mohit
- **Solver** handled by Ankit Sinha

## Equations Currently (dated: 30/06/2020) working on:

- Basic Algebra (Till 10th standard)
- Basic math

## Libraries:

- Keras
- Opencv
- Numpy
- Django
- Requests
- Numpy
- Sympy

## Basic Flow Diagram

![Architecture/image3.png](Architecture/image3.png)

## Details by **Pipeline Team**

### By Akashdeep Dhar:

![Architecture/image4.png](Architecture/image4.png)

1. Designed three pipelines and image/data transfer
2. user2read for conveying problem image to statement detector
3. read2solv for conveying detected statement to problem solver
4. solv2user for conveying obtained solution to end user

### Note
This documentation was last updated on 09:31 IST, 14 July 2020 by @t0xic0der.

### Introduction
The network pipeline for the project is an REST API built on the Django web framework. Being stateless in nature, either Django REST framework or FastAPI could have been a better choice but writing the API ground up using simply Django helps in facilitating the scalability of the application. The API makes use of HTTP requests for the transaction of JSON objects to and from the server. It has been written in a way in which it can be language-agnostic, hence wrapping the API around any kind of application - be it an mobile application, desktop software or a website, should be a piece of cake.

### Construction
As the actual implementation of Ramanujan involves getting the image file from the user, reading it for any textual content of any mathematical expression, solving the obtained mathematical expression and then finally returning the solution to the user - the API is made low-level to actually follow the stages exhibited by the underlying driver code. Hence there are three underlying applications in the API.

1. **`user2read`** - This application receives an image file from the user and sends it over to the expression recognition and detection system. The output of this application is a mathematical expression in string format.
2. **`read2solv`** - The output of `user2read` application is then conveyed as an input to this application where the mathematical expression string is evaluated with Python's standard `eval` procedure. The obtained result is in string format.
3. **`solv2user`** - The output of `read2solv` application is then conveyed as an input to this application where the evaluated result is sent back to the `conduit` application. This is then sent back to user as the final output.
4. **`conduit`** - This is a proto-application which acts as a layer of contact between the user and the other three applications. This sends the file to the `user2read` application and receives the output from the `solv2user` application.

### Details

1. **Why did you prefer to use multiple applications when you could have done it all in a single application?**  
The use of multiple small applications keeps the code granular and low-level, hence ensuring that every part of the API corresponds properly to their respective driver code. The granularity further helps in development and fixing of a specific application, should it require maintenance while keeping the other parts of the API safe and untouched.

2. **What is the performance hit that the API takes when conversing amongst the applications?**  
There is a marginal performance degradation which might lead to slow donws as less as ~1e-6 seconds due to the fact that the transaction among the multiple applications occur via requests and not by variable sharing.

3. **Why did you use a proto-application called `conduit` when you could have done with just three applications?**  
In the hindsight, the purpose of the `conduit` application is as meagre as receiving files from the user and sending the result back to the user. If you look closely, this lets you keep your other core applications safe by being easily switchable during any kind of availability attacks.

## Details by **Problem Extractor Team**

### By Mohit & Mahij:

1. Used OpenCV contours to create bounding boxes
2. TO solve some problems in this approach
3. transfer learning

![Architecture/image5.png](Architecture/image5.png)

## Model Training 
### By Mohit, Ankit & Mahij:
### Installation

1. Open a terminal and start a virtual environment by using `virtualenv venv`
2. Activate the virtual environment by `source venv/bin/activate`
3. Clone the repository and install the dependencies by executing command:

```
pip3 install -r ./requirements.txt
```

### Get YOLOv3 weights

Already done for you.

```
wget -P model_data https://pjreddie.com/media/files/yolov3.weights
```

### Get YOLOv3-tiny weights(optional)

It will give faster performance. More useful in real-time applications.

```
wget -P model_data https://pjreddie.com/media/files/yolov3-tiny.weights
```

### Steps to run

1. Change the directory: `cd transferlearningmodelYOLO`
2. Now put the following command in the terminal

```
python3 detection_custom.py
```

### For custom input

1. Open the file `detection_custom.py`
2. Change the value of the variable `image_path` to path of the source image.
3. Change the `output_path` where you want the resultant image to be stored.
4. The detect_image function will return a string which can be used for further calculations.
5. After making the changes run

```
python3 detection_custom.py
```
### For Equation-input generator

1. Change the directory: `cd transferlearningmodelYOLO`
2.  Change the directory: `cd mnist/Equation_Genrator`
2. Change the value of the variable `image_path` to path of the source image.
3. Change the `output_path` where you want the resultant image to be stored.
4. The detect_image function will return a string which can be used for further calculations.
5. After making the changes run for test data

```
python3 final_test.py 
```
1. Run for train data
```
python3 final_train.py
```

### Steps to Model Training

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

### Credits:

https://github.com/pythonlessons/TensorFlow-2.x-YOLOv3

![Architecture/image6.png](Architecture/image6.png)

## Details by **Problem Solver Team**

### By Ankit Sinha

### Currently worked on:
- Currently we are using Python Eval function
- Parsing the input string for value extraction
- Currently saving the data/value in an array and flag is used for operator
- Have the array indexing for optimal storage and generalized equations
- Looking over library like sympy and maths for providing the solution.
- One of more important task is to make a hierarchical structure for BODMAS or equation integrity

### Have to work on
- Have to Integrate Solver Engine   
- Different type of equations solver 
- system to send a equation to correct solver 


![Architecture/image7.png](Architecture/image7.png)
