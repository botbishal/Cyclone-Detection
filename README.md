# 🌪️ Cyclone Detection Using YOLOv5

The YOLOv5-based cyclone detection model achieved 89.9% accuracy, effectively identifying cyclone patterns in satellite images. However, full training and deployment were limited due to resource constraints, leaving room for further optimization and real-time application.

---

## 📁 Project Structure

```
cyclone-detection-/
├── data/
│   └── cyclone_dataset/         # Dataset (images and labels)
│       ├── images/
│       │   ├── train/
│       │   └── val/
│       └── labels/
│           ├── train/
│           └── val/
├── models/                      # Trained models (best.pt)
├── runs/                        # Training runs and results
├── yolov5/                      # Cloned YOLOv5 repo
├── cyclone.yaml                 # Custom dataset config
├── detect.py                    # Inference script
├── train.py                     # Training entry point
├── requirements.txt             # Required packages
└── README.md                    # Project overview (this file)
```

## **If you run it in Google Colab Then Only this `Cyclone_Detection_using_YOLOv5` file will be needed not this structure. It is for offline run.**

## ⚙️ Setup Instructions

1. **Clone the YOLOv5 Repository:**

```bash
!git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt
```

2. **Install Required Dependencies:**

Ensure Python 3.8+ is installed. Then:

```bash
pip install -r requirements.txt
```
---

## 🗂 Dataset Format

Your dataset should follow YOLO format:

```
cyclone_dataset/
├── images/
│   ├── train/
│   └── val/
└── labels/
    ├── train/
    └── val/
```

```bash
!git clone https://github.com/academy21/TC-Satellite-DataSet.git
%cd TC-Satellite-DataSet
```

**Only For Google Colab**
Each label `.txt` file should contain:

```
<class_id> <x_center> <y_center> <width> <height>
```

All values must be normalized (between 0 and 1).

---

## 📝 Dataset Config (`cyclone.yaml`)

```yaml
train: data/cyclone_dataset/images/train
val: data/cyclone_dataset/images/val

nc: 1
names: ["cyclone"]
```

Save this as `cyclone.yaml` in the root directory or inside `yolov5/data/`.

---

## 🏋️ Training

Train YOLOv5 on your cyclone dataset:

```bash
python train.py --img 640 --batch 16 --epochs 100 --data cyclone.yaml --weights yolov5s.pt --name cyclone_yolov5
```

Options:

- `--img`: Image size (640 recommended)
- `--weights`: Pre-trained model (e.g. `yolov5s.pt`, `yolov5m.pt`, etc.)
- `--name`: Name of your training run

---

## 🔍 Inference / Detection

Detect cyclones in new images or video:

```bash
python detect.py --weights runs/train/cyclone_yolov5/weights/best.pt --img 640 --source data/sample_images/
```

- For webcam: `--source 0`
- For video: `--source path/to/video.mp4`
- Output saved in `runs/detect/`

---

## 📈 Evaluation

Run validation metrics after training:

```bash
python val.py --weights runs/train/cyclone_yolov5/weights/best.pt --data cyclone.yaml --img 640
```

Metrics include:

- mAP (mean Average Precision)
- Precision
- Recall

---

## 🧠 YOLOv5 Variants

| Model     | Size    | Speed   | Accuracy |
| --------- | ------- | ------- | -------- |
| `yolov5s` | Small   | Fastest | Lower    |
| `yolov5m` | Medium  | Good    | Balanced |
| `yolov5l` | Large   | Slower  | Better   |
| `yolov5x` | X-Large | Slowest | Best     |

---

## 📸 Example Output

Here’s an example of the cyclone detection results:

```
Image → [Detected cyclone box(es)]
```

![Sample Output](docs/sample_output.jpg)

> _(Ensure to replace the image path with your actual image if uploading to GitHub)_

---

## 📋 Requirements

Install with:

```bash
pip install -r requirements.txt
```

Dependencies:

- torch
- torchvision
- opencv-python
- matplotlib
- numpy
- PyYAML
- tqdm

---

## 🔗 Resources

- [YOLOv5 Repo](https://github.com/ultralytics/yolov5)
- [PyTorch](https://pytorch.org/)
- [NASA Cyclone Data](https://www.nasa.gov/)
- [NOAA Hurricane Archive](https://www.nhc.noaa.gov/data/)
- [TC-Satellite-DataSet](https://github.com/academy21/TC-Satellite-DataSet)

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## 📬 Contact

- **Author**: Bishal Ray
- **Email**: research.mca23b010@gmail.com
- **GitHub**: [BotBishal](https://github.com/botbishal)

---

## 📝 License

This project is licensed under the MIT License. See `LICENSE` for more details.
