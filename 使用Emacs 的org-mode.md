## 如何在emacs 中使用org-mode

`org-mode` 是 Emacs 中的一个功能强大的模式，用于组织、计划、记录笔记、维护 TODO 列表、撰写文档、创建演示文稿等。以下是如何在 Emacs 中使用 `org-mode` 的基本步骤：

### 1. 创建或打开一个 Org 文件:

可以创建一个 `.org` 文件或打开一个现有的 `.org` 文件。打开或创建 `.org` 文件时，Emacs 会自动进入 `org-mode`。

```
C-x C-f filename.org

```

### 2. 基本结构:

在 `org-mode` 中，标题使用 `*` 符号标记:

```
* This is a top-level heading
** This is a second-level heading
*** This is a third-level heading

```

### 3. TODO 列表:

创建 TODO 列表:

```
* TODO Buy groceries
** TODO Buy vegetables
** DONE Buy fruits

```

使用 `C-c C-t` 来循环切换 TODO 状态。

### 4. 日期和时间:

要插入一个日期或时间戳，使用 `C-c .`。如果你想要一个范围，例如一个事件的开始和结束时间，使用 `C-c !`。

### 5. 链接:

在 `org-mode` 中创建链接很简单:

```
[[<https://www.example.com>][Example Website]]

```

### 6. 列表:

创建无序列表或有序列表:

```
- Item 1
- Item 2
  - Subitem 2.1
  - Subitem 2.2

```

或

```
1. First item
2. Second item

```

### 7. 表格:

在 `org-mode` 中，创建和操作表格非常简单:

```
| Name  | Age | Address      |
|-------+-----+--------------|
| Alice | 25  | 123 Elm St.  |
| Bob   | 30  | 456 Pine St. |

```

### 8. 导出:

`org-mode` 可以将文件导出为多种格式，如 HTML、PDF、LaTeX 等。使用 `C-c C-e` 调出导出菜单。

## org-mode 里如何运行代码

在 `org-mode` 中，可以使用 org-babel 来执行内嵌的代码块。org-babel 支持多种编程语言，比如 Python、C、C++、R、JavaScript、SQL 等。

以下是如何在 `org-mode` 中设置和运行代码块的步骤：

### 1. 设置

确保你的 Emacs 配置启用了 org-babel 并允许执行你想用的编程语言。例如，要在 `org-mode` 中运行 Python 代码，你可以添加以下配置：

```
(org-babel-do-load-languages
 'org-babel-load-languages
 '((python . t))) ; 这里启用 Python

```

### 2. 在 Org 文件中添加代码块

在你的 `.org` 文件中，你可以使用以下格式添加一个代码块：

```
#+BEGIN_SRC python
print("Hello, World!")
#+END_SRC

```

在这里，`python` 指定了代码块的语言。

### 3. 运行代码块

将光标放在代码块内，然后按 `C-c C-c`。Emacs 会询问你是否真的要执行代码块。选择 `yes`，然后 `org-mode` 将执行代码并在代码块下方插入结果。

例如，上述 Python 代码块执行后的输出为：
#+RESULTS: 
: Hello, World!