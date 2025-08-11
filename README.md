# BRO-S-SKIESHUB-TASK-_7
# Resize and convert images in batch.
# tools: python ,pillow
# deleverable: script that resize all image in a folder 
# hints
# use os to read image folder
# ude pil.image to resize and save

import os
from PIL import Image

# === Settings ===
input_folder = "images"          
output_folder = "resized_images" 
size = (800, 600)               
format = "JPEG"                 
ext = ".jpg"                     

# === Create output folder if not exists ===
os.makedirs(output_folder, exist_ok=True)

# === Process images ===
for filename in os.listdir(input_folder):
    if filename.lower().endswith(('.jpg', '.jpeg', '.png', '.bmp', '.gif')):
        input_path = os.path.join(input_folder, filename)
        output_name = os.path.splitext(filename)[0] + ext
        output_path = os.path.join(output_folder, output_name)

        try:
            with Image.open(input_path) as img:
                # Convert to RGB if needed
                if img.mode != "RGB":
                    img = img.convert("RGB")
                # Resize
                img = img.resize(size)
                # Save
                img.save(output_path, format)
                print(f"Saved: {output_path}")
        except Exception as e:
            print(f"Error with {filename}: {e}")
