Front-Facing - Dataset for Perceptual Quality Assessment of NeRF and Neural View Synthesis Methods

# Overview
There are two seperate datasets: Lab, captured using a 2D gantry in a laboratory with controlled lighting and background; and Fieldwork, captured in-the-wild, consisting of both indoor and outdoor scenes. Both datasets were captured with Sony A7RIII.


# Fieldwork Dataset
The Lab dataset consists of 9 scenes, each of them contains sparse training views and test views that can form a smooth reference video.The dataset was captured in both outdoor city areas and indoor rooms of a public museum, with a high variability of materials and complex geometries such as a whale skeleton.  

## Structure

The dataset is structured as follows:
```
	scene/
	|	images/
	|	|	000_train.png
	|	|	001_train.png
	|	|	...
    |	|	***_sequence.png
	|	|	***_sequence.png
	|	|	...
    |	poses_bounds.npy
    |	hwf_cxcy.npy
	
```
There are N images in each scene, each is of resolution 1008×756 px. the images end with *_train.png are training images and the images end with *_sequence.png are test images. These test frames can compose a smooth video sequence. Our poses_bounds.npy stores a Nx14 numpy array. Each row in this array is split into two parts of sizes 12 and 2. The first part, when reshaped into 3x4, represents the camera extrinsic. The second part with two dimensions stores the distances from that point of view to the first and last planes (near, far). The hwf_cxcy.npy file stores a 1x6 numpy array, which represents height, width, focal length x, focal length y, principal point cx and principal point cy.


# Lab Dataset
The Lab dataset consists of 6 scenes, each scene consists of a sparse set of 30 training views taken on a uniform grid, and a reference video consisted of 300 to 500 frames, captured in a rectangular camera motion. Each frame is of resolution 4032 × 3024 px. The scenes are designed to cover a wide range of objects with various materials, including glass, metal, wood, ceramic, and plastics. The dataset contains challenging viewdependent effects, such as diffraction on the surface of a CD-ROM, specular reflections from metallic and ceramic surfaces, and transparency of the glass. 

## Structure

The dataset is structured as follows:
```
	scene/
	|	images/
	|	|	image1.png
	|	|	image2.png
	|	|	...
	|	|	sequence_000.png
	|	|	sequence_001.png
	|	|	...
    |	poses_bounds.npy
    |	mask_corner.npy
	
```
There are N images in each scene, the first 30 images are sparse training images and the other images(start with sequence_***) can compose a video sequence. Our poses_bounds.npy is similar to the LLFF[2] file format with a slight modification. This file stores a Nx19 numpy array. Each row in this array is split into three parts of sizes 15, 2 and 2. The first part, when reshaped into 3x5, represents the camera extrinsic in first four columns(camera-to-world transformation), and fifth column represents height, width and focal length. The second part stores the principal point cx and principal point cy. The third part with two dimensions stores the distances from that point of view to the first and last planes (near, far). Our mask_corner.npy stores a Nx4  numpy array. Each mask forms a rectangle and each row stores the left-up and right-bottom coordinates of the mask. During training stage, we donnot use those masks. During evaluation stage, the metrics computations is evaluated only within the mask area.

# Project web page

More details can be found at: https://perceptualnerf.netlify.app/

If you find this dataset useful, please cite [1].

# References

[1] Liang, H., Wu, T., Hanji, P., Banterle, F., Gao, H., Mantiuk, R., & Oztireli, C. (2023). “Perceptual Quality Assessment of NeRF and Neural View Synthesis Methods for Front-Facing Views." arXiv preprint arXiv:2303.15206. Available: https://perceptualnerf.netlify.app/

[2] Mildenhall, B., Srinivasan, P. P., Ortiz-Cayon, R., Kalantari, N. K., Ramamoorthi, R., Ng, R., & Kar, A. (2019). “Local light field fusion: Practical view synthesis with prescriptive sampling guidelines.” ACM Transactions on Graphics (TOG), 38(4), 1-14.