# Problem Statement
You are given two sets of images:- background and threat objects. Background images are the
background x-ray images of baggage that gets generated after passing through a X-ray machine at
airport. Threat images are the x-ray images of threats that are prohibited at airport while travelling.

### Step Taken
## Reading and Resizing Images
Background Images are read and resized to size (600,600,3) and added to Backround Image list
Similarly Threat Images are read and added (300,300,3) to Threat Image list

## Rotating and Scaling Images
Rotation of an image for an angle \theta is achieved by the transformation matrix
OpenCV provides scaled rotation with adjustable center of rotation so that you can rotate at any location you prefer
To find this transformation matrix, OpenCV provides a function, cv2.getRotationMatrix2D 
The Threat Images were Rotated by 45 degrees clockwise without any scaling. We can adjust the scale for Image while rotating. As we have already scaled down image to size of 
(300,300), there is no need for scaling.

## Removing the black border/background around rotated image in result
After Rotating the images, images generates black border after rotation 
Since the image background is white and black,we can remove it by setting all black pixels in image as white in all axis.
Otherwise we can use GrabCut Algorithm

## BitWise Operation
Highly Useful for Extraction, Defining and working with any ROI of image.

*First we'll load the two images.

*I want to put threat object somewhere in middle, So I create a ROI. And since we've already transformed the image which only have white background it'll be easier to create mask. We'll use whole image as ROI

*Now create a mask for threat image and an inverse mask also

*Now black-out the area of object in image

*Take only region of threat object from threat image

*Take object in ROI and modify the background image

## Blending Images
We want threat object translucent , means it should not look like it is cut pasted.
For this, we use cv2.addWeighted() method.
This is also addition but different weights are given to images so that it gives a feeling of blending or transparency.
Here I took two images to blend them together. First image is given a weight of 0.6 and second image is given 0.4

### Bitwise Operation and Image Blending is performed for each background seperately. For every background image , threat object is added to it using for loop.

### Each parameter in the code can be tweaked to get desired results. Such as position of object, intensity of object, size of object.

