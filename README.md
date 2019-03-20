## detect_steel_number
DCIC 钢筋数量识别 baseline 0.98+
## my solution
### 关于检测/分割模型选择
尝试了retinanet、faster rcnn、fpn和msak rcnn，其中mask rcnn目前得分0.998，从kaggle上得知使用U-Net全卷积网络进行语义分割可能效果比较好，目前还没有尝试。
### 关于优化器选择
+ 前期选择默认SGD优化器，后来在60epoch后选择用Adam优化器。
+ I found that the model reaches a local minima faster when trained using Adam optimizer compared to default SGD optimizer。
### 关于学习率策略
每隔25epoch，学习率下降10倍比较好。
### 关于训练策略
Train in 3 stages: on 512x512 crops containing ships, then finetune on 1024x1024, and finally on 2048x2048. Inference on full-sized 2000x2666 images(由于时间关系没有尝试)
