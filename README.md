## Introduction
The purpose is to build millimeter wave gesture recognition using TI board

### Catalog description
- ai_course : ai videos course for learning the basics of AI
- config:     soli dataset config
- evb:        learning when try to using TI board to generate dataset instead of soli
- *.py      : python code for builindg ai models

### reference  paper info
This is the open source evaluation code base of our paper:

**Interacting with Soli: Exploring Fine-Grained Dynamic Gesture Recognition
in the Radio-Frequency Spectrum** <br />
Saiwen Wang, Jie Song, Jamie Lien, Poupyrev Ivan, Otmar Hilliges <br />
(link to the [paper](http://bit.ly/2ftSRcn))

## Step1: Model training base on soli dataset
Run the paper and training code based on Google soli dataset

###  install python env  
 install python3.6 env with python package "torch matplotlib h5py" 

### Data loading and preprocessing

- Download [dataset](https://polybox.ethz.ch/index.php/s/wG93iTUdvRU8EaT)
  (please let me know when the link doesn't work).
- Train/test split file (in JSON format) we used is stored in the repo
  `config/file_half.json`.
- The dataset contains multiple preprocessed Range-Doppler Image sequences.
  Each sequence is saved as a single HDF5 format data file. File names are
  defined as `[gesture ID]_[session ID]_[instance ID].h5`. Range-Doppler Image
  data of a specific channel can be accessed by dataset name `ch[channel ID]`.
  Label can be accessed by dataset name `label`. Range-Doppler Image
  data array has shape of `[number of frame] * 1024` (can be reshape back to 2D Range-Doppler Image to `32 * 32`)
- Dataset session arrangement for evaluation.
  - 11 (gestures) * 25 (instances) * 10 (users) for cross user evaluation:
    session 2 (25), 3 (25), 5 (25), 6 (25), 8 (25), 9 (25), 10 (25), 11 (25),
    12 (25), 13 (25).
  - 11 (gestures) * (50 (instances) * 4 (sessions) +
    25 (instances) * 2 (sessions)) for single user
    cross session evaluation: session 0 (50), 1 (50), 4 (50), 7 (50),
    13 (25), 14 (25).
  - Please refer to the paper for the gesture collecting
    campaign details.
- The gestures are listed in the table below. Each column represents
  one gesture and we snapshot three important steps for each gestures.
  The gesture label is indicated by the number in the circle above. Please
  notice that the gesture label order is different than the paper, as
  we regroup gestures in the paper. Sequences with gesture ID 11 are
  background signals with no presence of hand.

![gesture](http://bit.ly/2fHcMRX)

After downloading the data, extract it (as defualt) to **\dsp** folder.
The preprocessing script **'data_pp_tools.load_data()'** loads and parse the data. The data is splite roughly 50/50 to train/validation by the same configuration file from the original authors. Each data point is a sequence of variable length of 1024 dimensional vector which are reshaped to a [32,32] 2d Doppler map [range, velocity]. 
![Alt text](2d_sample.png?raw=true "Title")

The preprocessing script truncates the data points to equal length of 40 (as the authors mention in their paper). 33 & 23 sequences are droped from the training & validation sets respectivly as they have less than 40 samples.

### Parameters
Basic parameters can bee seen at the bottom of **'train.py'** packed by parser.

### Training
**'train.py'** will load and process the data as described above, and train a CNN-LSTM model.
Predictions are calculated based only on the last hidden LSTM state. Training is done using Negative log loss using true labels. Run command for training with default configurations:

`python train.py`

### Logging
For each run, a folder named by date and time will be created with a log file containing info about the parameters. Losses arrays, accuracy arrays, figures and the trained model are saved there as well.

![Alt text](acc_epochs.png?raw=true "Title")

## Step2: Gesture data acquisition based on TI board（Quite difficult）
Based on the data set collected by hardware, learn how to collect and label data
- read [evb/ti-board.md](evb/ti-board.md) you need buy board,then config hardware and software，There will be many problems in software and hardware configuration. Please refer to the official documents
- Data can be collected according to the gestures defined by soli. It is recommended that at least 10 people be involved
## Step3: Model training base on TI dataset
Replace the soli data set in the first step with the data set collected in the second step to train the offline AI model
- Replacement dataset and data preprocessing method，There is basically no need to modify other places

## Step4: Real time gesture detection
Realization of real-time detection system on PC based on Ti board dataset
- Read the data of mmware studio in real time through python, preprocess the data, and then conduct model reasoning. You can display the gesture recognition results according to the log data, or draw your own UI to display the gesture recognition results

## Reference items
- https://github.com/sholevs66/Deep-Soli---Hand-Gesture-recognition
- https://github.com/wolffarmer/deep-soli

