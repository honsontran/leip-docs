---
tags:
  - design
  - BYOD
custom-width: .nan
---
> [!NOTE]  Note
> [[What is LEIP?|LEIP]] supports many additional deep learning models. The models listed below only represent models that are supported for use in [[Design|LEIP Design]] ([[Golden Recipes]] and [[Recipe Designer]]) and contain additional optimization and performance testing.
> 
> If you would like to use LEIP with additional models via [[Bring Your Own Model (BYOM)]], see [Model Preparation and Supported Formats](https://leipdocs.latentai.io/cf/3.0/content/miscellaneous/supported-models/#leip-optimizecompile)
> 
> Future releases will support a greater range of ONNX models, including transformers.

Below is a list of our currently supported models for use in [[Design|LEIP Design]], whether you're [[Bring Your Own Data (BYOD)|Bringing Your Own Data (BYOD)]] to use with a [[Golden Recipes|Golden Recipe]] or creating your own [[Glossary#Recipe|recipe]].
# Classifier Models
LEIP supports most of the [pytorchcv](https://pypi.org/project/pytorchcv/) and [timm](https://huggingface.co/docs/timm/index) models.
# Detector Models

LEIP currently supports the following detector model families:
  
  - EfficientDet
  - YOLOv5
  - YOLOv8
  - SSD
  - NanoDet
## Best Performing Detector Backbones
The performance of the supported detector model families was tested extensively and used to generate the [[Golden Recipes|Golden Recipe Database (GRDB)]]. More details (target architecture, inference speed, accuracy, etc.) about models that passed LEIP end-to-end testing can be found at the [GRDB Explorer](https://gtc.latentai.io).

The following detector backbones were in the top 0.75% of the GRDB by performance (mAP):

| Model Family | Backbone               |
| ------------ | ---------------------- |
| EfficientDet | cspdarkdet53           |
|              | cspdarkdet53m          |
|              | cspresdet50            |
|              | cspresdext50           |
|              | cspresdext50pan        |
|              | efficientdet_d0        |
|              | efficientdet_d1        |
|              | efficientdet_d5        |
|              | efficientdet_em        |
|              | efficientdet_lite0     |
|              | efficientdet_q0        |
|              | efficientdet_q1        |
|              | efficientdet_q2        |
|              | efficientdetv2_ds      |
|              | efficientdetv2_dt      |
|              | resdet50               |
|              | tf_efficientdet_d0     |
|              | tf_efficientdet_d0_ap  |
|              | tf_efficientdet_d1     |
|              | tf_efficientdet_d1_ap  |
|              | tf_efficientdet_d2     |
|              | tf_efficientdet_d2_ap  |
|              | tf_efficientdet_d3     |
|              | tf_efficientdet_d3_ap  |
|              | tf_efficientdet_d4     |
|              | tf_efficientdet_d4_ap  |
|              | tf_efficientdet_d5     |
|              | tf_efficientdet_d5_ap  |
|              | tf_efficientdet_d6     |
|              | tf_efficientdet_lite0  |
|              | tf_efficientdet_lite1  |
|              | tf_efficientdet_lite2  |
|              | tf_efficientdet_lite3  |
|              | tf_efficientdet_lite3x |
|              | tf_efficientdet_lite4  |

|  Model Family      |  Backbone               |
|--------------------|-------------------------|
| NanoDet            |  nanodet-efficient-lite0|
|                    |  nanodet-efficient-lite1|
|                    |  nanodet-efficient-lite2|
|                    |  nanodet-m              |
|                    |  nanodet-m-1.5x         |
|                    |  nanodet-plus-m         |
|                    |  nanodet-plus-m-1.5x    |

| Model Family | Backbone  |
| ------------ | --------- |
| SSD          | mb1-ssd   |
|              | vgg16-ssd |

| Model Family | Backbone |
| ------------ | -------- |
| YOLOv5       | yolov5l  |
|              | yolov5l6 |
|              | yolov5m  |
|              | yolov5m6 |
|              | yolov5n  |
|              | yolov5n6 |
|              | yolov5s  |
|              | yolov5s6 |
|              | yolov5x  |
|              | yolov5x6 |

|  Model Family      |  Backbone               |
|--------------------|-------------------------|
|  YOLOv8            |  yolov8l                |
|                    |  yolov8m                |
|                    |  yolov8n                |
|                    |  yolov8s                |
|                    |  yolov8x                |
|                    |  yolov8x6               |