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

<img src="https://drive.google.com/file/d/1OX_fcbvY4mwOvrJPNE9KVrnuLKltpCy0/view?usp=sharing" alt="system_diagram.png" />

*Figure 1: Architecture diagram of our current system*

The hardware code is an extension of lab 3’s existing code with minimal tweeks:
 - Changed audio output to mono-only, due to our chosen ML model’s limitation of only being able to process mono audio
 - Set sample rate to 32kHz
 - Set recording buffer size to 1000
 
Our original system’s PS design is currently not fully implemented.
- The planned design was intended to have audio_capture and the ML animal detection model run concurrently, a feature that is not yet successfully implemented.
- Hence, our audio capture and ML model software is run on two separate boards at the moment. Audio capture is logged and stored on the SD card, which can be taken out and inserted into another board for ML sound processing, writing results back to the SD card as well.

Our planned intended design and its represented architecture diagram will be further elaborated below in section 6.

## 3. Board + program setup guide

text

## 4. Usage guide + expected behaviour of implementation

text

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



