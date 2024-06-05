# Fault-Classification-for-rotating-machinery-components-using-CNN
# Abstract 

The aim of this work is to develop, implement and validate a neural predictive maintenance algorithm for rotating device bearings. This algorithm is designed to analyze the created time-frequency spectrum based on diagnostic data and, on this basis, classify the condition of the bearing. The project will test various approaches to spectrum analysis using artificial neural networks and signal processing technologies.

The development of this algorithm aims to find the answer to the question: how can the potential of artificial intelligence and neural networks be used to diagnose and predict failures of rotating devices? How can the analysis of various types of spectra help to improve the efficiency and reliability of these devices? The development of this algorithm is aimed at answering the question: how can the potential of artificial intelligence and neural networks be used to apply and predict indicators of rotating devices? How can spectrum type analysis work for performance and these devices?

# Data

The data is collected from the Case Western Reserve University. The [website](https://engineering.case.edu/bearingdatacenter)
provides access to ball bearing test data for normal and faulty bearings.  Experiments is unique in that the actual test conditions of the motor as well as the bearing fault status have been carefully documented for each experiment.

Motor bearings were seeded with faults using electro-discharge machining (EDM). Faults ranging from 0.007 inches in diameter to 0.040 inches in diameter were introduced separately at the inner raceway, rolling element (i.e. ball) and outer raceway. Faulted bearings were reinstalled into the test motor and vibration data was recorded for motor loads of 0 to 3 horsepower (motor speeds of 1797 to 1720 RPM).

Vibration signals of 4 classes of bearings were measured in the experiment, namely:

-normal bearing without fault (N)

-bearing with single point fault at the inner raceway (IR)

-bearing with single point fault at the outer raceway (OR)

-bearing with single point fault at the ball (B).

# Data Pre-Processing

Deep learning algorithms require a lot of data. The larger their number, the higher the efficiency. The Case Western Bearing dataset is not a huge dataset. Therefore, data from each category is collected in segments of length 784 and transformed into a 2-D matrix of size (28 by 28). The offset is 300, which causes overlapping of segments, but significantly increases the number of examples provided at the network input. The total data size is therefore (9246, 32, 32.1). The data is randomly divided into a training set of 70% and a test set of 30%. Such a transformation was performed on the raw data vector, data after the FFT transform, data after the STFT transform and data after the CWT transform.

# Classification Models

A convolutional neural network model was used for feature extraction and classification. The number of classes for each dataset is 14. The model used is an 8-layer deep learning network. The network architecture is based on the LeNet 5 architecture. It contains 2 feature detection or extraction blocks. Each feature extraction block consists of convolutional layers, ReLU activation unit, and max-pooling layers. Both feature extraction blocks contain convolutional filters of size 5 × 5, max-pooling layer of size 2 × 2, step size of 1, ReLU activation unit. The number of layers used in the blocks are 64 and 32, respectively. A layer was then applied to flatten the data before entering the dense layers. Two dense layers of sizes 120 and 84 were successively used. The last layer consists of 14 neurons used to label the type of damage and the SoftMax activation function. The learning rate was set to 0.001 and the Adam optimizer was used.
![image](https://github.com/justyna1919/Fault-Classification-for-rotating-machinery-components-using-CNN/assets/118431395/58293162-afa6-4dfb-846f-f09dd14533fe)

# Results

![image](https://github.com/justyna1919/Fault-Classification-for-rotating-machinery-components-using-CNN/assets/118431395/28df9990-b87e-4fb6-867b-57d627a7addb)
![image](https://github.com/justyna1919/Fault-Classification-for-rotating-machinery-components-using-CNN/assets/118431395/600803b3-6546-4571-9f7e-b2442f1d1457)

The network achieves 97.8% accuracy on raw data vector, 90.09% on FFT transformed data, 92.47% on STFT transformed data, 95.53% on CWT transformed data . The confusion matrix shows that the algorithm shows the best efficiency for the raw data vector and data after CWT transformation. In the case of data after FFT and STFT transformation, the biggest mistake is made for the class of bearing with a damaged inner ring with a value of 0.36 mm (014_IR), incorrectly interpreting it as a bearing with a damaged ball with a value of 0.36 mm (014_B).

![image](https://github.com/justyna1919/Fault-Classification-for-rotating-machinery-components-using-CNN/assets/118431395/c7940ed3-a4b1-4b6a-8002-c31f25784f30)

# Conclusions 

The network implemented on the raw data vector shows the highest accuracy 99.44% for training data and 97.8% for test data. The network implemented on data previously subjected to STFT transformation has the lowest accuracy 89.6% for training data and 84.7% for test data. For CWT transformed data, there is the largest difference between the training data accuracy of 97.46% and the test data accuracy of 89.1%. The smallest difference between the accuracy of training data and the accuracy of test data is demonstrated by the network implemented on data after FFT transformation, and it is 91.22% and 90.09%, respectively.

![image](https://github.com/justyna1919/Fault-Classification-for-rotating-machinery-components-using-CNN/assets/118431395/78b7569e-6f4e-4a3d-a7b1-9f44c95b7b44)
