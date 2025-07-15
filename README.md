# TASK-2-
pixel manipulation for image encyption 

!pip install opencv-python

import cv2
import numpy as np
from google.colab.patches import cv2_imshow
from google.colab import files

def simple_encrypt(image_path, output_path):
    """Encrypts an image using a simple pixel manipulation."""
    img = cv2.imread(image_path)
    if img is None:
        print("Error: Could not load image.")
        return

    # Simple encryption: swap Red and Blue channels
    # OpenCV reads images in BGR format
    encrypted_img = img[:, :, [2, 1, 0]] # Swap B and R

    cv2.imwrite(output_path, encrypted_img)
    print(f"Image encrypted and saved to {output_path}")
    cv2_imshow(encrypted_img)


def simple_decrypt(encrypted_image_path, output_path):
    """Decrypts an image encrypted with simple_encrypt."""
    img = cv2.imread(encrypted_image_path)
    if img is None:
        print("Error: Could not load encrypted image.")
        return

    # Simple decryption: swap Red and Blue channels back
    decrypted_img = img[:, :, [2, 1, 0]] # Swap R and B back

    cv2.imwrite(output_path, decrypted_img)
    print(f"Image decrypted and saved to {output_path}")
    cv2_imshow(decrypted_img)

# Example usage:
# Upload an image first
uploaded = files.upload()

# Assuming you uploaded an image named 'my_image.png'
image_file = next(iter(uploaded))

print(f"Original Image: {image_file}")
img_original = cv2.imread(image_file)
if img_original is not None:
    cv2_imshow(img_original)
else:
    print("Could not display original image.")

# Encrypt the image
encrypted_output_file = 'encrypted_image.png'
simple_encrypt(image_file, encrypted_output_file)

# Decrypt the image
decrypted_output_file = 'decrypted_image.png'
simple_decrypt(encrypted_output_file, decrypted_output_file)
