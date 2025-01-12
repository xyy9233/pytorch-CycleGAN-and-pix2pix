# 基于生成对抗网络的图像生成

•  至少实现一种生成对抗网络（WGAN, Style GAN, CycleGAN等），完成图像生成 

•  对生成对抗网络模型进行参数调优、分析影响图像生成质量的关键因素， 给出合理、可靠结论

 •  尝试对现有生成对抗网络模型进行改进

 Tero Karras, Samuli Laine, Timo Aila. A Style-Based Generator Architecture for Generative Adversarial Networks. CVPR 2019.  (引用12846次) https://github.com/NVlabs/stylegan

## 数据集与模型下载

代码已同步至github：

并基于[官方开源的CycleGAN](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix)改进。

实验中用到的数据集下载：

https://people.eecs.berkeley.edu/~taesung_park/CycleGAN/datasets/

已经训练好的模型示例下载：

链接：

## 运行环境

这里使用autodl：

![image-20250112011620716](https://xyy9233.oss-cn-beijing.aliyuncs.com/hexoblog/image-20250112011620716.png)



## 运行方式

- 数据集下载好后解压置于datasets文件夹下。在datasets文件夹里提供了**monet2photo**, **vangogh2photo**, **facades** and **horse2zebra** 四个数据集

- 训练模型：

  ```shell
  python train.py --dataroot ./datasets/horse2zebra --name 			horse2zebra_cyclegan --model cycle_gan
  ```

  `--dataroot` ：使用的训练数据集的路径。

  `--name` ：训练过程中的结果被保存的路径。

  由于CycleGAN模型训练较为耗时，建议使用有高算力GPU的设备或服务器。没有GPU需要使用 `--gpu_id -1` 以在CPU上进行训练。

- 测试模型

  ```shell
  python test.py --dataroot ./datasets/horse2zebra/testB --name horse2zebra_cyclegan_with_CBAM_B --model test --no_dropout
  ```

  `--name`代表想要进行测试的模型的名称（分别与数据集相对应，存放在./checkpoints 文件夹下，可以通过 link 下载。

  `testA / testB` 代表想要测试的图片生成方向。

  没有GPU需要使用 `--gpu_id -1` 以在CPU上进行测试。

  所有训练过的模型都存放在checkpoints文件夹下，以 {dataset name}\_cyclegan(\_with\_CBAM)\_{A or B} 的方式进行命名，如``horse2zebra_cyclegan_with_CBAM_B`` 、`facades_cyclegan_A`等。

- ``with_CBAM``代表模型中使用了CBAM改进

- `A or B` 代表加载不同方向的生成器，A代表生成 A to B 的图像，B代表生成 B to A 的图像

## 实验结果

成对带标注语义分割数据集的效果

![14001642658835_.pic_hd](https://xyy9233.oss-cn-beijing.aliyuncs.com/hexoblog/14001642658835_.pic_hd.jpg)

不成对无标注训练的结果

![13991642658834_.pic_hd](https://xyy9233.oss-cn-beijing.aliyuncs.com/hexoblog/13991642658834_.pic_hd.jpg)

图像转换

![14011642658836_.pic_hd](https://xyy9233.oss-cn-beijing.aliyuncs.com/hexoblog/14011642658836_.pic_hd.jpg)

油画风格迁移

![13971642658832_.pic_hd](https://xyy9233.oss-cn-beijing.aliyuncs.com/hexoblog/13971642658832_.pic_hd.jpg)

![13981642658833_.pic_hd](https://xyy9233.oss-cn-beijing.aliyuncs.com/hexoblog/13981642658833_.pic_hd.jpg)

