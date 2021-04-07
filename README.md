# Detect Gun and Knife

- Short gun
- Long gun
- Knife


### *Using EfficientDet-D2*

## Prepare dataset


### Train
#### - With a coco-pretrained, you can even freeze the backbone and train heads only to speed up training and help convergence

*python train.py -c 2 --batchsize num_batch --lr learning_rate --num_epochs number_epochs --load_weights /path/to/your/weights/efficientdet-d2.pth --head_only = True*



