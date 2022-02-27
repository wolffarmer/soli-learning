## Introduction

This is the open source evaluation code base of our paper:

**Interacting with Soli: Exploring Fine-Grained Dynamic Gesture Recognition
in the Radio-Frequency Spectrum** <br />
Saiwen Wang, Jie Song, Jamie Lien, Poupyrev Ivan, Otmar Hilliges <br />
(link to the [paper](http://bit.ly/2ftSRcn))

##  install python env  
 install python3.6 env with python package "torch matplotlib h5py" 

## Data loading and preprocessing

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

## Parameters
Basic parameters can bee seen at the bottom of **'train.py'** packed by parser.

## Training
**'train.py'** will load and process the data as described above, and train a CNN-LSTM model.
Predictions are calculated based only on the last hidden LSTM state. Training is done using Negative log loss using true labels. Run command for training with default configurations:

`python train.py`

## Logging
For each run, a folder named by date and time will be created with a log file containing info about the parameters. Losses arrays, accuracy arrays, figures and the trained model are saved there as well.

![Alt text](acc_epochs.png?raw=true "Title")