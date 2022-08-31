---
title: "InitPlot"
---

# <font color="#DD8452"> InitPlot </font>

初始化绘图设置。

{{< hint info >}}
本程序依赖于 [`spcolor`]({{< ref "../spcolor/index.zh.md" >}}) 
{{< /hint >}}

## 说明
---

- `InitPlot` 使用默认值值初始化绘图设置。
- `InitPlot(LineWidth,FontSize,WindowStyle,Interperter)` 根据指定值初始化绘图设置。
- `InitPlot('remove')` 移除自定义设置，恢复 MATLAB 默认值。

## 输入
---

### LindWidth

绘图采用的线宽，默认值为 `2`。

### FontSize

绘图采用的坐标轴字号，默认值为 `20`。

### WindowStyle

绘图窗口样式，默认值为 `'docked'`，即将所有绘图以标签页的形式集中在一个绘图窗口。其他可选项有 `'normal'`（MATLAB 默认值），`'modal'`。

### Interpreter

绘图标记时文字的解释器，默认值为 `'latex'`。其他可选项有 `'tex'`（MATLAB 默认值）、`'none'`。

{{< hint info >}}
本程序将 `'latex'` 设置为默认解释器，在使用 `xlabel` 等进行文字标注时，若设计数学符号，必须使用 `$` 进行标注。如 `ylabel('$V_\mathrm{fed}\,\mathrm{[V/\sqrt{Hz}]}$')`。
{{< /hint >}}

## 使用示例

使用 `edit(fullfile(userpath,'startup.m'))` 建立 `startup` 脚本，该脚本会在 MATLAB 启动时自动运行。在该脚本中写入该函数，即可自动使用该绘图设置。
