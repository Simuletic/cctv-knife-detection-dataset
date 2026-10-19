# CCTV Knife Detection Dataset: free sample (synthetic CCTV, YOLO + COCO)

**Synthetic CCTV images of people holding knives, with YOLO and COCO boxes: 60 free images here, 1,000 in the full dataset.**

![Six synthetic CCTV images with YOLO boxes: a man holding a knife in an office lobby, a woman holding a knife on a hotel terrace, a man in a red jacket holding a knife in an office corridor, a woman with a knife in a shop aisle in monochrome night mode, a woman with a knife in a bike shelter, and a woman with a knife on a park path](assets/hero_grid.jpg)

**Hard negatives**: people holding bottles, a flashlight or a phone, and no knife; only `person` is labelled.

![Four hard-negative synthetic CCTV images, cropped around the person, with only person boxes: a man holding a water bottle at a shop entrance, a man carrying a bottle in monochrome night footage, a man with a flashlight in a warehouse, and a woman looking at her phone in a car park at dusk](assets/hard_negatives.jpg)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Simuletic/cctv-knife-detection-dataset/blob/main/notebooks/quickstart.ipynb) [![Licence: CC BY-NC 4.0](https://img.shields.io/badge/licence-CC%20BY--NC%204.0-lightgrey.svg)](LICENSE) [![Full dataset: 1,000 images](https://img.shields.io/badge/full%20dataset-1%2C000%20images-0a7cff.svg)](https://simuletic.com/datasets/cctv-knife-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset)

This free sample has 60 synthetic CCTV images for **knife detection, weapon detection, edged weapon detection**, with bounding boxes in **YOLO and COCO** format. The images show people holding knives, seen from ceiling- and pole-mounted CCTV cameras in shops, lobbies, offices, car parks, kitchens and outdoor areas, by day and at night. 15 of them are hard negatives: people holding phones, wallets, bottles, umbrellas or shopping bags, or nothing at all. Made by [Simuletic](https://simuletic.com/?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset), which builds synthetic CCTV datasets for computer vision.

The sample has the same classes, label rules and folder layout as the full [CCTV Knife Detection Dataset (1,000 images)](https://simuletic.com/datasets/cctv-knife-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset), so code you write for the sample runs unchanged on the full set.

## At a glance

| | Free sample (this repo) | [Full dataset](https://simuletic.com/datasets/cctv-knife-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset) |
|---|---|---|
| Images | 60 (48 train / 12 val) | 1,000 (900 train / 100 val) |
| Hard negatives | 15 | 232 |
| Classes | 2: `person`, `knife` | same |
| Labels | YOLO `.txt` + COCO `.json` | same |
| Resolution | mostly 1536×1024 and 1672×941 JPEG | same |
| Licence | CC BY-NC 4.0 (non-commercial) | research ($149) or commercial ($590), one-time |

## Classes and box counts

| Class | YOLO id | Boxes in sample | Boxes in full 1K |
|---|---|---|---|
| `person` | 0 | 77 | 1,418 |
| `knife` | 1 | 45 | 769 |

**Labelling rules.** Every person in the frame is boxed as `person`, including small, distant and partly hidden people. Each knife gets one tight box around the visible blade and handle. The person holding it also gets a `person` box. Hard-negative images contain only `person` boxes. Boxes are axis-aligned; YOLO coordinates are normalised (0–1), COCO boxes are `[x, y, width, height]` in pixels.

## Folder layout

```
cctv-knife-detection-dataset/
  data.yaml                        # Ultralytics config: class names and splits
  images/train/  images/val/       # JPEG, metadata stripped
  labels/train/  labels/val/       # YOLO: class x_center y_center width height (0-1), one .txt per image
  annotations/instances_train.json # COCO
  annotations/instances_val.json
  assets/                         # README images
  notebooks/quickstart.ipynb       # Colab: view labels, fine-tune YOLO, run inference
  quickstart.py                    # same steps as a script
```

## Quick start

**In the browser:** open the [Colab notebook](https://colab.research.google.com/github/Simuletic/cctv-knife-detection-dataset/blob/main/notebooks/quickstart.ipynb). It loads the sample, draws the labels, fine-tunes YOLO11 for a few epochs on a free GPU and runs inference.

**On your machine:**

```bash
git clone https://github.com/Simuletic/cctv-knife-detection-dataset
cd cctv-knife-detection-dataset
pip install ultralytics
python quickstart.py --epochs 30
```

`quickstart.py` counts the boxes, saves label previews to `runs/label_previews/`, trains, validates and saves predictions to `runs/predict/`. Point it at the full dataset with `--data /path/to/CCTV_Knife_Detection_1K/data.yaml`.

**In Python:**

```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")
model.train(data="data.yaml", epochs=30, imgsz=640)
model.predict("images/val", save=True)
```

Sixty images will not give you a deployable detector. The sample is for checking the format, the camera angles and the label quality against your own footage before you buy or train on the full set.

## Use cases

- knife and edged-weapon detection on CCTV and VMS cameras
- small-object detection from high camera angles
- testing false alarms on phones and other hand-held objects
- pre-training before fine-tuning on your own footage

## How the images were made

The images are fully synthetic: there are no real people and no real incident footage in them. Each image was generated to a scene and camera specification (environment, camera height and angle, lighting, distance), labelled automatically, and checked before release: a vision-language model verified that the object is present, that the frame reads as CCTV and that each box sits on the right object, and the set was reviewed by eye. Images that failed were removed.

**Limitations.** Synthetic images do not cover every camera, lens, compression artefact or scene you will meet in deployment. Validate on your own footage, and for production combine synthetic and real data. Some targets are small at CCTV distance; that is deliberate, but it makes the task harder than close-up datasets.

## Get the full dataset

The full **[CCTV Knife Detection Dataset](https://simuletic.com/datasets/cctv-knife-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset)** has 1,000 images (232 hard negatives) with the same labels and layout, as a single download. One-time licence: **research $149** (non-commercial, one lab or course) or **commercial $590** (one organisation; models you train are yours). Need other scenes, cameras or classes? See [custom data](https://simuletic.com/custom-data?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset).

Read more: [knife detection dataset guide on the Simuletic blog](https://simuletic.com/blog/knife-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset).

## More synthetic CCTV datasets from Simuletic

- [CCTV Weapon Detection Dataset](https://github.com/Simuletic/cctv-weapon-dataset): free sample on GitHub · [full 1K](https://simuletic.com/datasets/cctv-weapon-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset)
- [CCTV Fall Detection Dataset](https://github.com/Simuletic/cctv-fall-detection-dataset): free sample on GitHub · [full 1K](https://simuletic.com/datasets/cctv-fall-incident-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset)
- [All datasets](https://simuletic.com/datasets?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset) · [Free samples on Hugging Face](https://huggingface.co/Simuletic) · [All GitHub repos](https://github.com/Simuletic)

## Licence

The images and labels in this sample are licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/): you may share and adapt them for non-commercial purposes with credit to Simuletic. The code (`quickstart.py`, `notebooks/`) is MIT-licensed. For commercial use, buy the [commercial licence](https://simuletic.com/datasets/cctv-knife-detection-dataset?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset). The full dataset is licensed separately.

## Citation

```bibtex
@misc{simuletic_knife_2026,
  author       = {{Simuletic}},
  title        = {CCTV Knife Detection Dataset: synthetic CCTV images with YOLO and COCO labels},
  year         = {2026},
  publisher    = {Simuletic},
  howpublished = {\url{https://simuletic.com/datasets/cctv-knife-detection-dataset}},
  note         = {Free sample: \url{https://github.com/Simuletic/cctv-knife-detection-dataset}}
}
```

## Contact

Questions, bugs in the labels or custom requests: contact@simuletic.com · [simuletic.com](https://simuletic.com/contact?utm_source=github&utm_medium=readme&utm_campaign=cctv-knife-detection-dataset) · [open an issue](https://github.com/Simuletic/cctv-knife-detection-dataset/issues)
