---
title: "spcolor"
---

# <font color="#DD8452"> spcolor </font>

设置绘图颜色。

## 说明
---

- `spcolor` 输出当前配色方案的颜色名字及其归一化 RGB 值。
- `cVec = spcolor(num)` 根据数字索引输出对应颜色的 RGB 值。
- `cVec = spcolor(str)` 根据名称索引输出对应颜色的 RGB 值。
- `spcolor('ShowColors')` 绘图展示所有配色方案。
- `spcolor(hfig)` 将配色方案应用到指定的绘图中。
- `spcolor(_,style)` 指定配色方案。


## 输入
---

本程序仅支持单一输入，且在不同的输入条件下会有不同的效果，以便用于不同的场景。

当不给定输入时，程序仅在命令行输出当前的配色方案列表，包括颜色的名称及其归一化 RGB 值。

### num

数字索引，为整数或整数向量。在这种输入下，函数将输出对应索引下的颜色值。特别地，当输入为 `-1` 时，将输出当前配色方案下的所有颜色 RGB 值。

### str

名称索引，为字符串或字符串数组。在这种输入下，函数将输出指定名称的颜色值。特别地，当输入字符串为 `’ShowColors‘` （不区分大小写，或简化为 `’show‘`）时，程序将绘图并展示当前的配色方案。

### hfig

`figure` 或 `axes` 句柄，在这种输入下，可以将配色方案应用在当前图窗或坐标轴下的所有曲线。


### style

配色样式，默认为 `hybrid`，其他可选项有：`matplotlib`、`seaborn`、`seaborn2`。各个配色方案可以通过命令如 `spcolor('ShowColors')` 进行查看。


## 使用示例

``` matlab
N = 5;
x = linspace(0,2*pi,200)';
y = sin(x+(0:N-1)/(N-1)*pi);

% 仅把配色方案应用到指定坐标轴内的曲线
figure
ax1 = subplot(2,1,1);
plot(x,y,'k')
ax2 = subplot(2,1,2);
plot(x,y,'k')
spcolor(ax1)

% 把配色方案应用到图窗内所有曲线
figure
ax1 = subplot(2,1,1);
plot(x,y,'k')
ax2 = subplot(2,1,2);
plot(x,y,'k')
spcolor(gcf)
```

