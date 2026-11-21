# stable-diffusion-gui-test

本仓库根据 CompVis 官方 Stable Diffusion v1，实现了一份文生图工具。

本仓库包含上游代码的完整副本一份，自己写的界面和推理脚本一份。

我的工作：自己写了一套图形界面。

2026-11-21 整理磁盘的时候，上传了一份release备份到仓库资源内。

仓库地址：<https://github.com/horizontalsight/stable-diffusion-gui-test>

---

## 1. 目录

.\ldm          来源于上游。包括：潜空间扩散模型本体（UNet / VAE / CLIP 编码 / DDIM·PLMS·DPM 采样器）。

.\configs    来源于上游。包括：训练与推理 yaml（v2-inference.yaml留作备用）。

.\scripts     来源于上游。包括：txt2img / img2img / inpaint 等脚本。

.\models   来源于上游。包括：模型的配置文件。

.\data         来源于上游。包括：官方示例。

.\assets      来源于上游。包括：README 用到的图片。

.\output     来源于上游。包括：我自己运行生成的文件。

.\ui              来源于上游。包括：我自己写的一些ui。

.\dist           来源于上游。包括：打包生成的一些文件（不包含一个start.exe）



根目录下文件：

LICENSE    来源于上游。

Stable_Diffusion_v1_Model_Card.md    许可条款。

README.md

environment.yaml    来源于上游。环境文件，并做了一些修改。

setup.py    来源于上游。写明依赖。

main.py    来源于上游。主程序入口。

notebook_helpers.py    来源于上游。

t2img.py    我自己写的程序，文生图脚本。

my_txt2img.py    我自己写的程序，文生图脚本。

m.py    我自己写的程序，GUI脚本。

start.py     我自己写的程序，GUI入口。

start.spec     我自己写的打包配置。

XXXX.spec     我自己写的打包配置。

icon.ico      我自己做的图标。

```
上游：
CompVis/stable-diffusion        
    https://github.com/CompVis/stable-diffusion
  ┌──────────────────────────────────────────────┐
  │ 本仓库                                        │
  │  · 复制上游文件                                │
  │  · 自写一些文件，并修改一些配置                   │
  │  · output/ 为本机生成                          │
  └──────────────────────────────────────────────┘
```

**上游作者**：Robin Rombach、Andreas Blattmann、Dominik Lorenz、Patrick Esser、Björn Ommer（LMU Munich，CompVis 组）。
**上游许可**：CreativeML Open RAIL-M，见 `LICENSE`。

---

## 2. 项目安装过程

1.CompVis/stable-diffusion ( 2022-11-16 ) 得到主要代码。

2.通过environment.yaml 里面的 pip 安装，得到openai/CLIP ( 2023-02-20 ) 和 CompVis/taming-transformers ( 2022-11-07 ) 。

3.sd-v1-1.ckpt模型，来自CompVis/stable-diffusion-v-1-1-original。

4.openai/clip-vit-large-patch14，来自HuggingFace

5.本地输出output，本地打包产物start.exe

---

## 3. 模型权重

model.ckpt（.models/ldm/stable-diffusion-v1/model.ckpt，3.97 GiB）

地址：https://huggingface.co/CompVis/stable-diffusion-v-1-1-original/resolve/main/sd-v1-1.ckpt

注意，v1-4是更为推荐的模型版本。

---

## 4. 运行环境

| 项目                    | 版本                      |
| --------------------- | ----------------------- |
| Python                | 3.8.5                   |
| PyTorch / torchvision | 1.11.0 + cu113 / 0.12.0 |
| pytorch-lightning     | 1.4.2                   |
| transformers          | 4.19.2                  |
| PySide2               | 5.15.2.1                |
| GPU                   | RTX 3080 10 GB          |

```powershell
conda env create -f environment.yaml
conda activate ldm
```

---

## 5. 自定义图形界面

**图形界面：**

```powershell
python start.py
```

**命令行**：

```powershell
python m.py "['1', '9', '30', '512', '512', '8', '1', 'a cat']"
```

**参数表格**：

| 参数         | 默认值   | 含义       |
|:---------- | ----- | -------- |
| batch_size | 1     | 批次大小     |
| scale      | 9     | CFG 引导系数 |
| ddim_steps | 30    | 采样步数     |
| H          | 512   | 图像高度     |
| W          | 512   | 图像宽度     |
| f          | 8     | 下采样因子    |
| n_iter     | 1     | 迭代次数     |
| prompt     | a cat | 提示词      |
| C          | 4     | 代码固定值    |
| n_samples  | 1     | 代码固定值    |
| ddim_eta   | 0.0   | 代码固定值    |
| 采样器        | DDIM  | 代码固定值    |

---

## 6. 项目修改记录

| 时间                      | 记录                                                   |
| ----------------------- | ---------------------------------------------------- |
| 2022-11-17              | 源项目仓库                                                |
| 2023-05-11 12:30        | 下载并解压源ZIP，运行                                         |
| 2023-05-11 13:07        | 执行pip，拉取 src、clip、transformers                       |
| 2023-05-11 14:52        | environment.yaml中修改 diffusers==0.12.1、pip install -e |
| 2023-05-23 20:47        | 写t2img.py                                            |
| 2023-06-05 20:41        | 写my_txt2img.py                                       |
| 2023-06-05              | 建立GitHub的仓库                                          |
| 2023-06-08 19:46–20:30  | 写了icon.ico、XXXX.spec、start.spec、dist/start.exe、ui    |
| 2023-06-13 12:11        | 写了start.py、m.py                                      |
| 2023-06-06 21:00        | 上传整体代码                                               |
| 2023-06-07 21:00 +08:00 | 写README                                              |

## 7. 许可与引用

代码与模型遵守 **CreativeML Open RAIL-M**，详见 `LICENSE`。使用时须遵守该许可中的使用限制，并向下游传递同样的条款。

```bibtex
@misc{rombach2021highresolution,
      title={High-Resolution Image Synthesis with Latent Diffusion Models},
      author={Robin Rombach and Andreas Blattmann and Dominik Lorenz
              and Patrick Esser and Björn Ommer},
      year={2021},
      eprint={2112.10752},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```
