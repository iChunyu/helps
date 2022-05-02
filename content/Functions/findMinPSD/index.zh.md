---
title: "findMinPSD"
---

# <font color="#DD8452"> findMinPSD </font>

搜索关心频段内的最优功率谱密度。这里的最优定义为在给定积分区间内谱密度（以 {{< katex >}}\mathrm{*^2/Hz}{{< /katex >}} 为单位）的积分最小。

{{< hint info >}}
本程序依赖于 [`iLPSD`]({{< ref "../iLPSD/index.zh.md" >}}) 
{{< /hint >}}

## 说明
---

- `findMinPSD(data,fs)` 使用默认设置搜索最优功率谱密度并绘制时频曲面。
- `idx = findMinPSD(data,fs,Name,Value)` 根据键值对参数设置搜索最优功率谱密度，并返回对应的时域数据索引。
- `[pxx,f] = findMinPSD(data,fs,Name,Value)` 根据键值对参数设置搜索最优功率谱密度，并返回谱密度估计值。
- `[idx,pxx,f] = findMinPSD(data,fs,Name,Value)` 根据键值对参数设置搜索最优功率谱密度，并返回索引和谱密度估计值。

## 输入
---

### data

时域数据，为一维向量。

### fs

采样率，为标量，单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}。

## 输出
---

### idx

最优谱密度的时域索引，包含开始位置和终止位置。当函数只有一个输出时输出该索引；或当函数有三个输出时，该索引为第一个输出。

### pxx

估计的最优功率谱密度，单位为 {{< katex >}}\mathrm{*^2/Hz}{{< /katex >}}。当函数有两个输出时，谱密度为第一个输出；或当函数具有三个输出时，谱密度为第二个输出。

### f

谱密度对应的频率点，单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}。当函数有多个输出时，该频率为最后一个输出。

## 参数
---

### fmin

计算功率谱密度时关心的最小频率，为标量，单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}。默认值为 `1e-3`。

### fint

计算最优功率谱的积分区间，包含两个数值，对应单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}。默认值为 `[1e-2 1e-1]`。

### xi

数据分段扫描时的重叠率，为 0～1 之间的小数，默认值为 `0.8`。

### method

计算功率谱的算法，可选值为 `'periodogram'` 和 `'LPSD'`（同 `'iLPSD'`），默认值为 `'periodogram'`。

### Jdes

当设置功率谱算法为 `'LPSD'` 时该选项有效，为 LPSD 算法的期望频率点数，为标量。默认值为 `500`。

### pfig

是否绘制扫描功率谱的时频曲面，为逻辑变量，默认值为 `true`。

