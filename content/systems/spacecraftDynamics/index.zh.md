---
title: "航天器动力学"
---

# <font color="#DD8452"> 航天器动力学 </font>

{{< columns >}}

航天器轨道动力学和姿态动力学模型。

<--->


<div align=right>
    <img src=overview.png width=40% />
</div>

{{< /columns >}}

## 输入
---

- {{< katex >}}\mathbf{g}_s^i{{< /katex >}}：航天器受到的引力加速度；
- {{< katex >}}\mathbf{F}_{s,\mathrm{ng}}^s{{< /katex >}}：航天器受到的的非保守力；
- {{< katex >}}\mathbf{M}_s^s{{< /katex >}}：航天器受到的力矩。


## 输出
---

- {{< katex >}}\mathbf{r}_{is}^i{{< /katex >}}：航天器在惯性系下的位置；
- {{< katex >}}\mathbf{v}_{is}^i{{< /katex >}}：航天器在惯性系下的速度；
- {{< katex >}}\mathbf{a}_{s,\mathrm{ng}}^s{{< /katex >}}：非保守力引起的加速度；
- {{< katex >}}\mathfrak{q}_s^i{{< /katex >}}：航天器的姿态四元数；
- {{< katex >}}\bm{\omega}_{is}^s{{< /katex >}}：航天器角速度；
- {{< katex >}}\dot{\bm{\omega}}_{is}^s{{< /katex >}}：航天器角加速度。

说明：姿态四元数采用 {{< katex >}}\mathfrak{q} = [q_0,\, q_1,\, q_2,\, q_3]{{< /katex >}} 形式。

## 参数
---

- `Ms`：航天器的质量；
- `Js`：航天器的转动惯量矩阵；
- `r0_is_i`：航天器的初始位置；
- `v0_is_i`：航天器的初始速度；
- `omg0_is_s`：航天器的初始角速度；
- `q0_s_i`：航天器的初始姿态四元数。
