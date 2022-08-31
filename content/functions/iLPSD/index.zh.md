---
title: "iLPSD"
---

# <font color="#DD8452"> iLPSD </font>

使用 LPSD 算法进行功率谱估计。

## 说明
---

- `iLPSD(data,fs)` 根据给定数据和采样率直接绘制功率谱密度。
- `h = iLPSD(data,fs)` 当只有一个输出时，绘图并输出曲线句柄。
- `[pxx,f] = iLPSD(data,fs)` 当有两个输出时，计算数据的功率谱密度，不进行绘图。
- `iLPSD(data,fs,Name,Value)` 根据给定的键值对参数进行功率谱估计并绘图。
- `[amp,f] = iLPSD(data,fs,'type','Amp')` 计算幅度谱。

## 输入
---

### data

原始数据，为向量或矩阵。当 `data` 为矩阵时，按各列分别进行计算。

### fs

采样率，以 {{< katex >}}\mathrm{Hz}{{< /katex >}} 为单位，标量。

## 输出
---

### h

当函数只有一个输出时，输出该变量，为绘制曲线句柄。

### pxx/amp

当函数有两个输出时，该变量作为第一个输出，取决于参数 `‘type’` 的设置：

- 当 `’type‘` 设置为 `’PSD‘` （默认值）时，第一位置输出为功率谱密度，单位为 {{< katex >}}\mathrm{*^2/Hz}{{< /katex >}}；
- 当 `’type‘` 设置为 `’RMS‘` 时，第一位置输出为有效值，单位为 {{< katex >}}\mathrm{*}{{< /katex >}}；
- 当 `’type‘` 设置为 `’Amp‘` 时，第一位置输出为幅值，单位为 {{< katex >}}\mathrm{*}{{< /katex >}}。

### f

当函数有两个输出时，该变量为第二个输出，对应于第一个变量各点的频率，单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}。


## 参数
---

本函数支持使用 `'Name',Value` 的形式进行额外设置，可用键值对参数如下。

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


## 使用示例

```MATLAB
ASD = @(f) 0.07./f + 1;
fs = 10;
N = 1e4;
x = genNoise(ASD,fs,N);

figure
iLPSD(x,fs)
hold on
grid on
iLPSD(x,fs,'Jdes',3e3)
iLPSD(x,fs,'win',@hamming,'LineStyle','--')
xlabel('Frequency (Hz)')
ylabel('PSD')
```

## 参考资料

1. Michael Tröbs, Gerhard Heinzel. [Improved spectrum estimation from digitized time series on a logarithmic frequency axis. Measurement](https://www.sciencedirect.com/science/article/pii/S026322410500117X). 2005.
2. [LPSD 功率谱估计](https://ichunyu.github.io/lpsd/). 某春雨的后花园.
