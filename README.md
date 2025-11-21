# Wildlife Conservation Detection System on Kria KV260 - Full Usage Guide
Created by:
z5400652 - Edward Wijaya
z5421616 - Andre Tsai
z5430082 - Dennis Sungko
z5483690 - Nicholas Ng

## 1. Overview

The Wildlife Conservation Detection System is an embedded sound recognition system used to detect certain animal species and log detection times for further statistical analysis.

The system is aimed at but not limited to ecological research. As (land) animal species detection is a laborious process requiring constant surveillance, this system provides scientists/researchers a less-intensive way to detect and log appearances of certain species over an extended area, via detecting their sounds.

This system uses the Kria KV260 FPGA to process audio captured via a connected I2S MEMS microphone. The audio is dynamically passed into a machine-learning model which identifies specific animal species based on the sounds they emit near the mic, where the information is logged onto an external drive.

## 2. System architecture (PS and PL integration)

A rough structure of our current system is shown as an architecture diagram in *Figure 1*:

![Architecture diagram of our current system](https://drive.google.com/uc?export=view&id=1OX_fcbvY4mwOvrJPNE9KVrnuLKltpCy0)

*Figure 1: Architecture diagram of our current system*

The hardware code is an extension of lab 3’s existing code with minimal tweeks:
 - Changed audio output to mono-only, due to our chosen ML model’s limitation of only being able to process mono audio
 - Set sample rate to 32kHz
 - Set recording buffer size to 1000
 
Our original system’s PS design is currently not fully implemented.
- The planned design was intended to have audio_capture and the ML animal detection model run concurrently, a feature that is not yet successfully implemented.
- Hence, our audio capture and ML model software is run on two separate boards at the moment. Audio capture is logged and stored on the SD card, which can be taken out and inserted into another board for ML sound processing, writing results back to the SD card as well.

Our planned intended design and its represented architecture diagram will be further elaborated below in section 6.

As per software code run on baremetal, the following main functions are used:
- main() - a FSM for the board to turn on and off audio recording
- audio_capture()
Captures audio buffers until recording is turned off by main() fsm
Creates .wav file the recorded audio buffers. Also converts 32KHz to 16KHz sampling for ML usage. 
Logs recording data onto a text file

For the ML model, we originally used a pretrained model which is YamNet MobileNetV1 which we extract the embeddings of and run our own custom CV deep training script. We scoured the internet for datasets which for now we narrow down to birds due to their characteristic voices. Our current model now runs a tflite version of the original model which has been deep trained on Ubuntu on a separate board. 

## 3. Board + program setup guide
Board setup: (same as Lab 1-3)
1. Plug in “design proj A/B PMod board” into Kria KV260 “J2”.
2. Plug in a I2S MEMS mic into “Mic R”.
3. Connect and power up the board:
    a. Connect the USB cable to the FPGA “J4” and to the user’s computer.
    b. Connect the power cable to the FPGA “J12” and to the power.
4. Open PuTTY → connect right serial port → Baud rate 115200, no flow control.
5. Put the board into standalone mode via Xilinx xsct.

![boot_up_manual](https://drive.google.com/uc?export=view&id=18LpOxYyWkc8C63f2NdrtS6UB8_CJcBfC)
6. Plug in an SD card into the board’s J11 SD card slot.

Create vitis application:
1. Create a new platform using settings from Labs 1-3, use the .xsa file “sd_card_attempt_6_1000_mono.xsa” as provided in the files submission. Do not build the platform yet.
2. Enable Xilinx FAT file system reading for SD card access
    a. Open up platform.spr.
    b. On the platform.spr tab, click on “psu_cortexa53_0” →  “standalone on psu_cortexa53_0” → “Board Support Package”. Click on “Modify BSP Settings”.
![vitis_creation](https://drive.google.com/uc?export=view&id=1mYCoy5DOF5Jgjq7-_ZBThaMHGih8e-6g)
    c. Tick the box next to “xilffs” and press “Ok”.
![vitis_creation_2](https://drive.google.com/uc?export=view&id=1mYCoy5DOF5Jgjq7-_ZBThaMHGih8e-6g)




## 4. Usage guide + expected behaviour of implementation


## 5. Custom configuration guide

text

## 6. Project Challenges

text

## 7. Project extension / bigger picture

text


## Examples:
Take a look at these couple examples that I have in my own portfolio:

**Palettable:** https://github.com/alecortega/palettable

**Twitter Battle:** https://github.com/alecortega/twitter-battle

**Patch Panel:** https://github.com/alecortega/patch-panel



