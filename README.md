# Caffe-ExcitationBP

This is a Caffe implementation of Excitation Backprop described in

> [Jianming Zhang, Zhe Lin, Jonathan Brandt, Xiaohui Shen, Stan Sclaroff. "Top-down Neural Attention by Excitation Backprop." ECCV, 2016. (oral)](http://cs-people.bu.edu/jmzhang/excitationbp.html)

__This software implementation is provided for academic research and non-commercial purposes only.  This implementation is provided without warranty.  The Excitation Backprop method described in the above paper and implemented in this software is patent-pending by Adobe.__

## Prerequisites
1. The same prerequisites as Caffe
2. Anaconda (python packages)

## Quick Start
1. Unzip the files to a local folder (denoted as **root_folder**).
2. Enter the **root_folder** and compile the code the same way as in [Caffe](http://caffe.berkeleyvision.org/installation.html).
  - Our code is tested in GPU mode, so make sure to activate the GPU code when compiling the code.
  - Make sure to compile pycaffe, the python interface
3. Enter **root_folder/ExcitationBP**, run **demo.ipynb** using the python notebook. It will automatically download the pre-trained GoogleNet model for COCO and show you how to compute the contrastive attention map. For details for running the python notebook remotely on a server, see [here](https://coderwall.com/p/ohk6cg/remote-access-to-ipython-notebooks-via-ssh).

## Anaconda Quick Start
```
$ conda env create -f env_caffe.yml
$ conda activate caffe
$ pip install scipy==1.2.3 && pip install scikit-image==0.11.3
$ conda install ipykernel
$ rm -rf build && mkdir build && cd build
$ cmake -DBLAS=open ..
$ make -j$(nproc)
```

## Other comments
1. We also implemented the gradient based method and the deconv method compared in our paper. See **demo.ipynb**.
2. We implemented both GPU and CPU version of Excitation Backprop. Change `caffe.set_mode_eb_gpu()` to `caffe.set_mode_eb_cpu()` to run the CPU version.
3. Our pre-train model is modified to be fully convolutional, so that images of any size and aspect raioe can be directly processed.
4. To apply your own CNN model, you need to modify the deploy.prototxt according to **root_folder/models/COCO/deploy.prototxt**. Basically, you need to add a dummy loss layer at the end of the file. Make sure to remove any dropout layers.
5. (__New__) We have made some modifications to make our method work on ResNet like models. When handling __EltwiseLayer__, we ignore the bottom input corresponding to the skip link. We find that this works better than splitting the signals.

## Supplementary data
1. Image lists for COCO and VOC07, including sublists for the difficult images used in the paper: [download](https://www.dropbox.com/s/xnnkyrfros2s2e4/datalist_coco%2Bvoc07.zip?dl=0)
