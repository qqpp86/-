# -
可以对视频字幕进行识别，目前只实现了汉字OCR的部分

# 汉语识别

基于CRNN算法，pytorch框架开发的汉语识别（OCR）




## 开发环境
1. Ubuntu
2. PyTorch 1.10.2 
3. yaml
4. easydict
5. tensorboardX

### 数据

1. 数据来源：
github.com/YCG09/chinese_ocr
2. 数据简介：
共约364万张图片，按照99:1划分成训练集和验证集。
数据利用中文语料库（新闻 + 文言文），通过字体、大小、灰度、模糊、透视、拉伸等变化随机生成
包含汉字、英文字母、数字和标点共5990个字符（字符集合：https://github.com/YCG09/chinese_ocr/blob/master/train/char_std_5990.txt ）
每个样本固定10个字符，字符随机截取自语料库中的句子
图片分辨率统一为280x32

<p align='center'>
<img src='images/show.png' title='example' style='max-width:600px'></img>
</p>
 
文本
1. 文本存储在lib/dataset/txt下
2. char_std_5990.txt是汉字集合表，包含了5990个常用的汉字
3. train,test是训练集、测试集
4. eg： test.txt
```
    img_0000001.jpg 不用留地址了！"洪裳说
    img_0000002.jpg 孩林晓梅
    
```

## 训练
```angular2html
[run] python train.py --cfg lib/config/my_config.yaml

```
#### 损失值
<p align='center'>
<img src='images/train_loss.png' title='example' style='max-width:600px'></img>
</p>

##项目结构
images是图片文件夹

lib重要的库文件，包括config，core, dataset, models, utils

confit 配置文件夹：
alphabets.py 包含数据集用到的字符，以字符数组的形式存储 
my_config.yaml 是图片地址的配置信息

core文件夹：
包含了function.py 这是启动模型训练和模型评估函数

dataset文件夹：
txt文件：包含标签labels信息
init.py 初始化数据

models文件夹:
crnn.py 这是CRNN神经网络的结构文件

utils文件夹：
utils.py 里面包含了几个可选的优化器，日志信息生成函数，文字加解码函数等

output文件夹：
里面存储了模型的chekpoint，可以方便读取

test.py  测试文件
train.py 训练文件

README.md

## 结果展示
测试图片
<p align='center'>
<img src='images/test1.png' title='example' style='max-width:600px'></img>
</p>
<p align='center'>
<img src='images/test2.png' title='example' style='max-width:600px'></img>
</p>
<p align='center'>
<img src='images/test3.png' title='example' style='max-width:600px'></img>
</p>
<p align='center'>
<img src='images/test4.png' title='example' style='max-width:600px'></img>
</p>
识别结果
<p align='center'>
<img src='images/ans1.png' title='example' style='max-width:600px'></img>
</p>

<p align='center'>
<img src='images/ans2.png' title='example' style='max-width:600px'></img>
</p>

<p align='center'>
<img src='images/ans3.png' title='example' style='max-width:600px'></img>
</p>

<p align='center'>
<img src='images/ans4.png' title='example' style='max-width:600px'></img>
</p>

###可以看到得到的模型对于标准的汉字识别率很高，但是对于字幕信息的识别准确率很低，主要是因为训练的数据集和字幕之间的差距比较大。
###后续的改进：因为字幕数据集在网络上没有找到，所以可能需要自己编写一个文本图片生成器，自动合成一些数据，进行训练，最后在实现api接口，可以对视频的字幕进行处理


##参考
- https://github.com/meijieru/crnn.pytorch
- https://github.com/HRNet



