+++
title = "Clipcap学习笔记"
author = "lyt"
date = "2023-12-26"
description = "A learning record of clipcap"
tags = [
    "深度学习",
    "clipcap学习记录",
]
+++
 
##  一、配置学习
新建虚拟环境 

必须要有python的版本，否则pip之类的都用不了
```bash
conda create -n clipcap python=3.8
```

启动环境
```bash
conda activate clipcap
```


## 二、运行github文件
参考[Github链接](https://github.com/yangjianxin1/ClipCap-Chinese/tree/master)，下载zip文件，然后上传到MobaXterm，参考[MoaXterm博文](http://t.csdnimg.cn/kkTzg)

改变路径`cd <路径>`，激活环境`conda activate clipcap`

运行第一条命令`pip install -r requirements.txt`，等待

运行`python process_flickr.py`，这时候有错误提示，显示缺少**ViT-B-32.pt**

所以，[下载ViT-B-32.pt](https://openaipublic.azureedge.net/clip/models/40d365715913c9da98579312b702a82c18be219cc2a73407c4526f58eba950af/ViT-B-32.pt)

再次运行`python process_flickr.py`，发现还少东西，dataset没有数据集flickr30k

flickr30k[下载官网](https://shannon.cs.illinois.edu/DenotationGraph/)，填好表格，会给你的邮箱发送下载链接。上传flickr30k-images.tar和flickr30k.tar.gz。

解压flickr30k文件
```bash
tar -xvf flickr30k-images.tar
```

运行`bash scripts/train_finetune_gpt2.sh`，会报错，原因在于pre_model/gpt2的文件夹里面少pytorch_model.bin文件
PS:pytorch_model.bin是PyTorch模型的二进制文件，包含了训练好的模型权重参数。少GPT2的模型权重参数，当然没法继续。下载，上传到文件夹。再次运行。此时就可以成功训练了。


## 三、clipcap代码阅读

训练训练MLP+GPT2 tuning实在是太慢了...趁这段时间分析一下代码，重点看一下train.py和predict.py

### 关于导入python的库和模块

clipcap是pytorch框架下的，然后从pytorch中导入处理数据的类：Dataset和DataLoader，以及用来可视化训练过程的Tensorboard。

关于Bert模型的配置和分词器（token）是从Huggingface的transformer库中导入的。

' tqdm '库用来显示进度条，' loguru '库中的' logger '用来日志记录，' argparse '模块用来解析命令，' os '模块用来与计算机操作系统交互，' join '函数用来连接文件路径，' functional '模块包含不可学习参数的函数，如激活函数和损失函数。


### 导入模块

`from enum import Enum`: 导入 Python 的 Enum 类，用于创建枚举类型。

`from transformers import GPT2Tokenizer, GPT2LMHeadModel, AdamW, get_linear_schedule_with_warmup, BertModel, BertConfig, GPT2Config`: 导入 Hugging Face 的 Transformers 库中的相关类和函数，包括 GPT-2 模型和 tokenizer，AdamW 优化器，学习率调度器等。

`from transformers import TextGenerationPipeline, AutoTokenizer, AutoModelWithLMHead`: 导入 Hugging Face Transformers 库中的文本生成管道、AutoTokenizer 和 AutoModelWithLMHead 类。

`from transformers import AutoConfig, AutoModelWithLMHead`: 导入 Hugging Face Transformers 库中的自动配置和自动模型。

`import pickle`: 导入 Python 的 pickle 模块，用于序列化和反序列化对象。

`import sys`: 导入 sys 模块，提供对 Python 解释器的访问。

`import argparse`: 导入 argparse 模块，用于解析命令行参数。

`from typing import Tuple, Optional, Union`: 导入 Python 的 typing 模块，用于类型提示。


## 四、可视化
执行训练MLP+GPT2 tuning指令之后，想在tensorboard上查看一下，执行指令`tensorboard --logdir ./output `

网站打不开...转战到MobaXterm直接配置，
配置成功后，打开网页：`http://127.0.0.1:16006/#timeseries`



