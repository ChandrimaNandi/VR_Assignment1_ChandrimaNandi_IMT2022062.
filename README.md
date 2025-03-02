## Part 1

#### Problem Statement

Identify the number of coins and draw contours around them in the given image.

#### Methods Used
1. Image Preprocessing
   
    Resizing: Images are resized based on a scale factor to ensure uniform processing.
   
    Grayscale Conversion: The input images are converted to grayscale to simplify processing.
   
    Gaussian Blur: Applied to reduce noise and improve contour detection.
   
    Adaptive Thresholding: Used to create a binary image that highlights potential coin regions.

3. Edge Detection
   
    Contour Detection: Utilized cv2.findContours to identify potential coin edges.
   
    Circularity Filter: Ensured detected contours resemble circles using circularity and area thresholds.

5. Coin Segmentation
   
    Masking: Created circular masks for each detected coin.
   
    Bitwise Operations: Used to extract and save each coin as a separate image.

6. Counting Coins
   
    Counted detected contours and successfully segmented coins.

#### Folder Structure

Part1/

├── input/   		  # Folder containing input images (.jpg)

├── output/               # Folder where processed images will be saved

├── part1.ipynb                 # Main script to run the code

├── README.md             # This README file

#### System Requirements
- Python 3.x
  
- OpenCV
  
- NumPy
  
- os
  
- glob
  
Install the required libraries using:

	pip install opencv-python numpy glob os


#### How to Run
1. Place the input images (.jpg) in the input folder.
2. Run the notebook part1.ipynb to process the images.
3. The threshold image along with the segmented coins and contour image will be saved in the respective output folder.


#### Example output

Found images: ['input/coins1.jpg', 'input/coins2.jpg']

Image: coins1 - Detected Coins: 5, Segmented Coins: 5

Image: coins2 - Detected Coins: 4, Segmented Coins: 4

Threshold Image

![thresh_img](https://github.com/user-attachments/assets/bfebe13b-eb30-40dc-bbb7-32d54fb0c0cb)


Edge Detection

![DetectedEdges](https://github.com/user-attachments/assets/90d4272d-48c5-4476-a581-48acfc9c4cd8)





#### Learning Points
- I experimented with multiple methods for coin detection and segmentation, such as simple thresholding and basic edge detection, but they were ineffective under varying lighting conditions and overlapping coins.
- The use of adaptive thresholding, combined with filtering based on circularity and area, significantly improved the accuracy of detection.
- However, overlapping coins still posed challenges.
- The final approach utilized adaptive thresholding along with mask-based segmentation, which proved to be effective for most images.


## Part 2

#### Problem Statement
Create a stitched panorama from multiple overlapping images.

#### Methods Used
1. ORB keypoint detection extracts robust features from each image.
2. BFMatcher with Lowe’s ratio filters matches to ensure reliable correspondences.
3. RANSAC homography computation estimates the transformation for image alignment.
4. Warp, merge, and contour-based cropping combine images and remove unwanted borders.

#### Folder Structure

Part2/

├── input/                # Folder containing input images (.jpg)

├── output/               # Folder where processed images will be saved

├── part2.ipynb           # Main script to run the code

├── pano.jpg              # Initial panorama image (which is later split into overlapping images and placed in the input folder)

#### System Requirements
- Python 3.x
- OpenCV
- NumPy
- Matplotlib
- os
- PIL
- imutils

Install the required libraries using:

	pip install pillow opencv-python numpy matplotlib imutils


#### How to Run
1. Place the overlapping images (.jpg) in the input folder. You can replace pano.jpg with any image, which will be automatically split into 3 parts.
2. Run the notebook part2.ipynb to process the images.
3. The keypoints of the parts and the stitched panorama image will be saved in the output folder.


#### Example output
Saved annotated image: output/keypoints_part1.jpg

![keypoints_part1](https://github.com/user-attachments/assets/9dc91ba1-178f-45a8-82b3-b3c1c9d9ea33)


Saved annotated image: output/keypoints_part2.jpg

![keypoints_part2](https://github.com/user-attachments/assets/bbe6b4c4-ee5e-4f39-b73d-bb7739608d98)

Saved annotated image: output/keypoints_part3.jpg

![keypoints_part3](https://github.com/user-attachments/assets/40ffe394-4cf8-45e8-a313-6b91b954d899)

Refined panorama saved.

![stitched_pano](https://github.com/user-attachments/assets/d19048a0-14e0-4505-912e-27c5d5115883)

#### Learning Points
- Tried SIFT and ORB; settled on ORB for speed and ease.
- Used BFMatcher with kNN and Lowe's ratio test. This filtered out weak matches; however, sometimes too few matches were found when overlap was minimal.
- Warped the second image and overlaid it onto the first. Merging was successful, but simple overlay left visible seams.
- Less overlapped images were not able to stitch properly (black line occurs in between).
- Further blending techniques (e.g., feathering) may improve seam transitions if needed.
