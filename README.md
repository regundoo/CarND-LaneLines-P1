# **Finding Lane Lines on the Road** 

### Pipeline. 

#### General approach

The following bullet points show the programm flow in sequence
* Path to sample images are defined and stored
* All global variables (Canny parameters, Hough parameters, ...) are defined, which are given to the functions later. This allows a easier adaption to trim the parameters

---

The program works in a loop. It will read every image stored in the sample image folder and will process it until all images are processed
* Image is transformed in a grey scale image with the given function
* Gaussian blur is used to smooth the image
* Canny image is used with defined thresholds
* The size and shape of the mask is defined. A trapezoid is used for this case with boundary conditions defined in the global variables
* Image is cropped with the defined mask
* Hough lines are defined in the cropped region --> see below for description of line fitting function
* The plotted image is weighted with the given function to create the overlay of the original image

As sad, this process is repeated for every image in the loop.
For the videos, the same pipeline is used, only the for loop of the sample images is switch with the video controller.

#### draw line function

* The slope of every line is caluclated to determine if its a left or right lane
* Intersection is used define b from y = mx +b
* The length of the line is later used to calculate the average of every line, this is not really nessesary and can be done on multiple ways
* According to the calculated slope, the lanes are split in the two groups, left and right
* From all left and right lanes, one average lane is created, which is transformed back to the coordinate system

### 2. Identify potential shortcomings with your current pipeline

Shortcomings are for sure the fixed variables which are optimised for the specific problem but not sufficient for real world usage. A slight change in the environment such as lighting, or angel of the camera would destroy the code. Robustness is not given at all.

### 3. Suggest possible improvements to your pipeline

The masked I used is optimised for the specific camera angle, mounting position, focal length and only for flat roads.
A few more methods are needed to creat a bit more robust system. One option would be to create a method to track the horizon of the road. Horizontal lines can be detected and therefore the mask can be adapted in every sequence to the needed length. This does not work for curvy roads so high gradients in the hough lines should also show if a curve shows up. ... fun project, lot of things to work on 
