<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://docs.ell.so/_static/ell-wide-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="https://docs.ell.so/_static/ell-wide-light.png">
  <img alt="ell logo that inverts based on color scheme" src="https://docs.ell.so/_static/ell-wide.png">
</picture>

--------------------------------------------------------------------------------

[![文档状态](https://img.shields.io/badge/documentation-go)](https://docs.ell.so/) [![安装指南](https://img.shields.io/badge/get_started-blue)](https://docs.ell.so/installation) [![Discord](https://dcbadge.limes.pink/api/server/vWntgU52Xb?style=flat)](https://discord.gg/vWntgU52Xb) [![X (formerly Twitter) Follow](https://img.shields.io/twitter/follow/wgussml)](https://x.com/wgussml)


```bash

pip install -U ell-ai
```

`ell` 是一个轻量级的、功能性的提示工程框架，基于几个核心原则构建：

### 1. 提示是程序，而不是字符串。

提示不仅仅是字符串；它们是所有代码，最终导致字符串被发送到语言模型。在 `ell` 中，我们将使用语言模型的一种特定方式视为一个离散的子程序，称为 **语言模型程序**。

```python
import ell

@ell.simple(model="gpt-4o")
def hello(world : str):
    """你是一个有帮助的助手，用小写字母书写。""" # 系统消息
    return f"向{world[::-1]}问好，并附上一首诗。"    # 用户消息

hello("sama")
```

![alt text](https://docs.ell.so/_static/gif1.webp)

### 2. 提示实际上是机器学习模型的参数。

提示工程的过程涉及多次迭代，类似于机器学习中的优化过程。因为语言模型程序只是函数，`ell` 提供了丰富的工具来支持这一过程。

![ell 演示](https://docs.ell.so/_static/versions_small.webp)

`ell` 通过静态和动态分析以及 `gpt-4o-mini` **自动生成的提交消息** 直接存储到 *本地存储* 中，提供了 **提示的自动版本控制和序列化**。这个过程类似于机器学习训练循环中的 `检查点`，但它不需要任何特殊的 IDE 或编辑器——所有操作都是通过常规的 Python 代码完成的。

### 3. 监控、版本控制和可视化的工具

有了正确的工具，提示工程可以从一门暗黑艺术变成一门科学。**Ell Studio 是一个本地、开源的工具，用于提示版本控制、监控和可视化**。通过 Ell Studio，您可以随着时间的推移将提示优化过程经验化，并在为时已晚之前捕捉到回归。

<picture>
  <source srcset="https://docs.ell.so/_static/ell_studio_better.webp" type="image/webp">
  <img src="docs/src/_static/ell_studio_better.webp" alt="ell studio 演示">
</picture>

```bash
ell-studio --storage ./logdir 
```

### 4. 多模态应该是第一类

LLM 可以处理和生成各种类型的内容，包括文本、图像、音频和视频。使用这些数据类型的提示工程应该像使用文本一样简单。

```python
from PIL import Image
import ell


@ell.simple(model="gpt-4o", temperature=0.1)
def describe_activity(image: Image.Image):
    return [
        ell.system("你是 VisionGPT。回答 <5 个单词，全部小写。"),
        ell.user(["描述图像中的人在做什么：", image])
    ]

# 从网络摄像头捕捉图像
describe_activity(capture_webcam_image()) # "他们在拿着一本书"
```
![ell 演示](https://docs.ell.so/_static/multimodal_compressed.webp)

`ell` 支持多模态输入和输出的丰富类型强制。您可以在语言模型程序返回的 `Message` 对象中直接使用 PIL 图像、音频和其他多模态输入。

### ...还有更多！

阅读更多内容请访问 [文档](https://docs.ell.so/)！

## 安装
要安装 `ell` 和 `ell studio`，您可以使用 pip。请按照以下步骤操作：

1. 打开您的终端或命令提示符。
2. 运行以下命令从 PyPI 安装 `ell-ai` 包：

   ```bash
   pip install ell-ai
   ```

3. 通过检查 `ell` 的版本来验证安装：

   ```bash
   python -c "import ell; print(ell.__version__)"
   ```

这将同时在您的系统上安装 `ell` 和 `ell studio`，使您能够开始使用这些工具进行提示工程和可视化。

## 下一步

探索 [文档](https://docs.ell.so/) 以了解更多关于 `ell` 及其功能的信息。按照 [入门指南](https://docs.ell.so/getting_started.html) 创建您的第一个语言模型程序。加入我们的 [Discord 社区](https://discord.gg/vWntgU52Xb) 与其他用户联系并获得支持。