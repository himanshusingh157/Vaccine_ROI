## The main function used to get the ROI from the query Image is get_vaccination_roi(), which take queryImage, templateImage, coordinates as an argument. This function calls 2 functions:
### performHomography()
performHomography() take 2 arguement queryImage, templateImage. First we use SIFT for feature detection, which returns the keypoint and descriptors for both Images. Then using the descriptor we match the key points, using the matching keypoint we find the Homography matrix. Then we transform the Query image using the obtained Homography matrix and finally return the aligned Image
### extractRoi()
extractRoi() takes 3 Arguemnets alignedImage, templateImage, coordinates. For extracting the ROI, let the area of ROI be H`x`W,  we take a small neighbourhood area around the ROI, in particular, the small area contains the pixel representing the name of Vaccine, I did this by moving my upper left corner by 120 pixels to the left, so my new ROI has area H`x`(W+120). This is like an increasing field of view. After this, I use this new ROI as a template for matching in the Aligned Image. From the Aligned Image, I took the extra area of 25 pixels on each side of the new ROI. Then I used this as a template matching problem. After which I got the matching ROI, similar to new area, I finally cropped the matching area to the original ROI and returned it.

Suppose ROI from the Template Images (of size H`x`W) is\
<img src="Images/1.jpg" width=200>\
We add neighbourhood area to this file, so the new ROI of the template Image (of size H`x`(W+120) is\
<img src="Images/2.jpg" width=200>\
Then we take the following area from Query image to find a match (of size (H+50)`x`(W+120+50))\
<img src="Images/3.jpg" width=200>
# Libraries used:
### OpenCv, Matplotlib, Numpy
