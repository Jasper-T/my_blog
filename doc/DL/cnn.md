# CNN

## 原理介绍

## 模型搭建


### Pytorch
1. import
```python

import torch
import torch.nn as nn
import torch.optim as optim
import torchvision
import torchvision.transforms as transforms
from torch.utils.data import DataLoader
```
2. 
```python
# 定义残差块（Residual Block），这是ResNet的基础组件
class ResidualBlock(nn.Module):
    def __init__(self, in_channels, out_channels, stride=1, downsample=None):
        super(ResidualBlock, self).__init__()
        # 第一层卷积，卷积核大小为3x3，步幅可变，输出通道数为out_channels
        self.conv1 = nn.Conv2d(in_channels, out_channels, kernel_size=3, stride=stride, padding=1, bias=False)
        self.bn1 = nn.BatchNorm2d(out_channels)  # Batch Normalization层
        self.relu = nn.ReLU(inplace=True)  # ReLU激活函数
        # 第二层卷积，卷积核大小为3x3，步幅固定为1
        self.conv2 = nn.Conv2d(out_channels, out_channels, kernel_size=3, stride=1, padding=1, bias=False)
        self.bn2 = nn.BatchNorm2d(out_channels)  # Batch Normalization层
        self.downsample = downsample  # 下采样模块，用于调整残差路径中的输入维度

    def forward(self, x):
        identity = x  # 保存输入x，用于残差连接
        # 如果downsample不为空，调整残差路径中的输入x（例如调整通道数或尺寸）
        if self.downsample is not None:
            identity = self.downsample(x)

        # 正向传播：卷积1 -> BN1 -> ReLU -> 卷积2 -> BN2
        out = self.conv1(x)
        out = self.bn1(out)
        out = self.relu(out)

        out = self.conv2(out)
        out = self.bn2(out)

        # 残差连接：将输入x（可能已调整）加到卷积结果上
        out += identity
        out = self.relu(out)  # 对相加后的结果应用ReLU激活函数
        return out

# 定义ResNet50网络
class ResNet50(nn.Module):
    def __init__(self, num_classes=1000):  # num_classes为分类类别数，默认为ImageNet的1000类
        super(ResNet50, self).__init__()
        self.in_channels = 64  # 初始输入通道数为64

        # 网络的第一层：7x7的卷积，步幅为2，输出通道数为64
        self.conv1 = nn.Conv2d(3, 64, kernel_size=7, stride=2, padding=3, bias=False)
        self.bn1 = nn.BatchNorm2d(64)  # Batch Normalization层
        self.relu = nn.ReLU(inplace=True)  # ReLU激活函数
        self.maxpool = nn.MaxPool2d(kernel_size=3, stride=2, padding=1)  # 最大池化层，缩小特征图尺寸

        # ResNet的4个层，分别由不同数量的残差块组成
        self.layer1 = self._make_layer(64, 3)  # 第1层，包含3个残差块
        self.layer2 = self._make_layer(128, 4, stride=2)  # 第2层，包含4个残差块，步幅为2（下采样）
        self.layer3 = self._make_layer(256, 6, stride=2)  # 第3层，包含6个残差块
        self.layer4 = self._make_layer(512, 3, stride=2)  # 第4层，包含3个残差块

        self.avgpool = nn.AdaptiveAvgPool2d((1, 1))  # 全局自适应平均池化，将特征图缩小到1x1
        self.fc = nn.Linear(512 * 4, num_classes)  # 全连接层，将特征映射到类别数

    def _make_layer(self, out_channels, blocks, stride=1):
        # 如果步幅不为1，或输入通道数不等于输出通道数（out_channels * 4），则需要下采样
        downsample = None
        if stride != 1 or self.in_channels != out_channels * 4:
            downsample = nn.Sequential(
                nn.Conv2d(self.in_channels, out_channels * 4, kernel_size=1, stride=stride, bias=False),
                nn.BatchNorm2d(out_channels * 4),
            )

        # 创建层：第一个残差块可能需要下采样
        layers = []
        layers.append(ResidualBlock(self.in_channels, out_channels, stride, downsample))
        self.in_channels = out_channels * 4  # 更新输入通道数

        # 其余的残差块不需要下采样
        for _ in range(1, blocks):
            layers.append(ResidualBlock(self.in_channels, out_channels))

        return nn.Sequential(*layers)  # 将多个模块组合成一个Sequential模型

    def forward(self, x):
        # 网络的前向传播
        x = self.conv1(x)  # 第1层卷积
        x = self.bn1(x)  # Batch Normalization
        x = self.relu(x)  # ReLU激活
        x = self.maxpool(x)  # 最大池化

        # 通过4个ResNet层
        x = self.layer1(x)
        x = self.layer2(x)
        x = self.layer3(x)
        x = self.layer4(x)

        # 全局平均池化，将特征图缩小为1x1
        x = self.avgpool(x)
        x = torch.flatten(x, 1)  # 展平为一维向量
        x = self.fc(x)  # 全连接层

        return x

# 初始化模型
model = ResNet50(num_classes=1000)

# 示例输入：生成一个形状为 (batch_size, 3, 224, 224) 的随机张量
input_tensor = torch.randn(1, 3, 224, 224)

# 前向传播
output = model(input_tensor)

# 输出结果的形状
print(output.shape)  # 对于ImageNet，输出的形状为 (1, 1000)

```


### ...


------------------------------------------------------------

**[返回主页](/README.md)**