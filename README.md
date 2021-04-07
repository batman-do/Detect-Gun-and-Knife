# Detect Gun and Knife

- Short gun
- Long gun
- Knife

### Prepare dataset

- Chuyển dataset từ định sang xml sang dạng json (coco) 
- File dataset/gun/annotations chứa 2 file train and val 
- File label.txt chứa chứa 3 đối tượng : short_gun, long_gun, knife

```
  python voc_to_coco.py --ann_paths_list train.txt --label label.txt --output dataset/gun/annotations/instances_train.json --ext xml
  
  python voc_to_coco.py --ann_paths_list test.txt --label label.txt --output dataset/gun/annotations/instances_test.json --ext xml

```

### Train

```
  python train.py -c 2 -p gun_knife --batch_size 8 --lr 1e-5 --num_epochs 10 ----load_weights /path/to/your/weights/efficientdet-d2.pth --head_only True

```




