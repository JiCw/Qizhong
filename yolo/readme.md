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
