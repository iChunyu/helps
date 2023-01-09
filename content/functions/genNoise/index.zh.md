---
title: "genNoise"
---

# <font color="#DD8452"> genNoise </font>

产生任意谱密度的噪声。

{{< hint info >}}
本程序依赖于 [`iLPSD`]({{< ref "../iLPSD/index.zh.md" >}}) 
{{< /hint >}}

## 说明
---

- `genNoise(ASD,fs)` 根据给定谱密度和采样率构造噪声数据，并绘制其功率谱密度与目标曲线对比。
- `x = genNoise(ASD,fs,N)` 根据给定的谱密度、采样率和点数生成噪声数据。
- `x = genNoise(ASD,fs,N,seed,plt)` 生成给定噪声数据并手动控制是否绘图验证。

## 输入
---

### ASD

目标噪声谱密度的匿名函数，为函数句柄。例如 `ASD = @(f) 1./sqrt(f)` 为 {{< katex >}}1/f{{< /katex >}} 噪声。

### fs

噪声数据的采样率，为标量。

### N

噪声数据点数，为标量，默认值为 `1024`。

### seed

产生噪声所用的随机数种子，为整数，默认为 `0`。

### plt

是否绘图以对比生成的噪声和目标谱密度，为逻辑值，默认为 `false`。如果该函数没有输出，则函数一定绘图进行对比。

## 输出
---

### x

生成的噪声数据。

## 使用示例

``` matlab
ASD = @(f) 0.07./f + 1;
fs = 10;
N = 1e4;
x = genNoise(ASD,fs,N,true);
```
