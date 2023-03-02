## Installation
Follow https://github.com/fundamentalvision/BEVFormer/blob/master/docs/install.md to prepare the environment.

## Preparing Dataset
1. Download the gts and annotations.json we provided. You can download our imgs.tar.gz or using the original sample files of the nuScenes dataset.

2. Download the CAN bus expansion data and maps [HERE](https://www.nuscenes.org/download).

3. Organize your floder structure as below：
```
Occupancy3D
├── projects/
├── tools/
├── ckpts/
│   ├── r101_dcn_fcos3d_pretrain.pth
├── data/
│   ├── can_bus/
│   ├── occ3d-nus/
│   │   ├── maps/
│   │   ├── samples/     # You can download our imgs.tar.gz or using the original sample files of the nuScenes dataset
│   │   ├── v1.0-trainval/
│   │   ├── gts/
│   │   │── annotations.json
```


4. Generate the info files for training and validation:
```
python tools/create_data.py occ --root-path ./data/occ3d-nus --out-dir ./data/occ3d-nus --extra-tag occ --version v1.0-trainval --canbus ./data --occ-path ./data/occ3d-nus
``` 

## Training
```
./tools/dist_train.sh projects/configs/bevformer/bevformer_base_occ.py 8
```

## Testing
```
./tools/dist_test.sh projects/configs/bevformer/bevformer_base_occ.py work_dirs/bevformer_base_occ/epoch_24.pth 8
```
You can evaluate the F-score at the same time by adding `--eval_fscore`.

