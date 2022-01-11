# Face landmarks detection
Facial landmark detection is the task of detecting key landmarks on the face (jawline, eyes, eyebrows, nose and lips). This solution uses DLIB C++ Library to acquire face crops and convolutional neural network O-Net.

**O-Net**
O-Net is a convolutional neural network that was suggested in paper [Joint Face Detection and Alignment using Multi-task Cascaded Convolutional Networks](https://arxiv.org/pdf/1604.02878.pdf). Originally it has 16 output neurons: 2 for face classification, 4 for bounding box regression and 10 for landmarks regression (i.e. 5 keypoints: eyes, nose and mouth corners). I changed the number of output neurons to 136 to match [IBUG](https://ibug.doc.ic.ac.uk/resources/300-W/) format that is a 68-points mark-up.

![11212517PDTi2RyD](https://user-images.githubusercontent.com/65346868/149015994-4f887f36-4f2a-44da-aee4-310886197cb7.jpg)
> Face landmarks annotation in the IBUG 68 points format.

**Data**
Datasets used:
- [Menpo](https://ibug.doc.ic.ac.uk/resources/2nd-facial-landmark-tracking-competition-menpo-ben/)
- [300W](https://ibug.doc.ic.ac.uk/resources/300-W/)

**DLIB face detection**
I used DLIB C++ Library's face detector to create dataset of pictures of already cropped faces.

**Training**
O-Net was trained for 600 epochs with learning rates 0.01, 0.005 and 0.001 that changed every 200 epochs. Training for less number of epochs didn't get any good results with any parameters. Also some augmentations were applied to achieve better performance. I tried horizontal flip, moving bounding box predicted by DLIB, contrast and brightness changing. There's also rotate augmentation but it leaves black spaces after rotation and this problem still needs to be solved to try to make the augmentation somewhat useful (otherwise it doesn't affect network's performance in any way).

**Testing**
Metric used was AUC CED — area under graph of cumulative error distribution, error — Root Mean Square Error (RMSE) normalized by image's width and height, i.e. divided square root of their product. X-axis of the graph is error, Y-axis — percentage of images for which error is less than x-value. Max error value used is 0.08.

![Screenshot from 2022-01-11 22-57-11](https://user-images.githubusercontent.com/65346868/149019848-a1bbaf38-a798-459c-bc28-353fcfcf737c.png)
> Cumulative error distribution graph for O-Net.

I also calculated stated metric for DLIB's shape predictor (that is also designed for 68 landmarks). The results were pretty much the same, you can see them in the notebook mentioned below.

**Code**
- [O-Net training](https://www.kaggle.com/alenakokorina/face-landmarks-o-net-training/)
- [O-Net and DLIB's shape predictor comparison](https://www.kaggle.com/alenakokorina/face-landmarks-dlib-vs-o-net-testing)


