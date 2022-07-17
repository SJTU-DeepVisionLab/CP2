# CP2: Copy-Paste Contrastive Pretraining for Semantic Segmentation

This repo is the codebase of CP2.
* [CP2: Copy-Paste Contrastive Pretraining for Semantic Segmentation](https://arxiv.org/abs/2203.11709), in ECCV 2022.

## Installation
The implementation is built on top of [mmseg](https://github.com/open-mmlab/mmsegmentation) and [moco](https://github.com/facebookresearch/moco). Please install with the following steps:
```
git clone https://github.com/wangf3014/CP2.git
cd CP2/

# We recommend installing CP2 with torch==1.7.0 and mmcv==1.3.5
# Install mmcv (https://github.com/open-mmlab/mmcv). Make sure the mmcv version matches your torch version.
pip install mmcv-full==1.3.5 -f https://download.openmmlab.com/mmcv/dist/cu101/torch1.7.0/index.html
pip install -r requirements.txt
chmod u+x tools/dist_train.sh
```

## Pretraining
```
python main.py --data PATH_TO_YOUR_IMAGENET \
    --config config/config_pretrain.py \
    --epochs 200 --lr 0.015 -b 256
```
In CP2 we presented an efficient pretraining protocol, named Quick Tuning. For this protocol, you should first edit the config file `config/config_pretrain.py`, setting the `pretrained_path` to you pretrained backbone.

## Finetuning
We recommend finetuning on multiple GPUs.
```
# Please specify the NUM_GPU and YOUR_WORK_DIR
./tools/dist_train.sh configs/config_finetune.py NUM_GPU --work-dir YOUR_WORK_DIR
```
If using a part of GPUs on your device (e.g. 4/8), you should run finetuning with the following code:
```
CUDA_VISIBLE_DEVICES=0,1,2,3 PORT=23333 ./tools/dist_train.sh configs/config_finetune.py NUM_GPU --work-dir YOUR_WORK_DIR
```

## Citation
```
@article{wang2022cp2,
  title={CP2: Copy-Paste Contrastive Pretraining for Semantic Segmentation},
  author={Wang, Feng and Wang, Huiyu and Wei, Chen and Yuille, Alan and Shen, Wei},
  journal={arXiv preprint arXiv:2203.11709},
  year={2022}
}
```
