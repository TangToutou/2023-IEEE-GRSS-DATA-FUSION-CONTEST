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

  This track defines the joint task of building extraction and height estimation. Both are two very fundamental and essential tasks for building reconstruction. Same as in Track 1, the input data are multi-modal optical and SAR satellite imagery. Building extraction and height estimation from single-view satellite imagery depend on semantic features extracted from the imagery. Multi-task learning provides a potentially superior solution by reusing features and forming implicit constraints between multiple tasks in comparison to conventional separate implementations. Satellite images are provided with reference data, i.e., building annotations and normalized Digital Surface Models (nDSMs). The participants are required to reconstruct building heights and extract building footprints.Figure shows an example.
  
  ![figure](https://github.com/ISPNU-Signal-Group/2023-IEEE-GRSS-DATA-FUSION-CONTEST/blob/main/images/track2.png)



## Dataset Format
### Download
[track2.zip](https://ieee-dataport.org/competitions/2023-ieee-grss-data-fusion-contest-large-scale-fine-grained-building-classification#files) 

We provide individual RGB and SAR (Synthetic Aperture Radar) remote sensing images. For better use of multi-modal data, we provide a python script to generate 4-channel images concatenated in the channel dimension, in 4-channel (R,G,B,SAR) tif format. You can run the following command to generate the merge direcory:

```  
  python ./make_merge.py $DATASET_ROOT
```

  All the images are in size of 512x512. The data format follows the MS COCO format, and the annotation is in json format. The topology of the dataset directory is as follows：

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
  **A baseline that shows how to use the DFC23 data to train models, make submissions, etc., can be found [here](https://github.com/AICyberTeam/DFC2023-baseline).**  
  We choose the classical mask rcnn algorithm as the contest baseline model. Among the input image modalities are RGB and SAR. We use [MMDetection](https://github.com/open-mmlab/mmdetection) (version 2.25.1) to test the baseline model performance.  
### Baseline1
  The [performance ](https://github.com/AICyberTeam/DFC2023-baseline/tree/main/track1) report of Mask R-CNN on the validation set of track 2 (**building instance segmentation**) is as follows:
  <table>
	<head>
		<tr>
			<th >Model</th>
			<th >Modality</th>
			<th >mAP</th>
			<th >mAP_50</th>
		</tr>
	</head>
	<body>
		<tr>
			<th > Mask R-CNN</th>
			<th > RGB</th>
			<th >22.8</th>
			<th >49.1 </th>
		</tr>
	</body>
	<body>
		<tr>
			<th > Mask R-CNN</th>
			<th > RGB+SAR</th>
			<th >18.6</th>
			<th >43.6 </th>
		</tr>
	</body>
	
</table>

### 复现baseline1

  <table>
	<head>
		<tr>
			<th >Model</th>
			<th >Modality</th>
			<th >mAP</th>
			<th >mAP_50</th>
		</tr>
	</head>
	<body>
		<tr>
			<th > Mask R-CNN</th>
			<th > RGB</th>
			<th ></th>
			<th > </th>
		</tr>
	</body>
	<body>
		<tr>
			<th > Mask R-CNN</th>
			<th > RGB+SAR</th>
			<th ></th>
			<th > </th>
		</tr>
	</body>
	
</table>

### Baseline2

  The performance report of multimodal multitask learning (MML) framework on the validation set of track 2 (**instance segmentation and height prediction**) is as follows:
 <table>
	<head>
		<tr>
			<th >Model</th>
			<th >Modality</th>
			<th >mAP</th>
			<th >mAP_50</th>
			<th >Delta_1</th>
			<th >Delta_2</th>
			<th >Delta_3</th>
		</tr>
	</head>
	<body>
		<tr>
			<th >MML</th>
			<th >RGB+SAR</th>
			<th >15.1</th>
			<th > 41.1</th>
			<th > 30.1</th>
			<th > 35.3</th>
			<th > 39.6</th>
		</tr>
	</body>
</table>

### 复现baseline2

<table>
	<head>
		<tr>
			<th >Model</th>
			<th >Modality</th>
			<th >mAP</th>
			<th >mAP_50</th>
			<th >Delta_1</th>
			<th >Delta_2</th>
			<th >Delta_3</th>
		</tr>
	</head>
	<body>
		<tr>
			<th >MML</th>
			<th >RGB+SAR</th>
			<th ></th>
			<th ></th>
			<th ></th>
			<th > </th>
			<th ></th>
		</tr>
	</body>
</table>
