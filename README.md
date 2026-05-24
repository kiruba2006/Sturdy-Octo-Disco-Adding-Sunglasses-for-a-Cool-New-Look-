# NAME:Kiruba RC
# REG.NO: 212224230125

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

## program
```python
# ---------- SUNGLASS OVERLAY ON PASSPORT PHOTO ----------

# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

print("Libraries imported successfully!")

# Load passport image
passport_img = cv2.imread('passport_photo.jpg')

if passport_img is None:
    print("Passport image not found!")
else:
    print("Passport image loaded successfully!")
    print("Image Shape:", passport_img.shape)

# Display original passport image
plt.figure(figsize=(4,5))

plt.imshow(cv2.cvtColor(passport_img, cv2.COLOR_BGR2RGB))

plt.title("Original Passport Photo")

plt.axis("off")

plt.show()

# Load sunglass image
sunglass_img = cv2.imread('sunglass.png')

if sunglass_img is None:
    print("Sunglass image not found!")
else:
    print("Sunglass image loaded successfully!")
    print("Sunglass Shape:", sunglass_img.shape)

# Display original sunglass image
plt.figure(figsize=(5,2))

plt.imshow(cv2.cvtColor(sunglass_img, cv2.COLOR_BGR2RGB))

plt.title("Original Sunglass Image")

plt.axis("off")

plt.show()

# ---------- REMOVE BLUE BACKGROUND ----------

# Convert image to HSV
hsv = cv2.cvtColor(sunglass_img, cv2.COLOR_BGR2HSV)

# Detect cyan/blue background
lower_cyan = np.array([75, 50, 50])
upper_cyan = np.array([100, 255, 255])

mask = cv2.inRange(hsv, lower_cyan, upper_cyan)

# Invert mask
mask_inv = cv2.bitwise_not(mask)

# Create alpha channel
b, g, r = cv2.split(sunglass_img)

alpha = mask_inv

# Merge into transparent RGBA image
glass_rgba = cv2.merge([b, g, r, alpha])

print("Blue background removed successfully!")

# Display transparent sunglass
plt.figure(figsize=(5,2))

plt.imshow(cv2.cvtColor(glass_rgba, cv2.COLOR_BGRA2RGBA))

plt.title("Transparent Sunglass")

plt.axis("off")

plt.show()

# ---------- GET IMAGE SIZE ----------

img_h, img_w = passport_img.shape[:2]

print(f"Width : {img_w}")
print(f"Height: {img_h}")

# ---------- PERFECT EYE REGION ----------

eye_x = 118
eye_y = 140

eye_w = 185
eye_h = 55

print(f"Eye Region -> x:{eye_x}, y:{eye_y}, w:{eye_w}, h:{eye_h}")

# Draw eye region box
debug_img = passport_img.copy()

cv2.rectangle(
    debug_img,
    (eye_x, eye_y),
    (eye_x + eye_w, eye_y + eye_h),
    (0,255,0),
    2
)

# Display eye region
plt.figure(figsize=(4,5))

plt.imshow(cv2.cvtColor(debug_img, cv2.COLOR_BGR2RGB))

plt.title("Perfect Eye Region")

plt.axis("off")

plt.show()

# ---------- RESIZE SUNGLASSES ----------

resized_glass = cv2.resize(
    glass_rgba,
    (eye_w, eye_h),
    interpolation=cv2.INTER_AREA
)

print("Sunglass resized successfully!")

# ---------- SEPARATE RGB & ALPHA ----------

glass_rgb = resized_glass[:, :, :3]

glass_alpha = resized_glass[:, :, 3] / 255.0

# ---------- CREATE OUTPUT IMAGE ----------

output_img = passport_img.copy()

# ---------- OVERLAY SUNGLASSES ----------

for c in range(3):

    output_img[
        eye_y:eye_y + eye_h,
        eye_x:eye_x + eye_w,
        c
    ] = (

        glass_alpha * glass_rgb[:, :, c]

        +

        (1 - glass_alpha) *

        output_img[
            eye_y:eye_y + eye_h,
            eye_x:eye_x + eye_w,
            c
        ]
    )

print("Perfect sunglass overlay applied!")

# ---------- DISPLAY FINAL OUTPUT ----------

plt.figure(figsize=(4,5))

plt.imshow(cv2.cvtColor(output_img, cv2.COLOR_BGR2RGB))

plt.title("Passport Photo with Perfect Sunglasses")

plt.axis("off")

plt.show()

# ---------- COMPARISON ----------

fig, axes = plt.subplots(1, 2, figsize=(8,5))

# Original image
axes[0].imshow(cv2.cvtColor(passport_img, cv2.COLOR_BGR2RGB))
axes[0].set_title("Original Passport")
axes[0].axis("off")

# Final image
axes[1].imshow(cv2.cvtColor(output_img, cv2.COLOR_BGR2RGB))
axes[1].set_title("Sunglass Overlay Result")
axes[1].axis("off")

plt.suptitle(
    "Sunglass Overlay on Passport Photo",
    fontsize=15,
    fontweight='bold'
)

plt.tight_layout()

plt.show()
```
## output:
<img width="402" height="532" alt="image" src="https://github.com/user-attachments/assets/359ff718-0276-425c-91c9-5cc51aee5fba" />



<img width="505" height="239" alt="image" src="https://github.com/user-attachments/assets/d70d3ba7-208f-43b5-a1e3-a01bd1530f74" />



<img width="430" height="531" alt="image" src="https://github.com/user-attachments/assets/e04abf83-c71f-40e4-b993-de5a4792b292" />



<img width="424" height="527" alt="image" src="https://github.com/user-attachments/assets/ca9719d0-9653-4b02-9916-c6523893b85d" />



<img width="941" height="629" alt="image" src="https://github.com/user-attachments/assets/364a104a-fa6a-4057-b359-935f3b0d0cae" />


## Result:
Thus the program has been executed
