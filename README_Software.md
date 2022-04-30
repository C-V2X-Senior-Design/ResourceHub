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


## C-V2X Traffic Generator ([Changelog](#changelog))

We used Fabian Eckermann's [`cv2x-traffic-generator`](https://github.com/FabianEckermann/cv2x-traffic-generator) library in order to generate OTA c-v2x traffic. The citation for his work is the following:

[1] F. Eckermann, C. Wietfeld, *SDR-based open-source C-V2X traffic generator for stress testing vehicular communication*, In 2021 IEEE 93rd Vehicular Technology Conference (VTC-Spring), Helsinki, Finland, April 2021.

Additional reference(s):
  
  [2] Twardokus, Geoff, "Intelligent Lower-Layer Denial-of-Service Attacks Against Cellular Vehicle-to- Everything" (2021). Thesis. Rochester Institute of Technology.

#### Installation and Build 
* Setup the USRP equipment following the <a href="https://github.com/C-V2X-Senior-Design/ResourceHub/blob/main/README_Hardware.md">Lab Setup</a>.
* Clone the forked repository <a href="https://github.com/C-V2X-Senior-Design/cv2x-traffic-generator">here</a>. 
* Create a `build` directory within the `cv2x-traffic-generator` directory with`mkdir build`.
* In `cv2x-traffic-generator` execute `./maker.sh` to compile and build binary executables. 
* Navigate to `build/pssch_ue` and run the C-V2X transmitter with `./cv2x_traffic_generator -d UHD -a clock=external -o <ins>logfile</ins> -n 5 -l 10 -s 0`
* Navigate to `build/cv2x_traffic_generator` and run the C-V2X receiver with `./pssch_ue -o <ins>logfile</ins>`, e.g. `./pssch_ue -o logfile.csv`
    * Alternatively, run the receiver from the `modSrsRan` (repo: <a href="https://github.com/C-V2X-Senior-Design/modSrsRAN">modSrsRan</a>.) with the command `./pssch_ue -o <ins>logfile.csv</ins>`. 
* The results of the run will be located in the <ins>logfile</ins>. 
* The full argument list for the transmitter can be displayed with `./cv2x_traffic_generator --usage`

#### Interpretation of <ins>logfile</ins> output 
* The output is generated by the receiver and one row is generated each time the receiver successfully decodes a sidelink-control (PSCCH) packet. 
* Each row is formatted by {`subframe, timestamp (ms), resource_blocks`} and `resource_block` is a bitmap repesenting the resource block allocation for a single transmission. The resource block allocation is manufactured by an algorithm that derives from the paper [1]. 
* Each bit of the bitmap represents a resource block group (RBG) of the resource pool. 1 indicates that the RBG is used, 0 unused. E.g. if there are 5 sub-channels and each sub-channel is of length 10, the bitmap will have a length of 50. 
* The bitmap abides by the adjacent subchannelization scheme (rationale provided [Issue No.3](#issue-no3)), and contiguous allocation, as is standardardized in SCI Format 1 [1]. 
* `subframe` indicates the subframe index. A frame contains 10 subframes and indices repeat each frame, e.g. `0, 1,..., 9, 0, 1, 2,...`. [2]
* `timestamp` indicates the time of packet reception. 
* Important: The output does not indicate successful decode of transport blocks, as will be explained in the next section.   


## Changelog

#### Issue No.1
No packets were passing the `srslte_pssch_decode` in `pssch_ue.c`, i.e. `num_decoded_tb` always equaled 0, and therefore no PCAPs were generated.

  1. Problemtatic filename:function:linenum
      - `/lib/src/phy/phch/pssch.c:srslte_pssch_decode`:464
      - `/lib/src/phy/phch/pssch.c:srslte_pssch_decode`:487

  2. The Issue
      - It is not passing the checksum, i.e. `srslte_bit_diff()`, which essentially checks that every bit is the same and as a result an error is returned in `pssch_ue.c` indicating the packet cannot be decoded. 
      
  3. How to recreate the error
      - Add `ERROR("Checksum error")` error printing statements to those two places
      - Run `pssch_ue`. You should now see `Checksum error` error messages printed to the console
    
  4. How I "solved" this issue
      - Commented out CRC in `/lib/src/phy/phch/pssch.c:srslte_pssch_decode`:464 and `/lib/src/phy/phch/pssch.c:srslte_pssch_decode`:487
      - Now, `pssch_ue` will generate PCAPs in tmp/pssch.pcap, but this is garbage
 
#### Issue No.2
This is not an issue, but instructions on how to populate the transport block (payload) in C-V2X traffic generator.
  - In the original fork, C-V2X does not populate the `tb` array, possibly because it is only used for stress-testing of SCI. 
  - Edit `tb` to populate the array with up to `SRSLTE_SL_SCH_MAX_TB_LEN` bits. 
  - e.g.: `cv2x_traffic_generator.c`:426 populates `tb` with all 1s. 


#### Issue No.3
(Cross-documented with <a href="https://github.com/C-V2X-Senior-Design/modSrsRAN">modSrsRan</a>)
  - This is not an issue, but rather an explanation for why we do not need to
account for the non-adjacent C-V2X subchannelization scheme, just the adjacent scheme.
Refer to [1] for explanation of C-V2X subchannelization schemes. 

  - `cv2x-traffic-generator-fork/lib/src/phy/common/phy_common_sl.c`:407 defines `* @param adjacency_pscch_pssch subchannelization adjacency`
  - `cv2x_traffic_generator.c`:372 calls `srslte_sl_comm_resource_pool_set_cfg()` which is hardcoded to set `adjacency_pscch_pssch=true`.
  - Why I think true=adjacent and false=non-adjacent lies in `cv2x-traffic-generator-fork/lib/src/phy/ue/ue_sl.c`:658
      ``` 
      if (q->sl_comm_resource_pool.adjacency_pscch_pssch) {
        pscch_prb_start_idx = sub_channel_idx * q->sl_comm_resource_pool.size_sub_channel; 
      } else {
        pscch_prb_start_idx = sub_channel_idx * 2;
      }
      ```
  - If adjacency_pscch_pssch=true, then pssch starting block will be a multiple of the subchannel size, 
  else it is a multiple of 2. 
  - `modSrsRAN/lib/src/phy/common/phy_common_sl.c`:`srsran_sl_comm_resource_pool_get_default_config`:346, which is called in pssch_ue, hardcodes `adjacency_pscch_pssch=true`.


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

[@Yixiu]

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## ModSrsRAN ([Changelog](#changelog-1))

We used Software Radio System's (SRS) [`srsRAN`](https://github.com/srsran/srsRAN) suite in order to implement an end-to-end LTE network and extract IQ data.

#### Installation and Build 
* text

#### Interpretation of <ins>logfile</ins> output 
* text

## Changelog

#### Issue No.1
The srsRAN release 21.10 implementation of pssch_ue.c (found in `modSrsRan/build/lib/examples`) was giving a floating point exception error (GitHub issue in srsRAN open source found here: srsran/srsRAN#838).

  1. Problemtatic filename:function:linenum
      - `/lib/src/phy/sync/sync.c:srsran_sync_set_cp`:446
      - Change:
        ```
        q->nof_symbols = q->frame_size / (q->fft_size + q->cp_len) - 1; // ADDED COMMENT: FLOATING POINT EXCEPTION HAPPENING HERE
        ```

  2. The Issue
      - Both `q->fft_size` and `q->cp_len` are 0 which result in a divide by 0 error.
      
  3. How to recreate the error and debug it
      - Revert to commit 86a094c98e77b32ed0a1edcb053dabbed4b3c48d
      - Add -g flag to cmake line in maker.sh to enable debugging
      - Run: ./maker.sh
      - Navigate to pssch_ue executable: cd /build/lib/examples
      - Run gdb: gdb ./pssch_ue
      - Add breakpoints:
        1. b main
        2. b ue_sync.c:srsran_ue_sync_set_cell
        3. b sync.c:srsran_sync_set_cp
      - Step with 'continue' (c) until you hit error and you should see that you hit the error in sync.c:srsran_sync_set_cp:446
      - Revert back to this commit (which includes debugging print statements) and run the previous steps if you'd like

    
  4. How I "solved" this issue
      - srsran_sync_set_cp is called twice in ue_sync.c:srsran_ue_sync_set_cell:347 and ue_sync.c:srsran_ue_sync_set_cell:350, so I commented them out. Run now, floating point exception should disappear.
      - Another "solution" is to set the `FFT` and `CP_LEN` values to something non-zero, to do this uncomment lines `ue_sync.c`:`srsran_ue_sync_set_cell`:346 and `ue_sync.c`:`srsran_ue_sync_set_cell`:349. 

 
#### Issue No.2

#### Issue No.3


<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>
