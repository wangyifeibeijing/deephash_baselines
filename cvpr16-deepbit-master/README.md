# CVPR16-DeepBit

Learning Compact Binary Descriptors with Unsupervised Deep Neural Networks

Created by Kevin Lin, Jiwen Lu, Chu-Song Chen, Jie Zhou

## Introduction

We propose a new unsupervised deep learning approach to learn compact binary descriptor. We enforce three criterions on binary codes which are learned at the top layer of our network: 1) minimal loss quantization, 2) evenly distributed codes and 3) rotation invariant bits. Then, we learn the parameters of the networks with a back-propagation technique. Experimental results on three different visual analysis tasks including image matching, image retrieval, and object recognition demonstrate the effectiveness of the proposed approach.

The details can be found in the following [CVPR 2016 paper](http://www.iis.sinica.edu.tw/~kevinlin311.tw/cvpr16-deepbit.pdf)


## Citation

If you find DeepBit useful in your research, please consider citing:

    Learning Compact Binary Descriptors with Unsupervised Deep Neural Networks
    Kevin Lin, Jiwen Lu, Chu-Song Chen and Jie Zhou
    IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016


## Prerequisites

  0. MATLAB (tested with 2015a on 64-bit Ubuntu)
  0. Caffe's [prerequisites](http://caffe.berkeleyvision.org/installation.html#prequequisites)


## Installation

Adjust Makefile.config and simply run the following commands:

    $ make all -j8
    $ make matcaffe

For a faster build, compile in parallel by doing `make all -j8` where 8 is the number of parallel threads for compilation (a good choice for the number of threads is the number of cores in your machine).


## Retrieval evaluation on CIFAR10

First, run the following command to download and set up `CIFAR10 Dataset`, `VGG16 pre-trained on ILSVRC12`, `DeepBit 32-bit model trained on CIFAR10`. This script will rotate training data and create leveldb files.

    $ ./prepare.sh


Launch matalb and run `run_cifar10.m` to perform the evaluation of `precision at k` and `mean average precision at k`. We set `k=1000` in the experiments. The bit length of binary codes is `32`. 
    
    >> run_cifar10


Then, you will get the `mAP` result as follows. 

    >> MAP = 0.25446596


Note: CIFAR10 dataset is split into training and test sets, with 50,000 and 10,000 images, respectively. During retrieval process, the 50,000 training images are treated as the database. We use the 10,000 test images as the query samples.


## Train DeepBit on CIFAR10

Simply run the following command to train DeepBit:

    $ cd /examples/deepbit-cifar10-32
    $ ./train.sh


The training process takes a few hours on a desktop with Titian X GPU.
You will finally get your model named `DeepBit32_final_iter_1.caffemodel` under folder `/examples/deepbit-cifar10-32/`

To use the model, modify the `model_file` in `run_cifar10.m` to link your model:

```
    model_file = './YOUR/MODEL/PATH/filename.caffemodel';
```

Launch matlab, run `run_cifar10.m` and test the model!
    
    >> run_cifar10



## Resources

**Note**: This documentation may contain links to third party websites, which are provided for your convenience only. Third party websites may be subject to the third party’s terms, conditions, and privacy statements.

If the automatic "fetch_data" fails, you may manually download the resouces from:

0. For `./prepare.sh`:
    - VGGNet pre-trained on ILSVC12: [MEGA](https://mega.nz/#!0IsmmKTS!vYrCmGODqCRoSGhbPwMkK4ohJzFNu3WblNijnsvTZD0), [Dropbox](https://www.dropbox.com/s/yqkm2tgqonditgs/VGG_ILSVRC_16_layers.caffemodel?dl=0)

    - DeepBit 32bit model pre-trained on cifar10: [MEGA](https://mega.nz/#!kFd3RZbR!jhhlgfd-eOV4YpflBcZ3lE3UmeQqJFLuds1fLdIKS_0), [Dropbox](https://www.dropbox.com/s/z815s0cjdipwr5b/DeepBit32_final_iter_1.caffemodel?dl=0)

    - CIFAR10 dataset (jpg format): [MEGA](https://mega.nz/#!RENV1bhZ!x0uFnAkqUSTJzKr6HzeeNV9mtDjlgQ0x6ZaXfpxbJkw), [Dropbox](https://www.dropbox.com/s/f7q3bbgvat2q1u2/cifar10-dataset.zip?dl=0), [BaiduYun](http://pan.baidu.com/s/1pKsSK7h)


DeepBit models in the paper:
 
0. The proposed models trained on CIFAR10:
    - 16-bit model: [MEGA](https://mega.nz/#!lRswAKTY!OsaU4vyrRR3N8xl-rJsOE-w7h5PB6K7Dv35NrHwvGLo), [Dropbox](https://www.dropbox.com/s/cwzfelw8opho1pq/DeepBit16_final_iter_1.caffemodel?dl=0)
    - 32-bit model: [MEGA](https://mega.nz/#!kFd3RZbR!jhhlgfd-eOV4YpflBcZ3lE3UmeQqJFLuds1fLdIKS_0), [Dropbox](https://www.dropbox.com/s/z815s0cjdipwr5b/DeepBit32_final_iter_1.caffemodel?dl=0)
    - 64-bit model: [MEGA](https://mega.nz/#!pMFgQaJR!-kybfCeXDLvaD96NIRTzDZBMgET6x5SVBJ5H3HKQLrw), [Dropbox](https://www.dropbox.com/s/4nrhtsq7q2offx4/DeepBit64_final_iter_1.caffemodel?dl=0)


## Experiments on Descriptor Matching and Object Recognition

comming soon...


## Contact

Please feel free to leave suggestions or comments to Kevin Lin (kevinlin311.tw@iis.sinica.edu.tw), Jiwen Lu (lujiwen@tsinghua.edu.cn) or Chu-Song Chen (song@iis.sinica.edu.tw)

