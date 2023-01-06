# 2023-IEEE-GRSS-DATA-FUSION-CONTEST
## Calendar
```
· 1 月 3 日：竞赛开幕：发布训练和验证数据

· 1 月 4 日：评估服务器开始接受提交验证数据集

· 2 月 28 日：将每个轨道的 1-2 页方法的简短描述发送至iadf_chairs@grss-ieee.org（使用 IGARSS 论文模板）

· 3 月 7 日：测试数据发布；评估服务器开始接受测试提交

· 3 月 13 日：测评服务器停止接受投稿

· 3 月 15 日：该方法的更新和最终描述

· 3 月 28 日：获奖者公布

· 4 月 23 日：论文内部截止日期，DFC 委员会审查程序

· 5 月 22 日：将在 IGARSS 2023 会议记录中发表的最终论文的提交截止日期
```

## Multi-Task Learning of Joint Building Extraction and Height Estimation

  This track defines the joint task of building extraction and height estimation. Both are two very fundamental and essential tasks for building reconstruction. Same as in Track 1, the input data are multi-modal optical and SAR satellite imagery. Building extraction and height estimation from single-view satellite imagery depend on semantic features extracted from the imagery. Multi-task learning provides a potentially superior solution by reusing features and forming implicit constraints between multiple tasks in comparison to conventional separate implementations. Satellite images are provided with reference data, i.e., building annotations and normalized Digital Surface Models (nDSMs). The participants are required to reconstruct building heights and extract building footprints.

## Dataset Format
download[track2.zip](https://ieee-dataport.org/competitions/2023-ieee-grss-data-fusion-contest-large-scale-fine-grained-building-classification#files) 

The topology of the dataset directory is as follows：

```
DFC_Track_2
├── annotations
│   └── buildings_only_train.json
│   └── buildings_only_val.json
│   └── buildings_only_test.json
├── train
│   └── rgb
│   │   ├── P0001.tif
│   │   └── ...
│   │   └── P0009.tif
│   └── sar
│   │   ├── P0001.tif
│   │   └── ...
│   │   └── P0009.tif
│   └── height
│       ├── P0001.tif
│       └── ...
│       └── P0009.tif
├── val
│   └── rgb
│   │   ├── P0011.tif
│   │   └── ...
│   │   └── P0019.tif
│   └── sar
│   │   ├── P0011.tif
│   │   └── ...
│   │   └── P0019.tif
│   └── height
│       ├── P0011.tif
│       └── ...
│       └── P0019.tif
└── test
    └── rgb
    │   ├── P0021.tif
    │   └── ...
    │   └── P0029.tif
    └── sar
    │   ├── P0021.tif
    │   └── ...
    │   └── P0029.tif
    └── height
        ├── P0021.tif
        └── ...
        └── P0029.tif
```
     
## Baseline
  A baseline that shows how to use the DFC23 data to train models, make submissions, etc., can be found [here](https://github.com/AICyberTeam/DFC2023-baseline).  
  We choose the classical mask rcnn algorithm as the contest baseline model. Among the input image modalities are RGB and SAR. We use [MMDetection](https://github.com/open-mmlab/mmdetection) (version 2.25.1) to test the baseline model performance.  
  The performance report of Mask R-CNN on the validation set of track 2 (building instance segmentation) is as follows:
