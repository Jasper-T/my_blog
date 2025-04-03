# 瑞芯微Rockchip RKNN

- **官网**：https://www.rock-chips.com/

- **技术文档**：
  - [官方技术文档](https://github.com/airockchip/rknn-toolkit2/tree/master/doc)
  - [[野火]嵌入式AI应用开发实战指南—基于LubanCat-RK系列板卡](https://doc.embedfire.com/linux/rk356x/Ai/zh/latest/README.html)
  - [RKNN API](doc/sources/pdfs/03_Rockchip_RKNPU_API_Reference_RKNN_Toolkit2_V2.3.0_CN.pdf)

- **Github**:
  - [ultralytics_yolov8](https://github.com/airockchip/ultralytics_yolov8.git)
  - [rknn-toolkit2](https://github.com/airockchip/rknn-toolkit2)
  - [rknn_model_zoo](https://github.com/airockchip/rknn_model_zoo)


## 目录

- [瑞芯微Rockchip RKNN](#瑞芯微rockchip-rknn)
  - [目录](#目录)
  - [1 环境设置](#1-环境设置)
  - [2 模型量化](#2-模型量化)
  - [3 模型部署](#3-模型部署)
  - [4 runtime](#4-runtime)

--------------------------------------------------

## 1 环境设置
见[RKNPU_Quick_Start](doc/sources/pdfs/01_Rockchip_RKNPU_Quick_Start_RKNN_SDK_V2.3.0_CN.pdf)

**[目录](#目录)**

--------------------------------------------------

## 2 模型量化
```python
    model_path  = '.onnx'
    platform    = 'rk3588'
    do_quant    = 'i8'
    output_path = 'out'
    dataset     =  
    # Create RKNN object
    rknn = RKNN(verbose=False)

    # Pre-process config
    print('--> Config model')
    rknn.config(mean_values=[[0, 0, 0]], std_values=[
                    [255, 255, 255]], target_platform=platform)
    print('done')

    # Load model
    print('--> Loading model')
    ret = rknn.load_onnx(model=model_path)
    if ret != 0:
        print('Load model failed!')
        exit(ret)
    print('done')

    # Build model
    print('--> Building model')
    ret = rknn.build(do_quantization=do_quant, dataset=dataset)
    if ret != 0:
        print('Build model failed!')
        exit(ret)
    print('done')

    # Export rknn model
    print('--> Export rknn model')
    ret = rknn.export_rknn(output_path)
    if ret != 0:
        print('Export rknn model failed!')
        exit(ret)
    print('done')

    # Release
    rknn.release()
```

**[目录](#目录)**

--------------------------------------------------
## 3 模型部署


**[目录](#目录)**

--------------------------------------------------
## 4 runtime


**[目录](#目录)**

--------------------------------------------------

