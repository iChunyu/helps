---
title: "getCurrentPSD"
---

# <font color="#DD8452"> getCurrentPSD </font>

获取当前图窗内数据的功率谱密度。

{{< hint info >}}
本程序依赖于 [`iLPSD`]({{< ref "../iLPSD/index.zh.md" >}}) 
{{< /hint >}}

## 说明
---

`getCurrentPSD(fs)` 计算当前图窗内数据的功率谱密度，并在新的图窗中绘制结果。
`getCurrentPSD(fs,Name,Value)` 根据键值对参数控制 `iLPSD` 算法以及绘图选项。

## 输入
---

### fs

采样率，为标量，单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}。

## 参数
---

本程序将参数传递给 [`iLPSD`]({{< ref "../iLPSD/index.zh.md" >}})，包括以下可选参数。

### Jdes

期望的频率点数，为整数，默认值为 `1000`。

### Kdes

期望的分段次数，为整数，默认值为 `100`。

### xi

数据分段时的重叠率，为 0~1 之间的小数，默认值为 `0.5`。

### window

窗函数，为函数句柄，默认值为 `@hann`。支持自定义窗函数，但应当确保所定义的窗函数仅接受一个参数，即窗函数的长度（为整数）。

### parallel

是否使用并行计算，为逻辑变量，默认为 `false`。

### type

计算的谱类型，为字符变量，可选值有：

- `’PSD'`: 默认值，计算功率谱密度；
- `'RMS'`：计算有效值（标准差）；
- `'Amp'`：计算幅度谱。

### 绘图控制

本程序接受绘图控制的键值对，如 `'LineWidth',2`。更多绘图控制可以参考 [Plot 帮助文档](https://ww2.mathworks.cn/help/matlab/ref/plot.html?lang=en)。

