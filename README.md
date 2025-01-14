# Deep Reformulated Laplacian Tone Mapping

This is the implementation of [Deep Reformulated Laplacian Tone Mapping](https://arxiv.org/pdf/2102.00348.pdf). 


<img src="https://raw.githubusercontent.com/linmc-86/Deep-Reformulated-Laplacian-Tone-Mapping/master/laplacianet/dataset/result/9C4A0221-feaaa06d6f_predict.png" width="430"> <img src="https://raw.githubusercontent.com/linmc-86/Deep-Reformulated-Laplacian-Tone-Mapping/master/laplacianet/dataset/result/9C4A1511-702551eb64_predict.png" width="430">

<img src="https://raw.githubusercontent.com/linmc-86/Deep-Reformulated-Laplacian-Tone-Mapping/master/laplacianet/dataset/result/9C4A3782-70b3083cee_predict.png" width="430"> <img src="https://raw.githubusercontent.com/linmc-86/Deep-Reformulated-Laplacian-Tone-Mapping/master/laplacianet/dataset/result/9C4A4301-9fd6373e60_predict.png" width="430">



## Prerequisites for demo
* [Pycharm 2019](https://www.jetbrains.com/pycharm/download/#section=linux)
* [pretrained vgg16](https://github.com/machrisaa/tensorflow-vgg)
* [checkpoint](https://pan.baidu.com/s/1dcMH5UhOsqf0bijQBEjYrg)
* [demo tfrecord](https://pan.baidu.com/s/1WLMhB5jytr1EH_jGkCACvw)
* Tensorflow 1.9.0

### Additional prerequisites for training and testing
* [Laval Indoor dataset](http://indoor.hdrdb.com/)(EULA required)
* [Luminance HDR](https://github.com/luminancehdr/luminancehdr)

## Instructions
Download this repo.

### Network setup
1. Download [pretrained vgg16.npy](https://github.com/machrisaa/tensorflow-vgg) and place it under '/laplacianet/loss/pretrained/' folder.
2. Download the [checkpoint](https://pan.baidu.com/s/1dcMH5UhOsqf0bijQBEjYrg)(password: 9v3t if required).  Unzip it and place all 4 files under '/laplacianet/checkpoint/demo/' folder.  
3. Download the [demo tfrecord](https://pan.baidu.com/s/1WLMhB5jytr1EH_jGkCACvw)(password: mcl0 if required).  Unzip it and place it under '/laplacianet/dataset/tfrecord/' folder.  
4. (optional) Download the [HDR image in demo](https://pan.baidu.com/s/1SzecOWvAR1AjHafKrdkGJA)(password: frd0 if required).  Unzip it and place it under '/laplacianet/dataset/demo/' folder.  

`If the above links are invalid, please check this` [link](https://www.dropbox.com/sh/8ih50k9stsyqlqu/AADmsF8JX8pc1cy1gbal9iwWa?dl=0) `for checkpoint, tfrecord, and HDR images.`

### Pycharm setup
1. Download Pycharm.  Go to `File` -> `Open` and choose the project where it's downloaded.
2. Go to `File` -> `Settings`.  In the prompt window, select `Project:laplacianet` -> `Project Interpreter` on the left panel. At the top of the right panel,  click the `gear` icon to add a Python Interpreter with environment `Python 2.7`.
3. In the virtual environment under the same panel, install the following dependencies:
  - opencv-python. v 3.4.4.19
  - tensorflow-gpu. v 1.9.0
  - imageio. v 2.4.1 (need to install plugin to process hdr extension.  Use the script ```imageio_download_bin freeimage``` in Pycharm terminal)
  - easydict. v 1.9
  - scipy. v 1.1.0
  - matplotlib. v 2.2.3
  
### Demo 
In Pycharm, run `/laplacianet/operation/test.py` file.

### Train
1. Contact the author to request full access to [Laval Indoor dataset](http://indoor.hdrdb.com/)(~170GB).  
2. Follow the data preprocessing steps specified on the paper to process the data.  
3. Generate the label images. [Luminance HDR](https://github.com/luminancehdr/luminancehdr) and Photoshop are recommended. 
4. Divide the data in train set and test set.  Place the `.hdr` images of`train set` under '/laplacianet/dataset/train/hdr/' folder and the corresponding label images created from `step 3` under `/laplacianet/dataset/train/ldr/` folder.  Place the `.hdr` images of`test set` under '/laplacianet/dataset/test/hdr/' folder and the corresponding label images created from `step 3` under `/laplacianet/dataset/test/ldr/` folder.
5. To start training, in Pycharm, run `/laplacianet/operation/train_high_layer.py` to train the high frequency layer.  run `/laplacianet/operation/train_bottom_layer.py` to train the low frequency layer.  After the 2 layer's training accomplished, run `/laplacianet/operation/train_all.py` to fine tune the network.  Modify the parameters on the top of the code to specify the layer level **`n`**.  run `/laplacianet/operation/tfboard.py` file to monitor training using Tensorboard.  

### Test
1. In `/laplacianet/operation/test.py` file, modify the parameter **`mode`** to `'test'`.  Adjust the parameter level **`n`** as same as the training phase.
2. run `/laplacianet/operation/test.py`.




