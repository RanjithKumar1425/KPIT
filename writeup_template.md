## Writeup Template

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./camera_cal/calibration2.jpg "calibration Input"
[image2]: ./writeupImage/corners.jpg "Coners Ploted"
[image3]: ./writeupImage/calibration2_undist.jpg "Undistorted Image"
[image4]: ./writeupImage/straight_lines1_undist.jpg "Sobel X"
[image5]: ./writeupImage/straight_lines1_sobel.jpg "Sobel X"
[image6]: ./writeupImage/straight_lines1_s_threshold.jpg "S Threshold in HSL"
[image7]: ./writeupImage/straight_lines1_binary.jpg "Binary Combined"
[image8]: ./writeupImage/straight_lines1_warped.jpg "Wraped"
[image8]: ./writeupImage/straight_lines1_warped.jpg "Fitted Polynomial"
[image10]: ./output_images/straight_lines1.jpg "Final Input"
[video1]: ./project_video_out_subclip.mp4 "Video"


### Writeup 

### Camera Calibration

The code for this step is contained in the 3rd code cell of the IPython notebook located in "./AdvancelaneFinding_Final.ipynb" 

Steps for Camera Calibration:
    Convert the Image to Gray Scale.
    Find the Corners using the findChessboardCorners method in Opencv. (No of X and Y points  9 and 6 resp)
    Add the Object and Image points to array
    Call calibrateCamera in Opencv to get the distortion coefficients using Object and Image Points.
    
Illustrtaion:

![alt text][image1]
![alt text][image2] 
![alt text][image3]

Need to Explore more Color and Gradient combination to get smoother video in Challenge Video.

### Pipeline (single images)

#### 1. Distortion-corrected image.

Un-Distor the Image by calling undistort method in Opencv 

Sample Original and Un-distored Image are below

![alt text][image4]

#### 2.Color and Gradient Threshold.

I tried to use the below Gradient Combination.

SobelX 
S component in HLS

Illustration:

SobelX
![alt text][image5]

S Component in HLS
![alt text][image6]

Comnined Binary
![alt text][image7]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

Code for Perpective transform is cell No:6 of the IPython notebook located in "./AdvancelaneFinding_Final.ipynb" 

--Python Code snippet
src = np.float32([[490, 470], [810, 470], [1250, 740], [0, 740]])
dst = np.float32([[0, 0], [1280, 0], [1250, 720], [40, 720]])

This resulted in the following source and destination points:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 490, 470      | 0, 0           | 
| 0, 740        | 1280, 0        |
| 1250, 740     | 1250, 720      |
| 810, 470      | 40, 720        |

Sample Wraped Image Sample

![alt text][image8]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Code for identifying and Fitting the polynomial are in  cell No: 2 of the IPython notebook located in "./AdvancelaneFinding_Final.ipynb"
Line object has code to find Lane lines fresh or search around the last polonomial lines.


![alt text][image9]

#### 5. The radius of curvature of the lane and the position of the vehicle with respect to center.

Code for radius of curvature are in  cell No:10 of the IPython notebook located in "./AdvancelaneFinding_Final.ipynb" 


#### 6. Final Image

Draw the Lane line on the actual Image.
Code for drawinf the Lane line are  is in  cell No: of the IPython notebook located in "./AdvancelaneFinding_Final.ipynb" 

![alt text][image10]

---

### Pipeline (video)

Code for Video Pipeline is in cell No:11 of the IPython notebook located in "./AdvancelaneFinding_Final.ipynb"

For every frame , we try to find the line alone the Previous Polynomial coefficient. And use the Averaging of last 15 Frames values to get the smoother value. 


#### 1. Final Output Video.

Here's a [link to my video result](./project_video.mp4)

---

### Discussion

Above Pipeline was working fine for Project Video, but has lot to imporove in challenge video.
Need to try out diffrent color gradiant and see which colour combination is more helpful.


