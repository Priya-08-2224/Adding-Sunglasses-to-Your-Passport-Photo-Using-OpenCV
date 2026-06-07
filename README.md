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

Feel free to fork, contribute, or customize this project for your creative needs!
## program
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceimage=cv2.imread("C:\\Users\\admin\\dipt\\rithika photo.jpeg")
plt.imshow(faceimage[:,:,::-1]);plt.title("face")
```

<img width="792" height="642" alt="image" src="https://github.com/user-attachments/assets/0ab7af48-8cf8-433e-a221-46a2606084dc" />


```
glasspng=cv2.imread("C:\\Users\\admin\\Downloads\\glass.jpeg",-1)
plt.imshow(glasspng[:,:,::-1]);plt.title("GLASSPNG")
```
<img width="1091" height="583" alt="image" src="https://github.com/user-attachments/assets/3d4cbd12-3e15-4a0c-ba48-8dde075d403e" />


```
import cv2
import matplotlib.pyplot as plt
glasspng = cv2.imread("C:\\Users\\admin\\OneDrive\\Desktop\\DIPT\\glass.jpeg")
b, g, r = cv2.split(glasspng)
glass_bgr = cv2.merge((b, g, r))
gray = cv2.cvtColor(glasspng, cv2.COLOR_BGR2GRAY)

_, glass_alpha = cv2.threshold(gray, 240, 255, cv2.THRESH_BINARY_INV)

print("BGR shape:", glass_bgr.shape)
print("Alpha shape:", glass_alpha.shape)


plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(glass_bgr, cv2.COLOR_BGR2RGB))
plt.title("Sunglass BGR")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(glass_alpha, cmap="gray")
plt.title("Generated Alpha Mask")
plt.axis("off")

plt.show()
```


<img width="972" height="313" alt="image" src="https://github.com/user-attachments/assets/00798482-0445-4b87-8db2-04954a7dae78" />



```

glass_w = int(face_w * 0.60)
glass_h = int(glass_w * glassBGR.shape[0] / glassBGR.shape[1])

glassBGR = cv2.resize(glassBGR, (glass_w, glass_h))

glass_gray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask = cv2.threshold(glass_gray, 240, 255, cv2.THRESH_BINARY_INV)

glassMask = cv2.merge([glassMask, glassMask, glassMask])
glassMask = glassMask / 255.0  # normalize

x1 = int(face_w * 0.20)
y1 = int(face_h * 0.28)

x2 = x1 + glass_w
y2 = y1 + glass_h

faceWithGlasses = faceImage.copy()
eyeROI = faceWithGlasses[y1:y2, x1:x2]

eyeROI_f    = eyeROI.astype(np.float32)
glassBGR_f  = glassBGR.astype(np.float32)
glassMask_f = glassMask.astype(np.float32)

maskedEye   = cv2.multiply(eyeROI_f, (1 - glassMask_f))
maskedGlass = cv2.multiply(glassBGR_f, glassMask_f)

eyeFinal = cv2.add(maskedEye, maskedGlass)
eyeFinal = np.clip(eyeFinal, 0, 255).astype(np.uint8)

faceWithGlasses[y1:y2, x1:x2] = eyeFinal


plt.figure(figsize=(6,8))
plt.imshow(cv2.cvtColor(faceWithGlasses, cv2.COLOR_BGR2RGB))
plt.title("Final Output – Sunglasses on Eyes ")
plt.axis("on")
plt.show()


```


<img width="752" height="667" alt="image" src="https://github.com/user-attachments/assets/79c0e37a-ccda-4b88-9d2c-e3b69f36e312" />




```

faceWithGlassesArithmetic = faceImage.copy()

face_h, face_w, _ = faceWithGlassesArithmetic.shape

glass_w = int(face_w * 0.60)
glass_h = int(glass_w * glassBGR.shape[0] / glassBGR.shape[1])
glass_resized = cv2.resize(glassBGR, (glass_w, glass_h))

glass_gray = cv2.cvtColor(glass_resized, cv2.COLOR_BGR2GRAY)
_, glassMask = cv2.threshold(glass_gray, 240, 255, cv2.THRESH_BINARY_INV)
glassMask = cv2.merge([glassMask, glassMask, glassMask]) / 255.0

x1 = int(face_w * 0.20)
y1 = int(face_h * 0.28)
x2 = x1 + glass_w
y2 = y1 + glass_h

eyeROI = faceWithGlassesArithmetic[y1:y2, x1:x2]

eyeROI_f    = eyeROI.astype(np.float32)
glass_f     = glass_resized.astype(np.float32)
glassMask_f = glassMask.astype(np.float32)

maskedEye   = cv2.multiply(eyeROI_f, 1 - glassMask_f)
maskedGlass = cv2.multiply(glass_f, glassMask_f)
eyeFinal    = cv2.add(maskedEye, maskedGlass)
eyeFinal    = np.clip(eyeFinal, 0, 255).astype(np.uint8)

faceWithGlassesArithmetic[y1:y2, x1:x2] = eyeFinal

plt.figure(figsize=[10,10])
plt.subplot(121)
plt.imshow(cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(122)
plt.imshow(cv2.cvtColor(faceWithGlassesArithmetic, cv2.COLOR_BGR2RGB))
plt.title("With Sunglasses")
plt.axis("off")
plt.show()

```
<img width="982" height="550" alt="image" src="https://github.com/user-attachments/assets/f02c0859-ea90-4d10-8495-b88a5b1b05e4" />





