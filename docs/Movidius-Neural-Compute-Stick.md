```
Write @ 2018.07.14
```
   
 SW | Version / Commit ID  
:-|:-  
OS| Ubuntu 16.04  
ncsdk  | fd8fd034e52998aea529b955f50f697cf5d68630  
ncappzoo | abf59054b0695ebbd1943b15a4d1bbe25f996a0b
OpenVINO | 2.300  

[Movidius™ Neural Compute Stick - 神经元计算棒](https://developer.movidius.com/)

需要先安装官方的SDK，自己的应用需要使用官方的API来编写。 
# 1 Install the ncsdk
## 1.1 ncsdk1 & ncsdk2
目前已经发布 ncsdk2,但是使用ncsdk1 开发的应用无法使用ncsdk2。  
OpenVINO 2.300 使用的是ncsdk1。
## 1.2 Install ncsdk1
```
git clone https://github.com/movidius/ncsdk.git
cd ncsdk
make install
make examples
```

## 1.3 Install ncsdk2
如果你想使用ncsdk2 来开发自己的应用，如下安装ncsdk2
ncsdk2 在 branch ncsdk2
```
git clone -b ncsdk2 https://github.com/movidius/ncsdk.git
cd ncsdk
make install
make examples
```
**Note. ncsdk2 可能随时会设置为master 分支，所以请根据官方仓库的ReadMe来确定你需要的分支**

# 2 ncappzoo 
**ncsdk 本身包含 helloworld 类的基本examples,ncappzoo 是一些独立的 examples**

## 2.1 使用 ncsdk1 的 app
```
git clone  https://github.com/movidius/ncappzoo.git\
cd ncappzoo
make run
```
> make run 会运行所有的demo  

## 2.2 使用 ncsdk2 的 app
```
git clone -b ncsdk2 https://github.com/movidius/ncappzoo.git
cd ncappzoo
make run
```
# 3 运行 OpenVINO 的应用
需要先安装OpenVINO,建议版本2.xx以上(1.249 测试失败)

**Build all demo**  
```
cd /opt/intel/computer_vision_sdk_2018.2.300/
source bin/setupvars.sh
cd /opt/intel/computer_vision_sdk_2018.2.300/deployment_tools/inference_engine/samples/
mkdir build
cd build
cmake ..
make all
```
**使用神经棒运行车辆识别的应用**
```
cd /opt/intel/computer_vision_sdk_2018.2.300/deployment_tools/inference_engine/samples/build/intel64/Release
./security_barrier_camera_sample -d MYRIAD -d_va MYRIAD -d_lpr MYRIAD \
-i /opt/intel/computer_vision_sdk_fpga_2018.1.267/deployment_tools/demo/../demo/car_1.bmp \
-m /opt/intel/computer_vision_sdk_fpga_2018.1.267/deployment_tools/demo/../intel_models/vehicle-license-plate-detection-barrier-0007/FP16/vehicle-license-plate-detection-barrier-0007.xml \
-m_va /opt/intel/computer_vision_sdk_fpga_2018.1.267/deployment_tools/demo/../intel_models/vehicle-attributes-recognition-barrier-0010/FP16/vehicle-attributes-recognition-barrier-0010.xml \
-m_lpr /opt/intel/computer_vision_sdk_fpga_2018.1.267/deployment_tools/demo/../intel_models/license-plate-recognition-barrier-0001/FP16/license-plate-recognition-barrier-0001.xml
```
![image](https://user-images.githubusercontent.com/2216970/53687478-f73ac980-3d6f-11e9-8a16-a986619a9a3f.png)
