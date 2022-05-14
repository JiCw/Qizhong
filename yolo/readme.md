此文件夹为yolov3实验。
## 初始
### 下载编译darknet
git clone https://github.com/pjreddie/darknet
cd darknet
### 然后修改配置文件Makefile
make Makefile  
修改下面的即可  
GPU=1 #如果使用GPU设置为1，CPU设置为0  
CUDNN=1  #如果使用CUDNN设置为1，否则为0  
OPENCV=0 #如果调用摄像头，还需要设置OPENCV为1，否则为0  
OPENMP=0  #如果使用OPENMP设置为1，否则为0  
DEBUG=0  #如果使用DEBUG设置为1，否则为0  
### 下载yolov3模型
wget https://pjreddie.com/media/files/yolov3.weights
## 模型训练
模型训练前首先准备数据集，我们用VOC数据集，将VOC数据集解压，解压后共同存放在VOCevkit文件夹中，我将VOCevkit放在了darknet主文件夹/data/VOC/下。  
下载voc_label.py（wget https://pjreddie.com/media/files/voc_label.py ），在最后加上以下两行代码：  
os.system("cat 2007_train.txt 2007_val.txt 2012_train.txt 2012_val.txt > train.txt")  
os.system("cat 2007_train.txt 2007_val.txt 2007_test.txt 2012_train.txt 2012_val.txt > train.all.txt")  
然后运行。  
修改配置文件voc.data和yolov3-voc.cfg  
下载权重文件到darknet文件中：wget https://pjreddie.com/media/files/darknet53.conv.74   
开始训练：./darknet detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74   
## 计算mAP
计算map,我们需要两个python文件：
* voc_eval.py
* compute_mAP.py
其中voc_eval.py是github上开源项目的代码voc_eval.py；compute_mAP.py需要自己编写  
compute_mAP.py  
```
from voc_eval import voc_eval
import os
map_ = 0
# classnames填写训练模型时定义的类别名称
classnames = ['aeroplane','bicycle','bird','boat','bottle','bus','car','cat','chair','cow','diningtable','dog','horse','motorbike','person','pottedplant','sheep','sofa','train','tvmonitor']
for classname in classnames:
    ap = voc_eval('../results/{}.txt', '../data/VOC/VOCdevkit/VOC2007/Annotations/{}.xml', '../data/VOC/2007_test.txt', classname, '.')
    map_ += ap
    #print ('%-20s' % (classname + '_ap:')+'%s' % ap)
    print ('%s' % (classname + '_ap:')+'%s' % ap)
# 删除临时的dump文件
if(os.path.exists("annots.pkl")):
    os.remove("annots.pkl")
    print("cache file:annots.pkl has been removed!")
# 打印map
map = map_/len(classnames)
#print ('%-20s' % 'map:' + '%s' % map)
print ('map:%s' % map)

