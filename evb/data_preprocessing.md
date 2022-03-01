# Introduction
This paper introduces gesture recognition based on development board
The soli data set is already the data set after preprocessing. The data of Ti development board needs to be preprocessed by itself

## The original signal is processed into a 2D Doppler image
2D doppler just like a picture，reference code [fmcw_2d_doppler.py](fmcw_2d_doppler.py), 

## Delete DC operation
The original Rd image has a lot of static clutter. It is necessary to separately collect the RD image without hand action scene as the background to obtain the maximum value in the data. 
The subsequent Rd image needs to subtract the maximum value, so as to achieve the effect of removing static clutter
## Crop Rd graph
You will find that when the gesture moves, the RD diagram changes only in a certain area. It is recommended to perform the gesture action below 20cm, 
and matting the RD diagram. Only the changed area range is retained (for example, 128 * 128 is cut to 32 * 32). 
The purpose is to focus only on the changed area. The actual 20cm area can be converted to the calculated distance through the formula.
## Get gesture key information
After removing the static clutter, the RD diagram will be very clean. At this time, 
it will be found that there are still many change points in the data. At this time, 
it is necessary to sort the data in the data, only retain the maximum 10 (configurable) values, and clear the other values. 
The goal is to let the data learn the key points and change trend information
## Save RD data
Save each frame of RD diagram to a file for subsequent AI model training
