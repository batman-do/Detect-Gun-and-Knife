# Detect Gun and Knife

- Short gun
- Long gun
- Knife


### *Using EfficientDet-D2*

#### Train
# with a coco-pretrained, you can even freeze the backbone and train heads only
# to speed up training and help convergence.

*python train.py -c 2 --batchsize 16 --lr 1e-5 --num_epochs 500 --load_weights /path/to/your/weights/efficientdet-d2.pth --head_only = True
