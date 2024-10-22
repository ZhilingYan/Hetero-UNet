# Hetero-UNet

Official repository for Hetero-UNet: Heterogeneous Transformer with Mamba for Medical Image Segmentation.

## Installation 

Download code:
```python
git clone https://github.com/ZhilingYan/Hetero-UNet.git
cd Hetero-UNet/umamba
pip install -e .
```

Install the environment:
```python
conda create -n HUNet python=3.10 -y
conda activate HUNet
pip install torch==2.0.1 torchvision==0.15.2
pip install causal-conv1d==1.1.1
pip install mamba-ssm
```


## Model Training
Download dataset [here](https://drive.google.com/drive/folders/18QSSiABS8H3qtx8SZA6RQb3aH1nbc3iF) and put them into the `data` folder. Hetero-UNet is built on the popular [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) and [U-Mamba](https://github.com/bowang-lab/U-Mamba) framework. If you want to train Hetero-UNet on your own dataset, please follow this [guideline](https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_format.md) to prepare the dataset. 

### Preprocessing

```python
nnUNetv2_plan_and_preprocess -d DATASET_ID --verify_dataset_integrity
```

### Train 2D models

```python
nnUNetv2_train DATASET_ID 2d all -tr nnUNetTrainerMambaUNet
```

### Train 3D models

```python
nnUNetv2_train DATASET_ID 3d_fullres all -tr nnUNetTrainerMambaUNet
```


## Inference

```python
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c CONFIGURATION -tr nnUNetTrainerMambaUNet --disable_tta
```
`CONFIGURATION` can be `2d` and `3d_fullres` for 2D and 3D models, respectively.

## Metric Calculation

```python
python evaluation/abdomen_DSC_Eval.py --gt_path GT_PATH --seg_path SEG_PATH --save_path SAVE_PATH
```

## Paper

```

```


## Acknowledgements

We acknowledge the authors of the employed public dataset. We also thank the authors of [nnUNet](https://github.com/MIC-DKFZ/nnUNet) and [U-Mamba](https://github.com/bowang-lab/U-Mamba/tree/main) for making their valuable code publicly available. 

