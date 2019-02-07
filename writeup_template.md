
## Advanced Lane Finding Project

### The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the first code cell of the IPython notebook located in "./P2 - Advance Lane Lines.ipynb" I started by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image. Thus, objp is just a replicated array of coordinates, and objpoints will be appended with a copy of it every time I successfully detect all chessboard corners in a test image. imgpoints will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.

I then used the output objpoints and imgpoints to compute the camera calibration and distortion coefficients using the cv2.calibrateCamera() function.

As an example, I used the camera calibration and distortion coefficients to undistort the image: 
<img src="camera_cal/calibration3.jpg" width="480" alt="Combined Image" />

After undistortion, image looked like:

<img src="output_images/calibration3_undistorted.png" width="480" alt="Combined Image" />

### Pipeline (single images)

#### 1. Distortion-corrected image.
The images for camera calibration are stored in the folder called camera_cal. I compute the camera matrix and distortion co-efficients to undistort the image. After applying the distortion correction, test images looked like this one:

<img src="output_images/undistorted_img.png" width="480" alt="Combined Image" />

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.
First I created binary image by applying gradient X thresholds and Then, I created binary image after applying HLS and HSV color thresholds to detect yellow and white lane colors as shown below.

<img src="output_images/sobel_binary_image.png" width="480" alt="Combined Image" />
<img src="output_images/color_thresholds_binary_image.png" width="480" alt="Combined Image" />
Then OR'ed above binary images as shown below:
<img src="output_images/main_binary_image.png" width="480" alt="Combined Image" />

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

After applying perspective transform, here is how binary image and test image looked like:
<img src="output_images/warped_binary_image.png" width="480" alt="Combined Image" />
<img src="output_images/warped_img.png" width="480" alt="Combined Image" />

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Then I did some other stuff and fit my lane lines with a 2nd order polynomial kinda like this:

![alt text][image5]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in lines # through # in my code in `my_other_file.py`

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in lines # through # in my code in `yet_another_file.py` in the function `map_lane()`.  Here is an example of my result on a test image:

![alt text][image6]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
