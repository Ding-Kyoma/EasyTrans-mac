# EasyTrans-mac
网上很难找到没有限制的优质批量PDF翻译, 而这个项目解决了这个限制。支持PDF 批量翻译，翻译后的PDF格式基本不变。支持导出PDF, TXT和Docx。优化并精简了来自于QPromise 的 EasyTrans。使用最新的PyMuPDF库!

**翻译的质量对比看 input_file 和 output_file 文件夹中的论文**

![](https://raw.githubusercontent.com/Ding-Kyoma/CloudPic/master/gif/Kapture_2022-04-05_at_17.18.19.gif)

## 特点

- 支持批量翻译

- 优化了换行符造成的翻译质量的问题

- 优化了百度翻译API (免费版), 可以稳定进行**大量**的翻译

- 可视化翻译进度, 实时预览翻译内容

- 翻译后可导出PDF, TXT, Word

- 精简了环境安装包, 可自行尝试最新版PyMuPDF. 环境需求:
  - PyMuPDF (适配 new version 1.20.2)
  - python-docx
  - tqdm
  - PyExecJS
  - requests
  
  

环境为mac. linux同理, win可以尝试

## 使用

### Step.1 安装环境, 推荐使用conda, m1 mac需要额外运行带说明的命令

> 如何安装conda 自行google/baidu, 非必须

(可选) `conda create --name trans python=3.10 -y`   # 创建trans环境

(可选) `conda activate trans`  # 激活环境

`git clone https://github.com/Ding-Kyoma/EasyTrans-mac.git`  # 下载代码

`cd EasyTrans-mac`  # 进入文件夹

(arm mac)`brew install mupdf swig freetype`

(arm mac)`pip install https://github.com/pymupdf/PyMuPDF/archive/master.tar.gz`

`pip install -r requirements.txt `  # 安装环境



### Step.2 使用自己的百度翻译API (更加稳定, 完全免费)

1. 在 https://api.fanyi.baidu.com 注册 **通用翻译**, 开通**高级版**账号
   - **高级版**优点是速度快, 每个月免费的额度有100w字数限制
2. 在**管理控制台**, **总览** 的最下面找到自己的 APP ID 和 密钥, 修改 `account.py` 的 appid 和secretKey. 支持添加**多个账号**来获得更高的请求速度以及更多的字数. 
3. 若想使用其他翻译的API, 在`main.py` 中更改 `from translate_func import baidu_translate as net_translate`  
   - 有道翻译 `from translate_func import youdao_translate as net_translate` 
   - 谷歌翻译 `from translate_func import google_translate as net_translate`
   - gpt翻译 效果更好 `from translate_func import gpt_translate as net_translate`
     - 在secretKey里放自己的api key

### Step.3 批量翻译

1. 将需要翻译的PDF文件放入input_file文件夹
2. 运行 `python main.py `
3. output_file 文件夹中查看结果

 

  

## Some Tips:

- 若不想让翻译文件包含图片，或翻译内容和原文重叠, 在`main.py` 中将第28行改为 `save_img = False`
- 若想导出word, 在`main.py` 中将第29行改为 `save_docx = True`

 

 

**有问题可以提交issue~**

# Update 日志

#### 2023.10.21 
- update GPT API [#8](https://github.com/Ding-Kyoma/EasyTrans-mac/pull/8) 


#### 2022.11.13

- 在`account.py` 更改百度api账号
- 添加原始文件的txt输出，方便一些手动处理一些奇怪换行的pdf

#### 2022.8.18
- 移除特定版本包
- 百度API规则更新，标准版不在提供无限量翻译了，请注册高级版API
- 更新支持 `PyMuPDF==1.20.2`

#### 2022.6.28

- 更新支持 `PyMuPDF==1.20.1`
- 添加 m1 mac的支持

#### 2022.4.29

- 添加txt输出, 针对某些PDF内容换段错误的文件
- 优化长段的分割算法
- 调用多账号逻辑优化
- 翻译完成的文件统一放入 output_file 文件夹
- 主程序名称改为 main.py
