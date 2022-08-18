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
  - PyMuPDF (适配 new version 1.20.1)
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

(m1 mac)`brew install mupdf swig freetype`

(m1 mac)`pip install https://github.com/pymupdf/PyMuPDF/archive/master.tar.gz`

`pip install -r requirements.txt `  # 安装环境



### Step.2 使用自己的百度翻译API (更加稳定, 完全免费)

1. 在 https://api.fanyi.baidu.com 注册 **通用翻译**, 开通**基础版/高级版**
   - **基础版**优点是可以无限翻译,但是有速度限制 (每秒1次请求)
   - **高级版**优点是速度快, 但是每个月免费的额度有200w字数限制 (低需求翻译可申请这个)
   - 推荐使用基础版, 并注册多个账号, 可以达到高级版的速度同时无字数限制
2. 在**管理控制台**, **总览** 的最下面找到自己的 APP ID 和 密钥, 修改 `translate_func.py` , 151, 152 行的 appid 和secretKey. 支持添加**多个基础版账号**来获得更高的请求速度 (3-5 个足以). 
   - 若添加**高级版账号**请注释掉下面的 # contral QPS 代码块
3. 若想使用其他翻译的API, 在`trans_file.py` 中 替换 `from translate_func import baidu_translate as net_translate`  
   - 有道翻译 `from translate_func import youdao_translate as net_translate` 
   - 谷歌翻译 `from translate_func import google_translate as net_translate`



### Step.3 批量翻译

1. 将需要翻译的PDF文件放入input_file文件夹
2. 运行 `python run.py `
3. output_file 文件夹中查看结果

 

  

## Some Tips:

- 若不想让翻译文件包含图片, 在`run.py` 中将第28行改为 `save_img = Flase` (若出现翻译文件有中英文重叠可以尝试)
- 若想不导出word, 在`run.py` 中将第29行改为 `save_docx = Flase`

 

 

**有问题可以提交issue~**

# Update 日志

#### 2022.8.18
- 移除特定版本包

#### 2022.6.28

- 更新支持 `PyMuPDF==1.20.1`
- 添加 m1 mac的支持

#### 2022.4.29

- 添加txt输出, 针对某些PDF内容换段错误的文件
- 优化长段的分割算法
- 调用多账号逻辑优化
- 翻译完成的文件统一放入 output_file 文件夹
- 主程序名称改为 run.py
