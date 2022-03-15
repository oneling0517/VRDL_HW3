# VRDL_HW3 - Nuclei segmentation

## The link of my Colab

Click [My colab link](https://colab.research.google.com/drive/11Xs7121Fi7WiNWwiuSN_79oTtH0XLhAu?usp=sharing) or just run Nuclei segmentation.ipynb

## Git clone my project
```
os.chdir('/content')
!git clone https://github.com/cocodataset/cocoapi.git
os.chdir('/content/cocoapi/PythonAPI')
python3 setup.py build_ext install
!make
```
```
!git clone https://github.com/matterport/Mask_RCNN.git
os.chdir("/content/Mask_RCNN/samples")
!git clone https://github.com/oneling0517/VRDL_HW3.git
```
Move the folder named PythonAPI in order to generate the result of coco format.
```
!cp -r /content/cocoapi/PythonAPI/pycocotools /content/Mask_RCNN/samples/VRDL_HW3/
```

## Install my requirements
```
os.chdir("/content/Mask_RCNN")
pip3 install -r requirements.txt
python3 setup.py install
```
We need to change our version in order to match the version in [requirements.txt](https://github.com/matterport/Mask_RCNN/blob/master/requirements.txt).
First uninstall keras.
```
pip uninstall keras
```
Install keras 2.0.8 and tensorflow 1.15.2
```
%tensorflow_version 1.x
pip install keras==2.0.8
pip install tensorflow-gpu==1.15.2
```
I don't know why there is an error sometimes. If there is an error, you can run this again.
```
pip install keras==2.0.8
```
We also need to install the elder version of h5py
```
pip uninstall h5py
pip install h5py==2.10 -i https://pypi.tuna.tsinghua.edu.cn/simple/
```
## Dataset Download
```
os.chdir("/content/Mask_RCNN")
!gdown --id '1nEJ7NTtHcCHNQqUXaoPk55VH3Uwh4QGG' --output dataset.zip

!apt-get install unzi
!unzip -q 'dataset.zip' -d dataset
```

## Training
Use Mask R-CNN resnet101
```
os.chdir("/content/Mask_RCNN/samples/VRDL_HW3")
python3 nucleus.py train --dataset=/content/Mask_RCNN/dataset/dataset --subset=train --weights=imagenet
```

## Validation
```
os.chdir("/content/Mask_RCNN/samples/VRDL_HW3")
python3 nucleus.py detect --dataset=/content/Mask_RCNN/dataset/dataset --subset=val --weights=/content/Mask_RCNN/log/mask_rcnn_nucleus_0019.h5
```

## Testing
Use the weights from [Google Drive](https://drive.google.com/file/d/1Apj1jhAVYkVR-SDFrIpeDchNBDkPjfMd/view?usp=sharing).
```
os.chdir("/content/Mask_RCNN")
!gdown --id '1Apj1jhAVYkVR-SDFrIpeDchNBDkPjfMd' --output weights19.zip

!apt-get install unzi
!unzip -q 'weights19.zip' -d log
```
```
os.chdir("/content/Mask_RCNN/samples/VRDL_HW3")
python3 nucleus.py detect --dataset=/content/Mask_RCNN/dataset/dataset --subset=test --weights=/content/Mask_RCNN/log/mask_rcnn_nucleus_0019.h5
```

## Inference

You can click [Inference.ipynb](https://colab.research.google.com/drive/13vLcOs_x6R_ALSdEjlYYxuOcER0Xr-gd?usp=sharing).

## Reference
https://github.com/matterport/Mask_RCNN/tree/master/samples/nucleus
https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/mask.py
