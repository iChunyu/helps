# <font color="#DD8452"> SpringLib 帮助文档 </font>

嗨，欢迎访问某春雨仿真库的在线帮助文档。

{{< hint warning >}}
本库尚处开发阶段，如果你已经获得本库的部分函数或模块，欢迎提交错误报告或功能需求。
{{< /hint >}}

## 安装

下载后从 MATLAB 进入本库的根目录，在命令行运行以下命令即可:

```MATLAB
setupLibrary
```

安装完成后会自动打开 `startup.m` 文件 (如果没有会自动创建)。取消 `%InitPlot` 的注释可以使用本仓库提供的默认绘图设置（推荐）。

## 卸载

从 MATLAB 进入本库的根目录，运行以下命令即可:

```MATLAB
setupLibrary uninstall
```

## 手动设置

对于已经拿到部分函数的小伙伴可以将其放置在单独的文件夹内，并将该文件夹添加到 MATLAB 搜索路径，相应卸载也只需要将文件夹从搜索路径移除即可。

点击主页的 __Set Path__ 可以进行设置。若使用代码，从 MATLAB 进入放置程序的文件夹中，运行以下命令即可：

```MATLAB
addpath(pwd); savepath;     % 安装
rmpath(pwd);  savepath;     % 卸载
```

