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
      <a href="#modsrsran">ModSrsRAN</a>
    </li>
  </ol>
</details>

<br/>


## Overview

The software in this was primarily used in three sections: the normal transmission and reception of radio signals, the jamming of the aforementioned signal, and the machine learning models. ModSrsRAN was used as a baseline to automate building and configuration, along with some added code for data extraction. It also served as a starting point for general LTE signal over the air transmission. Later, we mainly used C-V2X Traffic Generator, a more specialized library created by Fabian Eckerman with proper V2X signal implementation. To create the jammer, We built off of the LTE jammer from two graduate students at WPI, making it a a midband jammer with a slower hop speed, thorugh direct modification of Python blocks generated from GNURadio. Last but not least are the two machine learning repositories. The Machine Learning Yixiu repository focused on using IQ or interphase/quadrature data of each received segment of signal to differentiate between valid and jammed messages. The C-V2X Machine Learning repository also looked to classify a V2X packet as jammed or clear, but through the use of resource blocks, a method of sending messages used by LTE based protocols that breaks the overall packet into smaller sections. Each repository had a unique role to fulfill, from the creation of the signal itself, to data extraction and algorithmic analysis of the data.

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

[@Jason here]

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

## Jammer Modifications

The following modifications were made to the jammer code:
* `random.randrange(2.6775e9,2.6825e9,1e3))` changed to `random.randrange(5.9165e9,5.917e9,1e3)` (center frequency)
* `time.sleep(1.0 / (40))` changed to `time.sleep(1.0)` (duration between jamming frequency hopping)

## Receiver

Our receiver code for data collection and visualization was written in gnuradio:
![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/receiver_blocks.png?raw=true)

After adjusting gain and squelch in order to remove most noise, we collected data for the following scenarios:

![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/cv2x_transmit.gif?raw=true)*Our receiver capturing an OTA `cv2x_traffic_generator` c-v2x traffic signal*

![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/jammer_transmit.gif?raw=true)*Our receiver capturing the OTA `./top_block.py` jammer signal*

![Alt Text](https://github.com/C-V2X-Senior-Design/gnuradioRX-Jamming/blob/main/img/jammed_cv2x.gif?raw=true)*Jammed c-v2x traffic*


<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## ModSrsRAN

[@Julia and @Michael here]

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>
