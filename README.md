# Object Detection - README

## Overall Approach
Our approach began with understanding the task of detecting pedestrians and parked/moving cars in videos using a Python program. Before coding, we conducted research to find relevant articles and resources that could simplify our implementation. Once we had compiled useful sources, we structured our process into sequential steps, refining them as we progressed. The key steps were:

1. Load the videos using OpenCV.
2. Implement a pre-trained Mask R-CNN model and configure it using the COCO dataset and weights.
3. Develop a main method to count pedestrians and cars frame-by-frame.
4. Execute the method on input dashcam videos and display the results.

Certain aspects required fine-tuning after implementation. For instance, movement thresholds for differentiating between parked and moving cars were determined through trial and error to achieve satisfactory results.

## Software & Packages Used
We primarily used OpenCV, TensorFlow, and external GitHub packages for Mask R-CNN and centroid tracking. The majority of computations occur in our main function `count_objects(...)`, which takes as input the video file path and a threshold for movement detection.

- **OpenCV**: Used to read video frames separately for analysis by the detection model.
- **Mask R-CNN Model**: Based on prior assignments, configured for inference mode to predict objects in frames. The COCO dataset provides multiple class labels, but we focused on detecting 'person' and 'car'.
- **CentroidTracker**: Tracks objects in sequential frames using Euclidean distance, updating positions while handling appearances and disappearances. This helps maintain unique object IDs and prevent misclassification.

The main method initializes object trackers for both pedestrians and cars and assigns unique IDs. Detected objects are extracted from bounding boxes, trackers are updated, and counters are incremented before updating frames.

## Summary of Program Output
The program analyzed two dashcam videos and produced the following detection results:

- **McGill Dashcam Video**:
  - 193 pedestrians detected
  - 92 moving cars detected
  - 129 parked cars detected

- **St. Catherine Dashcam Video**:
  - 351 pedestrians detected
  - 172 moving cars detected
  - 229 parked cars detected

These values are slightly overestimated compared to manually verified ground truth values, likely due to program limitations discussed below.

## Program Performance & Issues
The program executes quickly, completing object counting in 3-4 minutes using a T4 GPU in Google Colab. However, some challenges were identified:

1. **Overcounting Objects**: The program may recount the same objects across frames instead of uniquely identifying them, leading to inflated detection counts.
2. **Frame Skipping**: Although used to improve performance, skipping frames can result in missed detections and reduced accuracy.
3. **Object Association Errors**: Misidentifications in sequential frames could cause inconsistencies in tracking moving cars, affecting detection reliability.

Future improvements could include refining tracking logic to ensure unique object identification across frames, optimizing movement thresholding, and experimenting with alternative frame-skipping strategies to balance performance and accuracy.
