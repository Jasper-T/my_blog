# AMD Xilinx Vitis

- **官网**：https://www.amd.com/en/solutions/ai.html

- **技术文档**：
    - [Vitis AI 用户指南 (UG1414)](https://docs.amd.com/r/zh-CN/ug1414-vitis-ai/Vitis-AI-%E6%A6%82%E8%BF%B0)
    - [Vitis AI Library 用户指南 (UG1354)](https://docs.amd.com/r/zh-CN/ug1354-xilinx-ai-sdk/%E7%AE%80%E4%BB%8B)
    - [Vitis AI 文档登陆页面 (UG1431)](https://docs.amd.com/v/u/zh-CN/ug1431-vitis-ai-documentation)
    - [Vitis AI 优化器用户指南 (UG1333)](https://docs.amd.com/r/3.0-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87/ug1333-ai-optimizer/vai_p_pytorch-API)
    - [适用于 Zynq UltraScale+ MPSoC 的 DPUCZDX8G 产品指南 (PG338)](https://docs.amd.com/r/zh-CN/pg338-dpu/%E6%A0%B8%E6%A6%82%E8%BF%B0)
    - [AMD Vitis™ AI](https://xilinx.github.io/Vitis-AI/3.5/html/index.html)
- **Github**:
    - [Vitis-AI](https://github.com/Xilinx/Vitis-AI)
    - [Vitis Accelerated Libraries](https://github.com/Xilinx/Vitis_Libraries)
    - [Vitis-Tutorials](https://github.com/Xilinx/Vitis-Tutorials)

## 目录

- [AMD Xilinx Vitis](#amd-xilinx-vitis)
  - [目录](#目录)
  - [1 环境设置](#1-环境设置)
    - [1.1 Dokcer](#11-dokcer)
  - [2 模型量化](#2-模型量化)
    - [2.1 替换不支持的激活函数](#21-替换不支持的激活函数)
    - [2.2 重新训练](#22-重新训练)
    - [2.3 提取不支持的后处理算子](#23-提取不支持的后处理算子)
    - [2.4 加载模型](#24-加载模型)
    - [2.5 校准](#25-校准)
    - [2.6 export](#26-export)
  - [3 模型部署](#3-模型部署)
  - [4 runtime](#4-runtime)

--------------------------------------------------

## 1 环境设置
### 1.1 Dokcer


**[目录](#目录)**

--------------------------------------------------

## 2 模型量化
### 2.1 替换不支持的激活函数
由于 Vitis AI 不支持 SiLU 激活函数, 将激活函数从 SiLU 更改为 LeakyRelu。

[Vitis AI受 PyTorch 支持的运算符](https://docs.amd.com/r/en-US/ug1414-vitis-ai/Operators-Supported-by-PyTorch)

[yolov5s各激活函数性能测试](https://wandb.ai/glenn-jocher/activations?nw=nwuserglennjocher)

```python
# self.act = nn.SiLU()
self.act = nn.LeakyReLU(26/256, inplace=True) # in place of nn.SiLU
```

### 2.2 重新训练

### 2.3 提取不支持的后处理算子

### 2.4 加载模型

### 2.5 校准

### 2.6 export



**[目录](#目录)**

--------------------------------------------------
## 3 模型部署


**[目录](#目录)**

--------------------------------------------------
## 4 runtime


**[目录](#目录)**

--------------------------------------------------
