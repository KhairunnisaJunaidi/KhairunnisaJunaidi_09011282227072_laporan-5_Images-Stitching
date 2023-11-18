# KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching
# Proses image_stitching tanpa MPI

## Daftar isi
- [Install packages yang akan digunakan](Install-Packages-Yang-Akan-Digunakan)
- [Eksekusi Images Stitching](Eksekusi-Images-Stitching)

# Install packages yang akan digunakan
1. membuat sebuah folder di direktori windows:
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/b153a7ff-e699-424f-b3b4-119cc98c42cc)
   
2. membuat sebuah folder di direktori ubuntu desktop:
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/0f612549-7472-44a2-a227-0d72bdd5f248)
   
3. gambar yang digunakan:
   
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/f3f074fb-d769-4c4f-ab2a-aeff9667eb23)
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/4cad5552-2684-4e93-81ee-6630ecf53e61)
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/cc45b12f-86cc-45b7-b9a0-88f328402d1a)
   
4. program python yang digunakan : <br>
```sh
# USAGE
# python image_stitching_simple.py --images images/scottsdale --output output.png

# import the necessary packages
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", type=str, required=True,
	help="path to input directory of images to stitch")
ap.add_argument("-o", "--output", type=str, required=True,
	help="path to the output image")
args = vars(ap.parse_args())

# grab the paths to the input images and initialize our images list
print("[INFO] loading images...")
imagePaths = sorted(list(paths.list_images(args["images"])))
images = []

# loop over the image paths, load each one, and add them to our
# images to stich list
for imagePath in imagePaths:
	image = cv2.imread(imagePath)
	images.append(image)


# initialize OpenCV's image stitcher object and then perform the image
# stitching
print("[INFO] stitching images...")

# Create a Stitcher with a default ORB (feature-based) detector
stitcher = cv2.Stitcher_create(cv2.Stitcher_SCANS)

# Detect keypoints and set camera parameters manually
status, stitched = stitcher.stitch(images)
if status != cv2.Stitcher_OK:
    print("[INFO] Camera parameters adjustment failed. Retrying with manual adjustment...")
    
    # Manually set camera parameters
    stitcher.setWarper(cv2.detail_WaveCorrectKind_HORIZ)
    stitcher.setWaveCorrection(True)
    stitcher.setFeaturesFinder(cv2.Stitcher_createFeaturesFinder())
    
    # Retry stitching
    status, stitched = stitcher.stitch(images)

# print additional information
print("[INFO] Stitching Status:", status)

# if the status is '0', then OpenCV successfully performed image
# stitching
if status == cv2.Stitcher_OK:
    # write the output stitched image to disk
    cv2.imwrite(args["output"], stitched)

    # display the output stitched image to our screen
    cv2.imshow("Stitched", stitched)
    cv2.waitKey(0)

# otherwise, the stitching failed
else:
    print("[INFO] image stitching failed ({})".format(status))

    # print additional information
    if status == cv2.Stitcher_ERR_NEED_MORE_IMGS:
        print("[INFO] Need more images for stitching.")
    elif status == cv2.Stitcher_ERR_HOMOGRAPHY_EST_FAIL:
        print("[INFO] Homography estimation failed.")
    elif status == cv2.Stitcher_ERR_CAMERA_PARAMS_ADJUST_FAIL:
        print("[INFO] Camera parameters adjustment failed.")
    elif status == cv2.Stitcher_ERR_MATCH_CONFIDENCE_FAIL:
        print("[INFO] Match confidence test failed.")
    elif status == cv2.Stitcher_ERR_CAMERA_PARAMS_VERIFY_FAIL:
        print("[INFO] Camera parameters verification failed.")

# ... (existing code)

5. melakukan penginstilan di ubuntu desktop dan cmd:
```
`pip install numpy`
`pip install imutlis`
`pip install opencv-python`

![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/deb44381-4682-49ae-84d0-a88eeccdf38f)
![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/1eb55b23-ed8e-41bf-aaca-db60962d27a1)

# Eksekusi Image_Stitching
1. pindah ke direktori:
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/1220bf45-29ef-4d6f-8fea-e93cf69e1af9)
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/a4533e17-6153-490a-9007-1ae2b83de7c5)
   
3. menampilkan output dengan perintah:
   ```
   python image_stitching_simple.py --images images/scottsdale --output output.png

4. Hasil Running program (output):
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/666481af-6b4c-416b-bb30-24bf35f895cb)
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/0f307375-93bb-4f22-b4f3-4f6f52a4de00)
   ![image](https://github.com/KhairunnisaJunaidi/KhairunnisaJunaidi_09011282227072_laporan-5_Images-Stitching/assets/150565586/007f6f1a-e4a1-460f-9298-0eaaaf6e3ffb)




