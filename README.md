# Detect Gun and Knife

- Short gun
- Long gun
- Knife

### Prepare dataset

- Chuyển dataset từ định sang xml sang dạng json (coco) 
- File *dataset/gun/annotations* chứa 2 file train and val 
- File *label.txt* chứa chứa 3 đối tượng : short_gun, long_gun, knife

```
  python voc_to_coco.py --ann_paths_list train.txt --label label.txt --output dataset/gun/annotations/instances_train.json --ext xml
  
  python voc_to_coco.py --ann_paths_list test.txt --label label.txt --output dataset/gun/annotations/instances_test.json --ext xml

```
#### Data

```
 dataset
  └─gun
    ├─annotations # instances_train.json,instances_test.json
    ├─train   # train images
    └─test   # val images
  
```
### Chỉnh sửa file

- Chỉnh sửa file *efficientdet/config.py*
```
COCO_CLASSES = ["short_gun","long_gun","knife"]

```
- Chỉnh sửa file *efficient_test.py*
```
obj_list = ["short_gun","long_gun","knife"]
compound_coef = 2 # Ở bài này em sử dụng efficientdet-d2

```
- Có thể chỉnh sửa các thông số default trong file train hoặc có không cần khi mình train có thể tự chỉnh bằng câu lệnh

- Khởi tạo file *gun_knife.yml*

```
project_name: gun  # also the folder name of the dataset that under data_path folder
train_set: train
val_set: test
num_gpus: 2 (có 2 con gpu)

# mean and std in RGB order, actually this part should remain unchanged as long as your dataset is similar to coco.
mean: [0.485, 0.456, 0.406]
std: [0.229, 0.224, 0.225]

# this is coco anchors, change it if necessary
anchors_scales: '[2 ** 0, 2 ** (1.0 / 3.0), 2 ** (2.0 / 3.0)]'
anchors_ratios: '[(1.0, 1.0), (1.4, 0.7), (0.7, 1.4)]'

```
### Train

```
  python train.py -c 2 -p gun_knife --batch_size num_batch_size --lr learning_rate --num_epochs number_epochs --load_weights efficientdet-d2.pth --head_only True

```
- Có thể tự chỉnh được epochs ,.... nhưng ở đây dài quá nên chỉnh luôn trong file train để default
- Khi trên sẽ tạo ra file logs lưu loss và weights của model,có thể biểu diễn loss (sử dụng tesorboradX)

### Evaluate model

```
python coco_eval.py -p gun_knife -c 2 -w path_weights_model logs/gun/efficientdet-d2_.....pth

```

### Test

- Điều chỉnh lại trong file test để chỉ đúng folder test

```
python efficientdet_test.py

```


