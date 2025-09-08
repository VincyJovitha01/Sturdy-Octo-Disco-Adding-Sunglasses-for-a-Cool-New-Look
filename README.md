# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:
Developed By: VINCY JOVITHA V
Register no: 212223230242
```
# Import libraries and Load the Face Image
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('photo.JPG')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="543" height="582" alt="image" src="https://github.com/user-attachments/assets/a79d5803-6d82-46d1-837b-c8636c8e6a15" />
```
#resized_faceImage.shape
faceImage.shape
```
<img width="179" height="44" alt="image" src="https://github.com/user-attachments/assets/b959ae6f-7a3a-44c7-a36e-81ff590959dc" />
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('glasss.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="781" height="522" alt="image" src="https://github.com/user-attachments/assets/939c67b3-dc19-4a5b-b6b1-d9375b60c92d" />
```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(550,400))
print("image Dimension ={}".format(glassPNG.shape))
```
<img width="290" height="23" alt="image" src="https://github.com/user-attachments/assets/d61fcc79-7839-42e6-9c64-c68204f49dc2" />
```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```
```
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1208" height="341" alt="image" src="https://github.com/user-attachments/assets/4f068db6-62e6-4b5d-8cc1-c3b5e59cc87a" />
```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[400:800, 350:900]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI= faceWithGlassesArithmetic[400:800, 350:900]
maskedEye = cv2.multiply(eyeROI,(1-glassMask ))
maskedGlass = cv2.multiply(glassBGR,glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
<img width="1229" height="331" alt="image" src="https://github.com/user-attachments/assets/c99d17cb-5e99-4364-8b79-dfc06c61b2a5" />
```
faceWithGlassesArithmetic[400:800, 350:900]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="453" height="298" alt="image" src="https://github.com/user-attachments/assets/93ca7285-e053-4fbe-b9a6-b0fe1101d60f" />
