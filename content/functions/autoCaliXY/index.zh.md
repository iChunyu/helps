---
title: "autoCaliXY"
---

# <font color="#DD8452"> autoCaliXY </font>

求取阶梯信号平坦段内的平均值，并根据给定的函数模型进行拟合。

## 说明

---

- `autoCaliXY(x,y)` 使用默认设置对阶梯形式的数据进行线性拟合。
- `[xm,ym] = autoCaliXY(x,y)` 使用默认设置对阶梯形式的数据进行线性拟合，并返回阶梯平坦段内的平均值。
- `[xm,ym,xd,yd] = autoCaliXY(x,y,Name,Value)` 根据键值对参数对阶梯信号进行拟合，返回平坦段内数据的平均值和标准差。

## 输入

---

### x, y

输入数据，两者的函数关系名义上为：{{< katex >}}y = f(x){{< /katex >}}。

{{< hint info >}}
使用该函数之前请确保两个输入数据具有相同的采样率和长度，并且台阶对齐（可使用内置 [`alignsignals`](https://ww2.mathworks.cn/help/signal/ref/alignsignals.html) 函数）。
{{< /hint >}}

## 输出

---

### xm, ym

自变量和函数值在台阶平坦段内的平均值。

### xd, yd

自变量和函数值在台阶平坦段内的标准差。

## 参数

---

### sample

样本索引的标记，为两个元素的 `cell` 数组，第一个元素可以设置为采样时间，第二个元素为绘图时的标记。默认为 `{1, 'Sample'}`。

### xname, yname

`x` 和 `y` 数据的名称，分别默认为 `'x'`、`'y'`。

### StairFrom

默认为 `'x'`，表示从输入的 `x` 数据判断阶梯的边缘，可以根据数据情况将其设置为 `'y'`。

### IndexRange

输入数据的有效索引范围，默认为 `[0 inf]`。只有在该区间内的数据才会进行阶梯判断和平均、拟合。

### FlatRange

设置用于计算平坦段均值的数据范围，支持向量或 _cell_ 数组：

- 若 `FlatRange` 内的元素小于 `1`，则表示相对台阶起、止边缘的百分比；
- 若 `FlatRange` 内的元素大于 `1`，则表示相对台阶起、止边缘的数据点数。
- 若 `FlatRange` 为标量，则将其扩充为相同元素的 {{< katex >}}1 \times 2{{< /katex >}} 数组；
- 若 `FlatRange` 为数组（或标量扩充的数组），两个元素分别表示用于计算平均值的数据在平坦段起、止位置；
- 若 `FlatRange` 为 _cell_ 数组，两个元素分别表示用于计算平均值的数据的起始位置和长度。

### FlatVariation

平坦段数据长度的最大变动比，默认为 `0.1`。

根据台阶信号的差分对边缘进行检测时，数据噪声的存在可能导致边缘重复计算。利用该参数可以约束台阶宽度的变动比，从而剔除出误判的重复边缘。

### PeakStd

台阶边缘由数据差分后绝对值异常点进行判定，当异常点的数值大于 `PeakStd` 倍后，认为此处为台阶边缘。该参数默认值为 `3`。

### Drop

指定台阶索引，在拟合前抛弃该段数据，此参数默认为 `[]`。

### FitType

拟合目标函数类型，默认为 `'poly1'`，即线性拟合。相关说明可以参考内置函数 [`fit`](https://ww2.mathworks.cn/help/curvefit/fit.html) 和 [`fittype`](https://ww2.mathworks.cn/help/curvefit/fittype.html)。

### ErrorBar

展示拟合结果时是否根据平坦段数据的标准差绘制误差棒，默认为 `'none'`，其他可选项有：`'x'`、`'y'`、`'xy'`。

### CapSize

误差棒的长度，默认为 `10`。

### Marker

数据标记，当不添加误差棒时，默认为 `'o'` 绘制圆圈；当指定任意形式误差棒时，默认为 `'none'`。

### MarkerSize

数据标记的大小，默认为 `10`。

## 使用实例

```matlab
% 构造阶梯数据
nStairs = 5;
nPoints = 100;
x0 = nan(nStairs*nPoints,1);
for k = 1:nStairs
    x0((k-1)*nPoints+1:k*nPoints) = k;
end

% 加入前置和后置数据零偏
bias = zeros(50,1)+3;
x0 = [bias; x0; bias];
x = x0 + randn(size(x0))*0.03;
y = 3.14159*x0 + 2.71828 + randn(size(x0))*0.3;

% 自动标定
autoCaliXY(x,y)
```
