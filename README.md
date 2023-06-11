# Visualizing Attention Maps in IRISFormer

This project is based on the [paper](https://arxiv.org/pdf/2206.08423.pdf) titled "IRISformer: Dense Vision Transformers for Single-Image Inverse Rendering in Indoor Scenes". Main contributions of this project are 

1. Introduced code (function "visualize_attention" in file "train/train_funcs_joint_all_iiw.py") to generate attention maps for different input scenes from different self-attention layers of IRISFormer.
2. Detailed analysis of the generated attention maps

## Environment
Tested with conda environment with Python 3.10 and Torch 2.0.0.

``` bash
pip install -r requirements.txt
```

Before you run any script, change the following paths in `train/utils/config/defaults.py`:

``` yaml
PATH.root_local # to your local project root
PATH.torch_home_local # for downloading temporary models from Torch model zoo
DATASET.dataset_path_local # to the full OpenRooms dataset path
DATASET.real_images_root_path 
DATASET.iiw_path_local
```

## IIW Dataset

Download IIW dataset (Full dataset (release 0, 1.5G)) from [here](http://opensurfaces.cs.cornell.edu/publications/intrinsic/#download)

Extract the zip file and rename the folder to "iiw-dataset". Place this folder at `dataset/`.

## Pre-trained checkpoints and evaluation

Download checkpoints from [this folder](https://drive.google.com/drive/folders/18xWTUB_63GyzJ_SZrzV9cW2Dvy40rQPf?usp=share_link) and place checkpoints at `Checkpoint/`.

### Generate attention maps on IIW

Create a folder with name `Attention_Maps/`. This folder will be used to save the generated attention maps.

``` bash
CUDA_VISIBLE_DEVICES=0 python train/train_iiw.py --task_name DATE-train_mm1_albedo_eval_IIW_RESUME20230517-224958 --if_train False --if_val False --if_vis True --eval_every_iter 4000 --config-file train/configs/train_albedo.yaml --resume 20230517-224958--DATE-train_mm1_albedo
```
