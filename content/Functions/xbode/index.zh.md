---
title: "xbode"
---

# <font color="#DD8452"> xbode </font>

绘制系统的 Bode 图，可指定为幅频响应或相频响应。

## 说明
---

- `xbode(sys)` 使用默认设置绘制系统的幅频响应。
- `xbode(sys,f,'Type','Magnitude')` 指定频率绘制系统的相频响应。
- `[mag,f] = xbode(sys,f,'ShowBode',true)` 计算幅频响应并输出，并将结果绘图。
- `[mag,phase,f] = xbode(sys,_)` 计算系统的频率响应并输出，可使用参数进行设置。


## 输入
---

### sys

待分析的系统，可以使用传递函数、状态空间、传递函数矩阵等；支持连续时间系统和离散时间系统。

{{< hint info >}}
如果指定了系统输入、输出名称（例如使用 `getIOTransfer` 获得的状态方程会自带 `InputName` 和 `OutputName` 属性），在构造向量、矩阵时应当遵守 MIMO 系统的规则以避免出现警告。例如单输入多输出应当构造为列向量、多输入单输出应当构造为行向量。
{{< /hint >}}


### f

可选参数，用于控制 Bode 图的频率范围，默认单位为 {{< katex >}}\mathrm{Hz}{{< /katex >}}，允许以下情形：

- 留空：此时将由 `bode` 函数控制频率范围和计算的频率点数量；
- 标量：当系统为离散系统时允许传入标量，此时对应绘图频率下限频率的对数，即 {{< katex >}}\log_{10} f_\mathrm{min}{{< /katex >}}。如此做，频率上限默认为 Nyquist 频率 {{< katex >}}f_\mathrm{max} = f_s/2{{< /katex >}}，频率点数为 {{< katex >}}100{{< /katex >}}；
- 长度为 {{< katex >}}2{{< /katex >}} 的向量：分别对应最小、最大频率的对数，即 {{< katex >}}[\,\log_{10}f_\mathrm{min},\, \log_{10}f_\mathrm{max}\,]{{< /katex >}}，默认频率点数为 {{< katex >}}100{{< /katex >}}。对于离散系统，程序会判断设置的最大频率并将其约束在 Nyquist 频率以内；
- 长度大于 {{< katex >}}2{{< /katex >}} 的向量：手动指定计算的频率点。对于离散系统，程序会判断设置的最大频率并将其约束在 Nyquist 频率以内。


## 输出
---

### mag

幅度响应，根据传入系统的尺寸不同，将有以下两种输出：

- 输入为系统向量：输出为矩阵，各列对应各子系统的频率响应；
- 输入为系统矩阵：输出为三维数组，前两个维度与输入矩阵对应（行列分别对应输出、输入），第三个维度为频率响应。

### phase

相位响应，输出形式同幅度响应规则。

### f

幅频响应和相频响应对应的频率点。


## 参数
---

### ShowBode

是否绘制 Bode 图，为逻辑值。当函数没有输出时默认为 `true`，否则默认为 `false`。

### Type

Bode 绘图选择，可选值为 `'Magnitude'` 或 `'Phase'`，分别对应绘制幅频响应和相频响应。默认值为 `'Magnitude'` 。

### TreatAs

绘图选项，可选值为 `'SISO'` 或 `'MIMO'`。当输入系统向量时，`'SISO'` 将所有的频率响应绘制在一个坐标系以便对比，`'MIMO'` 将各系统的响应绘制在多个坐标系中，子图的形状与系统向量的形状一致。该选项默认值为 `'SISO'`，但当输入系统矩阵时，将强制为 `'MIMO'`。

### 绘图控制

本程序支持使用键值对进行绘图控制，如 `'LineWidth',2`。应当注意的是：当传入系统向量或矩阵时，该选项会对所有绘图生效。因此建议只在绘制单个系统的响应时使用该功能。


## 使用示例

``` matlab
sys1 = tf(2*pi,[1 2*pi]);
sys2 = tf(20*pi,[1 20*pi]);
f = [-2 3];

figure
xbode(sys1,f)
hold on
xbode(sys2,f,'LineStyle','--')

figure
xbode([sys1;sys2],f,'TreatAs','MIMO')
```
