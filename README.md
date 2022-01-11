# Face landmarks detection
Facial landmark detection is the task of detecting key landmarks on the face (jawline, eyes, eyebrows, nose and lips). This solution uses DLIB C++ Library to acquire face crops and convolutional neural network O-Net.

**O-Net**
O-Net is a convolutional neural network that was suggested in paper [Joint Face Detection and Alignment using Multi-task Cascaded Convolutional Networks](https://arxiv.org/pdf/1604.02878.pdf). Originally it has 16 output neurons: 2 for face classification, 4 for bounding box regression and 10 for landmarks regression (i.e. 5 keypoints: eyes, nose and mouth corners). I changed the number of output neurons to 136 to match [IBUG](https://ibug.doc.ic.ac.uk/resources/300-W/) format that is a 68-points mark-up.


![figure_1_68](https://user-images.githubusercontent.com/65346868/149015831-f3cd3a09-26fb-4727-99cb-1b5391e9bcd1.jpg)

