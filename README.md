# PG-DRFNet: Position Guided Dynamic Receptive Field Network for Finite-Pixel Object Detection in Remote Sensing Images

This repository is the official implementation of "PG-DRFNet: Position Guided Dynamic Receptive Field Network for Finite-Pixel Object Detection in Remote Sensing Images" at: [Here]()

## Introduction

This repository is the official implementation of "PG-DRFNet: Position Guided Dynamic Receptive Field Network for Finite-Pixel Object Detection in Remote Sensing Images" at: [Here]()

The master branch is built on MMRotate which works with **PyTorch 1.8+**.

PG-DRFNet's train/test configure files are placed under configs/PG-DRFNet/

## Deep Learning Experiments

### Source of Pre-trained models

* CSPNeXt-m: pre-trained checkpoint supported by Openmmlab([link](https://download.openmmlab.com/mmdetection/v3.0/rtmdet/cspnext_rsb_pretrain/cspnext-m_8xb256-rsb-a1-600e_in1k-ecb3bbd9.pth)).
* ResNet: pre-trained ResNet50 supported by Pytorch.

### Results and models

|                    Model                     | Datasets |  mAP  | Angle | lr schd | Batch Size |                           Configs                            |                           Download                           |
| :------------------------------------------: | -------- | :---: | :---: | :-----: | :--------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| [RTMDet-M](https://arxiv.org/abs/2212.07784) | DOTA2.0  | 57.71 | le90  |   6x    |     8      |                              -                               |                              -                               |
|                  PG-DRFNet                   | DOTA2.0  | 59.01 | le90  |   6x    |     8      | [pg_drfnet-6x-dota2](./configs/PG-DRFNet/pg_drfnet-6x-dota2.py) | [model](链接：https://pan.baidu.com/s/1r4XwtQtBs8DVgS3di8QSvA?pwd=yj0f <br/>提取码：yj0f) \| [log](./tools/work_dirs/PG-DRFNet/20231017_003441.log) |

For example, when dataset is DOTA2.0 and method is PG-DRFNet, you can train by running the following

```bash
python tools/train.py \
  --config configs/PG-DRFNet/pg_drfnet-6x-dota2.py \
  --work-dir work_dirs/PG-DRFNet \
  --load_from path/to/pre-trained/model \
```

and if you want submit the DOTA2.0 results for online evaluation, you can run  as follows

```bash
python tools/test.py \
  --config configs/PG-DRFNet/pg_drfnet-6x-dota2.py \
  --checkpoint path/to/gvt/model \
  --cfg-options test_dataloader.dataset.ann_file=''  test_dataloader.dataset.data_prefix.img_path=test/images/ test_evaluator.format_only=True test_evaluator.merge_patches=True test_evaluator.outfile_prefix='path/to/save_dir'
```

### Hyperparameters Configuration

Detailed hyperparameters config can be found in configs/base/

## Installation

MMRotate depends on [PyTorch](https://pytorch.org/), [MMCV](https://github.com/open-mmlab/mmcv) and [MMDetection](https://github.com/open-mmlab/mmdetection).
Below are quick steps for installation.
Please refer to [Install Guide](https://mmrotate.readthedocs.io/en/latest/install.html) for more detailed instruction.

```shell
conda create --name openmmlab python=3.8 -y
conda activate openmmlab
conda install pytorch==1.8.0 torchvision==0.9.0 cudatoolkit=10.2 -c pytorch
pip install -U openmim
mim install mmcv-full
mim install mmdet
git clone https://github.com/zcablii/Large-Selective-Kernel-Network.git
cd Large-Selective-Kernel-Network
pip install -v -e .
```

## Get Started

Please see [get_started.md](docs/en/get_started.md) for the basic usage of MMRotate.
We provide [colab tutorial](demo/MMRotate_Tutorial.ipynb), and other tutorials for:

- [learn the basics](docs/en/intro.md)
- [learn the config](docs/en/tutorials/customize_config.md)
- [customize dataset](docs/en/tutorials/customize_dataset.md)
- [customize model](docs/en/tutorials/customize_models.md)

## Acknowledgments

The code is developed based on the following repositories. We appreciate their nice implementations.

|              Method              |                      Repository                       |
| :------------------------------: | :---------------------------------------------------: |
|               ViT                | https://github.com/google-research/vision_transformer |
|              ResNet              |          https://github.com/pytorch/pytorch           |
|               CLIP               |            https://github.com/openai/CLIP             |
|             MoCo_v2              |       https://github.com/facebookresearch/moco        |
|            SimCLR_v2             |       https://github.com/google-research/simclr       |
|            SimCLR_v2             |     https://github.com/Separius/SimCLRv2-Pytorch      |
|               MAE                |        https://github.com/facebookresearch/mae        |
|              SimMIM              |          https://github.com/microsoft/SimMIM          |
| logistic regression, naive Bayes |     https://github.com/scikit-learn/scikit-learn      |

## Cite this repository

If you use this software in your work, please cite it using the following metadata. Liuqian Wang, Jing Zhang, et. al. (2023). PG-DRFNet by BJUT-AI&VBD [Computer software]. https://github.com/Qian-CV/PG-DRFNet