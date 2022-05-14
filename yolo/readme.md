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

