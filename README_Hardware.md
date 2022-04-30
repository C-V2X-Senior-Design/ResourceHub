<h1 align="center">Hardware Report</h1>

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
      <a href="#bill-of-materials">Bill Of Materials</a>
    </li>
    <li>
      <a href="#data-sheets">Data Sheets</a>
    </li>
    <li>
      <a href="#lab-setup">Lab Setup</a>
    </li>
  </ol>
</details>

<br/>


## Overview

Hardware sat at the heart of this project, as all the data created had to be analog. The three National Instruments software defined radios, or SDRs read in C code to trahslate function calls into configurations for the radio, such as the gain, FFT size, and frequency to broadcast at, among other capabilities. These served as the transmitter, reciever, and jammer for our mockup. To support and program these, we had two desktops with Dragon OS. This allowed us to not just have a consistant station to program the radios, but monitoring software such as GQRX to confirm signal stability and strength. The two Keysight signal generators made sure the radios had a precise pulse per second, or PPS for timekeeping, as well as a 10 MHz reference waveform to function as the clock for our V2X signal. The oscilloscope from LeCroy gave us the capibility to confirm the accuracy of the signals. Finally, the CDA 8 Channel Clock Distribution Module, or Octoclock for short, was later used for a more unified apporach for a GPS sync between the radios. Overall, each of these products were vital to delivering data over the air between radios.

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## Bill Of Materials
<table>
    <tbody>
        <tr">
            <td colspan="1" rowspan="2">
                <p></p>
                <p align=center>No.</p>
            </td>
            <td colspan="1" rowspan="2">
                <p></p>
                <p align=center>Project-related Device &amp; Materials</p>
            </td>
            <td colspan="1" rowspan="2">
                <p></p>
                <p align=center>Manufacturer</p>
            </td>
            <td colspan="2" rowspan="1">
                <p align=center>Specs of Device &amp; Material</p>
            </td>
            <td colspan="1" rowspan="2">
                <p></p>
                <p align=center>Total Cost ($)</p>
            </td>
        </tr>
        <tr">
            <td colspan="1" rowspan="1">
                <p>Quantity </span></p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Unit Cost ($)</p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>1</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>CDA 2990 8 Channel Clock Distribution Module</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>National Instruments</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>1</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>2,866</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>2,866</p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>2</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Desktop with Dragon OS</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Dell</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>2</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>Around 500</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>1,000</p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>3</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Keysight 33500B signal generator</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Keysight Technologies</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>2</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>1,979</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>3,958</p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>4</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>LeCroy Wavesurfer 422 Oscilloscope</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Teledyne Lecroy</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>1</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>5,141</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>5,141</p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>5</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>NI 2901 USRP (AFRL provided)</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>National Instruments</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>3</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>2,010</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>6,030</p>
            </td>
        </tr>
        <tr>
            <td colspan="5" rowspan="1">
                <p>Total Cost</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>18,995</p>
            </td>
        </tr>
    </tbody>
</table>

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>


## Data Sheets

<table>
    <tbody>
        <tr">
            <td colspan="1" rowspan="1">
                <p align=center>No.</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>Device</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>Datasheet</p>
            </td>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>1</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>CDA 2990 8 Channel Clock Distribution Module</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center><a href="https://www.ni.com/pdf/dspdf/en/ds-572">link</a></p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>2</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Desktop with Dragon OS</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center>N/A<a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">.</a></p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>3</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>Keysight 33500B signal generator</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center><a href="https://www.keysight.com/us/en/assets/7018-05928/data-sheets/5992-2572.pdf">link</a></p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>4</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>LeCroy Wavesurfer 422 Oscilloscope</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center><a href="https://cdn.teledynelecroy.com/files/manuals/ws-om-e_rev_b.pdf">link</a></p>
            </td>
        </tr>
        <tr>
            <td colspan="1" rowspan="1">
                <p align=center>5</p>
            </td>
            <td colspan="1" rowspan="1">
                <p>NI 2901 USRP (AFRL provided)</p>
            </td>
            <td colspan="1" rowspan="1">
                <p align=center><a href="https://www.ni.com/pdf/manuals/374925c.pdf">link</a></p>
            </td>
        </tr>
    </tbody>
</table>

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>

                                        
## Lab Setup

![LabSetup](./images/Labsetup.png)

Above are the devices described in the overview. Two desktops, with the one on the left behind the monitor. The two signal generators are located in the middle, with one SDR on top. The other two radios are stacked on top of one another on the right desktop. Finally, the Oscilloscope is behind the left monitor.

### Setup Procedure
                                        
Perform the following steps to set up USRPs for communication
                                        
* Connect each USRP to separate power sources and computers.
  * You can ensure these USRPs have been properly connected and are visible to the computer by running  `uhd_find_devices` on the command-line of the connected PC.
* Connect each USRP to one of the following:
  * Two signal generators connected to the same relative inputs on each USRP with the following settings:
    * A “Pulse, Off, 50 Ohm” wave which is “AM modulated by sine”, frequency of 1 Hertz, amplitude of 10 dBm
    * A “Square, Off, 50 Ohm” wave which is “AM modulated by sine”, frequency of 10 Megahertz, amplitude of 100 millivolts (this should probably be 10 dBm)
  * The GPS output of the 8 channel clock distribution module
* Enable communication between USRPs by doing one of the following:
  * Attaching antennae to the transmit and receive inputs of each USRP
  * Connect the transmit input of each USRP to the receive inputs of all other USRPs via cable, using wire splitters if necessary
                                        
Now, use software such as GQRX and SrsRAN to confirm that your radios are communicating.

<br/>
<p align="center">(<a href="#navigation">to table of contents</a>)</p>
