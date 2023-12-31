# Facial Segmentation From Scratch
Facial segmentation with a mobile_Unet neural network. The ipynb contains the code used for this experiment. 

## 1. Data Set
The data set chosen for the training is the 'human faces' from kaggle. For each image we need to create a mask with the facial region, I have also marked the iris in each mask, as shown in the figure.

<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/cc8f3997-2241-45d9-90b2-1880abcfd943" height="400" />
</p>

## 2. Training
After processing the images and their masks, we can use them to train our network. In the definition of the mobile_Unet, we can choose a squared image shape as 2^n, where n = 5, 6, 7, 8, 9, ... Inclising the image dimension means more precision and more computational time to train. For this experiment, I have defined a 256x256 input mobile_Unet, therefore, all images need to be redimensioned to that shape.

Also, since I am only interested in shapes, not in colors, all the images will be converted to gray. A training image with its mask is given below.

<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/acb570fc-76d2-458e-8856-a83e2572c242" height="400" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/aa97ef68-43e8-404d-917e-397377542775" height="200" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/7b358191-280b-4fce-bbac-1d2d329af3ba" height="400" />
</p>

The training for 50 epochs in about 5 hours. 

## 3. Results
The test set results in a loss of 2.2071 and accuracy of 0.7906. Since the test set has 336 images, we can interpret as a total of 22 pixels of the masks in 336 tests where predicted wrong. By inspecting the resulting masks, we also can see that the result is pretty good. Some examples and their masks are given below.


<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/16871a4c-a52c-41db-83c4-ad8b69d61cc2" height="250" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/9956d725-d322-4807-8395-a509edacbf52" height="250" />
</p>

## 4. Examples of Applications
We can do many applications with a facial mask, we can retrive the bbox of the face and eyes.
![bbox3](https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/0711bc14-d33c-42c9-852c-21cd08b193ce)
![bbox1](https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/f4496f06-f4e9-450f-af7d-dd8b02d01f79)


We can also get the contours of the face that can be used to determine the facial shape.
![contour3](https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/a80bd2ea-344a-4f3d-b13c-a1b2f2fa917a)
![contour1](https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/dcb6e4f4-a19a-4782-908b-7d5f2b303f73)
