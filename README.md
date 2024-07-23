# Facial Segmentation From Scratch
Facial segmentation with a U-net using a pretrained mobilenet as an encoder. The ipynb contains the code used for this experiment. 

## 1. Data Set
The data set chosen for the training is the 'human faces' from Kaggle (https://www.kaggle.com/datasets/ashwingupta3012/human-faces). For each image, we need to create a mask with the facial region. I have also included the eyes/iris positions in the masks, as shown in the figure.

<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/cc8f3997-2241-45d9-90b2-1880abcfd943" height="200" />
</p>

After the creation of the masks, I converted the images to grayscale since I am only interested in shapes, not colors. By doing this, the number of channels in each image is reduced from three to one, and the dimension is reduced from height x width x 3 to height x width. 

## 2. Training 
After processing the images and their masks, we can use them to train our network. In the definition of the mobile_Unet, we can choose a squared image shape as 2^n, where n = 5, 6, 7, 8, 9, ... Increasing the image dimension means more precision, but also more computational time to train. In this case, I choose a 256x256 dimension, therefore, all images need to be resized to that shape.

The input shape also influences the choice of layers that will be used to make the decoders of the U-net. In this case, we use the layers "input", "block_1_expand_relu", "block_3_expand_relu", "block_6_expand_relu" and "block_13_expand_relu" to build the decoder blocks of the U-net.

The sigmoid activation function was used to generate the output, since the output mask has only one class. A training image with its mask is given below.

<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/acb570fc-76d2-458e-8856-a83e2572c242" height="200" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/7b358191-280b-4fce-bbac-1d2d329af3ba" height="200" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/aa97ef68-43e8-404d-917e-397377542775" height="200" />
</p>

The training was set for 50 epochs, and took about 5 hours to conclude. 

## 3. Results
The test set results in a mean loss of 2.2071 and an accuracy of 0.7906. Since the test set has 336 images, we can interpret the result as a total of 22 pixels of the masks in the 336 tests that were predicted wrong. By inspecting the resulting masks visually, we can verify the accuracy of  the results. Some examples and their masks are given below.


<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/16871a4c-a52c-41db-83c4-ad8b69d61cc2" height="200" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/9956d725-d322-4807-8395-a509edacbf52" height="200" />
</p>

## 4. Examples of Applications
We can do many applications with a facial mask, we can retrieve the bbox of the face and eyes.

<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/0711bc14-d33c-42c9-852c-21cd08b193ce" height="250" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/f4496f06-f4e9-450f-af7d-dd8b02d01f79" height="250" />
</p>

We can also get the contours of the face, which can be used to determine the facial shape.

<p align="center">
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/a80bd2ea-344a-4f3d-b13c-a1b2f2fa917a" height="250" />
<img src="https://github.com/brunolhc/facial-segmentation-from-scratch/assets/106080016/dcb6e4f4-a19a-4782-908b-7d5f2b303f73" height="250" />
</p>
