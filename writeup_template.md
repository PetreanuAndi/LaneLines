#**Finding Lane Lines on the Road** 

(1)Set goal for this project is to correctly identify and capture the corresponding lane lines of a vehicle,within a daylight / highway / forward motion scenario


[//]: # (Image References)

[image1]: ./capture.png "Challenge Capture"

---

### Reflection

I innitially split the main functionality between "houghInference(image)" and "colorInference(image)" methods.
Within "houghInference(image)" :
* grayscale the image
* apply histogram equalisation and thresholding on 1 channel, within "colorIngerence(image)"
* apply canny edge detection
* create ROI for hough transform
* Hough transform with "threshold" and "min_line_length" parameters experimentally set to minimum values, in order to preserve small curve-lines.

Within the preprovisioned "hough_lines(masked_edges, rho, theta, threshold, min_line_length, max_line_gap)":
* have modified the recommended "draw_lines(line_img, lines)" method, such that spatial-temporal averaging and line extrapolation was included.
* keep a global history of the previous line detected, in order to continuously display a line even when data-filtration of input was too powerfull.(nothing is detected by cv2.HoughLinesP)
* make use of cv2.fitLine(..) method in order to fit the best possible line out of all my candidates (per frame per slope direction, Left or Right)
* also keep a global history of "the best" lines detected (lines that resemble the expected slope of a lane-line + lines that are close to my current average)
* calculate the intersection of my best fitted lines, at each frame, in order to dinamically compute their upper Y bounds.
* compute the "safe-zone" polygon and visualice nicely :D

![alt text][image1]


### Potential Shortcomings:
Will probably not generalise to an evnironment different than the one in hipothesis(1)
Given the pretty hard filtration parameters used, there might be scenarios where displaying the same "previousLine" will cause big errors.


## Suggest possible improvements to your pipeline

IR camera
ML
