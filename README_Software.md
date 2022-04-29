<h1 align="center">Software Report</h1>

<p align="center"><b>Team 13: C-V2X Misbehavior Detection System</b></p>

<br/>


## Navigation

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#software-report">Title</a>
    </li>
    <li>
      <a href="#overview">Overview</a>
    </li>
    <li>
      <a href="#repositories">Repositories</a>
    </li>
    <li>
      <a href="#c-v2x-machine-learning-via-resource-block-allocation">C-V2X Machine Learning via Resource Block Allocation</a>
    </li>
    <li>
      <a href="#c-v2x-traffic-generator">C-V2X Traffic Generator</a>
    </li>
    <li>
      <a href="#gnuradio-rx-jammer">GNURadio RX Jammer</a>
    </li>
    <li>
      <a href="#machine-learning-via-iq-data">Machine Learning via IQ Data</a>
    </li>
    <li>
      <a href="#modsrsran">ModSrsRAN</a>
    </li>
  </ol>
</details>

<br/>


## Overview

[Describe Role of Software in Project]

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## Repositories

Due to the diversity of technologies used, this project leverages multiple repositories within the <a href="https://github.com/C-V2X-Senior-Design">C-V2X Senior Design Github Organization</a>. These include modified forks of existing radio software repositories and original repositories for machine learning model generation. Each repository in-turn has its own README, highlights of which are included herein.

Substantial repositories used throughout the project's lifecycle are listed below and are described in further detail under their own headings.

* <a href="https://github.com/C-V2X-Senior-Design/CV2X_MachineLearning">C-V2X Machine Learning</a>
  * A python based machine-learning suite designed to generate and evaluate misbehavior-detection models trained on resource block allocation data
  * <a href="https://github.com/C-V2X-Senior-Design/CV2X_MachineLearning/blob/main/README.md#C-V2X-Machine-Learning">README</a>

* <a href="https://github.com/C-V2X-Senior-Design/cv2x-traffic-generator">C-V2X Traffic Generator</a>
  * A fork of Fabian Eckerman's <a href="https://github.com/FabianEckermann/cv2x-traffic-generator">Cellular Vehicle-to-Everything Traffic Generator</a> repository used in simulating and testing C-V2X traffic
  * <a href="https://github.com/FabianEckermann/cv2x-traffic-generator/blob/master/README.md#Cellular-Vehicle-to-Everything-Traffic-Generator">README</a>

* <a href="https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming">GNURadio RX Jammer</a>
  * A frequency-hopping jammer based on the work of WPI's Yaya Brown and Cynthia Teng, linked <a href="https://digital.wpi.edu/concern/student_works/hm50tv580?locale=en">here</a>
  * <a href="https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/README.md#gnuradioRX-Jamming">README</a>

* <a href="https://github.com/C-V2X-Senior-Design/MachineLearning_Yixiu">Machine Learning Yixiu</a>
  * A python based machine-learning suite designed to generate and evaluate misbehavior-detection models trained on I/Q data
  * <a href="https://github.com/C-V2X-Senior-Design/MachineLearning_Yixiu/blob/main/README.md#MachineLearning_Yixiu">README</a>

* <a href="https://github.com/C-V2X-Senior-Design/modSrsRAN">ModSrsRAN</a>
  * A fork of the <a href="https://github.com/srsran/srsRAN">srsRAN</a> repository with added code to automate building, running, extracting radio metrics such as I/Q data and resource block allocation
  * Superseded by the C-V2X traffic generator code, which is more specific to the C-V2X protocol
  * <a href="https://github.com/C-V2X-Senior-Design/modSrsRAN/blob/master/README.md#modsrsran">README</a>

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## C-V2X Machine Learning via Resource Block Allocation

There are two main files for operating the machine learning models with resource block allocations:  
- **CreateModels.py**<br/>
Creates, trains, and tests the data developed by the [simulator library](https://github.com/C-V2X-Senior-Design/CV2X_MachineLearning/blob/main/simulator.py). After testing and evaluating new models, each model is saved in a directory called `models/`. 

- **Evaluation.py**<br/>
Evaluates models in the `models/` directory using data generated located in the `data/` directory. It also evaluates the data using [scikit learn](https://scikit-learn.org/stable/) algorithms.
<br/><br/>
#### Methodology
Approaching resource block allocations with Convolutional Neural Networks (CNN) allows for us to use these powerful ML architectures to determine if the signal is in a jammed state or not. The method derives from a simple case, in which we developed the simulator library, to contain boolean values during each subchannel and subframe show the signal's state.
<img src="https://camo.githubusercontent.com/8d628b2aedac8253766eb99f48042d9d105c2a02bbd1fcb3cc54fcaacb3ede86/68747470733a2f2f72666d772e656d2e6b657973696768742e636f6d2f776972656c6573732f68656c7066696c65732f3839363030622f77656268656c702f73756273797374656d732f6c74652f636f6e74656e742f7265736f75726365732f696d6167652f6c74655f6672616d652e706e67"><br/>
When a subchannel has a `FALSE` boolean value, the resource block is unused. When the signal is jammed; there would be atleast one `FALSE` boolean bit for every ~2 subchannels. Using a CNN model allows for pattern recognition to find the state of the signal, most models created follow this rule as shown using the MNIST dataset.<br/>
<br/>
An example of a resource block diagram generated by the simulator library (Key: Yellow = 1, Blue = 0):
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8b71116d-6eb2-4664-8193-05b5702d439a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220429%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220429T194100Z&X-Amz-Expires=86400&X-Amz-Signature=3b417659b352e182cb4fc1f06847081feb39ad00723ee98dd4eff50cf4b16b98&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject">
<br/>
An example of a CNN model using resource block allocation:
```python
ImprovedCNNModel
Model: "sequential_3"
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 flatten_3 (Flatten)         (None, 500)               0

 dense_6 (Dense)             (None, 256)               128256

 dense_7 (Dense)             (None, 128)               32896

 dense_8 (Dense)             (None, 64)                8256

 dense_9 (Dense)             (None, 2)                 130

=================================================================
Total params: 169,538
Trainable params: 169,538
Non-trainable params: 0
_________________________________________________________________
63/63 - 1s - loss: 7.6662 - accuracy: 0.5030 - 693ms/epoch - 11ms/step
```

### Getting Started
To get started on using the machine learning tool with resource block allocations, install the required packages and use the default models provided in the [models library](https://github.com/C-V2X-Senior-Design/CV2X_MachineLearning/blob/main/models.py)<br/>
For more information, read over the [README.md](https://github.com/C-V2X-Senior-Design/CV2X_MachineLearning)
<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## C-V2X Traffic Generator


We used Fabian Eckermann's [`cv2x-traffic-generator`](https://github.com/FabianEckermann/cv2x-traffic-generator) library in order to generate OTA c-v2x traffic. The citation for his work is the following:

F. Eckermann, C. Wietfeld, *SDR-based open-source C-V2X traffic generator for stress testing vehicular communication*, In 2021 IEEE 93rd Vehicular Technology Conference (VTC-Spring), Helsinki, Finland, April 2021.

[@Julia here]


<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## GNURadio RX Jammer

[@Sam and @Max here]

The jammer we are using is a modified version of one written by YaYa Brown and Cynthia Teng of Worcester Polytechnic Institute. This jammer does not work with the latest version of gnuradio due to the `ofdm mod` block being phased out. The workaround to this was to use a docker image provided by our graduate student advisor and client, Stefan Gvozdenovic, which uses gnuradio version 3.7.11. The docker image is available [here](https://github.com/gefa/cv2x-docker-grc3.7).

YaYa Brown and Cynthia Teng's paper (which links to jammer) is available [here](https://digital.wpi.edu/concern/student_works/hm50tv580?locale=en) and the citation for their work is the following:

*Brown, YaYa Mao, and Cynthia Teng. *Lte Frequency Hopping Jammer.* : Worcester Polytechnic Institute, 2019.

### Jammer Modifications

The following modifications were made to the jammer code:
* `random.randrange(2.6775e9,2.6825e9,1e3))` changed to `random.randrange(5.9165e9,5.917e9,1e3)` (center frequency)
* `time.sleep(1.0 / (40))` changed to `time.sleep(1.0)` (duration between jamming frequency hopping)

### Receiver

Our receiver code for data collection and visualization was written in gnuradio:
![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/receiver_blocks.png?raw=true)

After adjusting gain and squelch in order to remove most noise, we collected data for the following scenarios:

![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/cv2x_transmit.gif?raw=true)*Our receiver capturing an OTA `cv2x_traffic_generator` c-v2x traffic signal*

![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/jammer_transmit.gif?raw=true)*Our receiver capturing the OTA `./top_block.py` jammer signal*

![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/jammed_cv2x.gif?raw=true)*Jammed c-v2x traffic*


<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>



## Machine Learning via IQ Data

Deep learning models have a better model architecture compared to other approaches (E.g. our simple CNN with Q-learning integrated.), so it can utilize our limited computing resources much more efficiently. Furthermore, deep learning models have a huge number of learnable weights and possibly can outperform other potential approaches. 

Here is a completely new approach of making threel trials based on a graduate team’s research in Noiselab UCSD. Those trial models are separately listed below for parts worth mentioning:

* Robust CNN (Convolutional Neural Network)
  * – This model provides 87% of accuracy 
* ResNet (Residual Network)
  * – Currently looks good, but not sure if this model will still be suitable if the model is applied on another dataset. 
  * – This model provides 81% of accuracy
* CLDNN (Convolutional Long Short Term Deep Neural Network)
  * – I have additionally  implemented a Pickle data loading technique
  * – Am trying to load with a preprocessed dataset to make the model more responsive
  * – This model provides 84% of accuracy
The figure below will show the architecture of Robust CNN Method(which currently outputs the highest accuracy.)

![Alt Text](https://github.com/C-V2X-Senior-Design/ResourceHub/blob/main/images/Architecture%20(1).PNG?raw=true)

Here are also some result plots collected:
![Alt Text](https://github.com/C-V2X-Senior-Design/ResourceHub/blob/main/images/accuracy.png?raw=true)
![Alt Text](https://github.com/C-V2X-Senior-Design/ResourceHub/blob/main/images/Loss.png?raw=true)

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## ModSrsRAN

[@Julia and @Michael here]

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>
