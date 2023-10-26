doom emacs 如何添加 左侧文件目录



`Doom Emacs` 是一个配置框架，它为 `Emacs` 提供了一个快速、健壮、且更好看的配置。如果你想在 `Doom Emacs` 中添加一个左侧的文件目录视图，你通常会使用 `treemacs` 这个插件。

`Doom Emacs` 默认已经包含了 `treemacs`，所以你只需要做一些基础的配置和键位绑定。

1. **确保 Treemacs 已经被启用**

打开你的 `~/.doom.d/init.el` 文件，确保 `treemacs` 模块已经被启用（取消其前面的注释）：

```elisp
:ui
treemacs          ; a project drawer, like neotree but cooler
```

如果你修改了这个文件，记得运行 `doom refresh` 来更新你的配置。

2. **基础使用**

默认情况下，你可以使用以下键位来操作 `treemacs`：

- `SPC o p`：打开/关闭 Treemacs
- `SPC o P`：只打开 Treemacs
- `SPC o t`：切换至 Treemacs buffer

`SPC` 是 `Doom Emacs` 的主前缀键，如果你的配置中这个键被改变了，你需要替换为你的主前缀键。

3. **Treemacs 中的操作**

一旦你打开了 Treemacs，你可以使用以下键来操作：

- `TAB`：展开/折叠目录
- `h`：隐藏 Treemacs
- `l`：展开目录
- `r`：刷新
- 可以在 Treemacs 的 buffer 中按 `?` 来查看更多的绑定。

