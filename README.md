# cctv-knife-detection-dataset

This is an open-source synthetic dataset for computer vision object detection, focused on people holding knives in public and semi-public environments, viewed from CCTV and surveillance camera perspectives. It is designed to help train and evaluate YOLO, YOLOv8, YOLOWorld, Detectron, and other object detection models for threat recognition, security analytics, and abnormal behavior detection.

Key Features

Classes: person, knife Annotations: YOLO format (bounding boxes, normalized) Image Type: Synthetic, realistic, CCTV-style angles Scenes: Indoor/outdoor, airports, walkways, corridors, public spaces Purpose: Threat detection, surveillance AI, safety analytics, security CV research Size: 114 high-quality annotated images (sample version)

This is a sample dataset created by Simuletic. Larger knife detection sets (3K+ images) and custom scene generation (security, airport, military, intruder, behavior) are available at https://simuletic.com

images/ → .jpg or .png image files
labels/ → YOLO annotation .txt files (same file name as images)
annotations.csv → (optional) structured label overview

class_id center_x center_y width height 0 0.45 0.55 0.20 0.30 # person 1 0.63 0.60 0.15 0.18 # knife

path: /path/to/data train: images val: images names: 0: person 1: knife

Potential use cases:

Knife detection: Identify knives in CCTV/security environments Threat detection: Detect armed individuals in public spaces Surveillance training: Train security camera anomaly models Synthetic data research: Test synthetic-to-real domain transfer

Ethics & Considerations Fully synthetic — no real individuals or incidents depicted Created to support security, safety, and ethical AI research and implementation May not represent full real-world diversity — see our larger dataset for full diversity.

License Creative Commons Attribution 4.0 (CC BY 4.0) You may share, modify, and use commercially, as long as credit to Simuletic is given.

Citation @dataset{simuletic_knife_detection_2025, author = {Simuletic}, title = {Simuletic Synthetic Knife Detection CCTV Dataset}, year = {2025}, url = {https://simuletic.com} }

Related Links Website: https://simuletic.com Weapon Detection Dataset (previous release) https://www.kaggle.com/datasets/simuletic/cctv-weapon-dataset Github & Hugging Face links coming soon

Questions or custom dataset requests? Visit https://simuletic.com or message via Kaggle / Hugging Face.
