# A lightweight YOLOv8 integrating FasterNet for real‑time underwater object detection, J Real-Time Image Proc 21, 49 (2024). https://doi.org/10.1007/s11554-024-01431-x

Code to reproduce the experiments in the paper [A lightweight YOLOv8 integrating FasterNet for real‑time underwater object detection](https://link.springer.com/article/10.1007/s11554-024-01431-x)


## Prerequisits

1. Download and prepare the datasets.  [RUOD](at https://github.com/dlut-dimt/RUOD) from their official sources.

the structure of the dataset:
   ./datasets
    ├── RUOD
    │   ├── train        
    │   │   ├── images
    │   │   └── labels
    │   ├── test        
    │   │   ├── images
    │   │   └── labels
    │   ├── val        
    │   │   ├── images
    │   │   └── labels

modify the directory in ./ultralytics/datasets/RUOD.yaml
    train: ./datasets/RUOD/train/images
    val:   ./datasets/RUOD/val/images
    test: ./datasets/RUOD/test/images


### train
python train.py --device 0 --yaml ultralytics/models/v8/yolov8s-fasternet.yaml --data RUOD.yaml --workers 8 --batch 64 --name yolov8s-fasternet --project runsD --imgsz 640 --cache --epochs 100

###test
python val.py --weight ./runs/train/RUOD/yolov8s/weights/best.pt --data RUOD.yaml --split test  --batch 1 --project runs/val/RUOD --name yolov8s-fasternet

