# Doom Emacs配置C++开发环境步骤

Doom Emacs 是一个 Emacs 配置框架，旨在使 Emacs 启动速度更快、界面更现代化、并且预先配置了一些流行的插件和功能。配置 C++ 开发环境需要以下步骤：

1. **安装 Doom Emacs**： 如果你还没有安装 Doom Emacs，你可以按照其官方 GitHub 仓库中的指南进行安装：[https://github.com/hlissner/doom-emacs](https://github.com/hlissner/doom-emacs)
    
2. **启用必要的 Doom 模块**： 打开你的 `~/.doom.d/init.el` 文件并确保以下模块已被启用（取消前面的注释）：
    
    ```
    :lang
    (cc +lsp) ; C/C++/Obj-C madness
    
    ```
    
    这将启用 C++ 支持并选择 LSP (Language Server Protocol) 作为后端。
    
3. **安装 C++ Language Server**：
    
    - `ccls` 和 `clangd` 是两个流行的选择。
    - 例如，对于 `ccls`，你可以使用包管理器进行安装：
        - Ubuntu/Debian: `sudo apt-get install ccls`
        - macOS (with Homebrew): `brew install ccls`
4. **配置 LSP**： 如果你使用的是 `ccls`，Doom Emacs 通常会自动检测并使用它。但为了确保，你可以在 `~/.doom.d/config.el` 中加入以下配置：
    
    ```
    (after! lsp-mode
      (setq lsp-enable-on-type-formatting nil)
      (setq lsp-clients-clangd-executable "ccls"))
    
    ```
    
5. **其它配置（可选）**： 你可能还想加入其他 C++ 开发相关的配置，例如自动代码格式化、代码片段等。
    
    例如，为了使用 `clang-format` 来自动格式化你的代码，你可以安装 `clang-format` 并在 `~/.doom.d/config.el` 中加入以下配置：
    
    ```
    (after! cc-mode
      (setq clang-format-style-option "llvm")
      (add-hook 'c++-mode-hook #'clang-format+-mode))
    
    ```
    
6. **更新 Doom Emacs**： 在修改完配置文件后，确保在终端中运行以下命令以更新你的 Doom Emacs 配置：
    
    ```bash
    doom sync
    
    ```
    
7. **重启 Emacs**： 退出并重新启动 Doom Emacs，此时 C++ 开发环境应该已经配置完毕。
    

### 配置完C++ 开发环境后如何运行cpp文件

在 Doom Emacs 中配置完 C++ 开发环境后，运行 C++ 文件通常涉及到编译和执行二进制文件的过程。以下是如何进行操作的步骤：

1. **手动编译和运行**：
    
    1. 打开你的 C++ 文件。
        
    2. 使用 `M-x` (通常是 `Alt + x` 或 `Space x`) 打开命令执行器。
        
    3. 输入 `vterm` 并按 `Enter` 打开一个终端窗口（前提是你已启用 `vterm` 模块）。
        
    4. 在终端中，使用 g++ 或 clang++ 等编译器编译你的代码。例如：
        
        ```bash
        g++ your_file.cpp -o output_name
        
        ```
        
    5. 编译成功后，运行生成的二进制文件：
        
        ```bash
        ./output_name
        
        ```
        
2. **使用 `projectile` 运行 Makefile 或其他构建系统**:
    
    如果你的 C++ 项目使用了 Makefile、CMake 或其他构建系统，你可以使用 `projectile` 快速运行构建命令：
    
    - 在项目的任意文件中，使用 `SPC p c` (在 `evil` 模式下) 或 `M-x projectile-compile-project` 来运行项目的构建命令。
    - 如果你的项目使用 Makefile，它通常会自动运行 `make` 命令。
    - 对于其他构建系统，你可能需要在第一次运行时提供构建命令。
3. **使用快捷键**:
    
    如果你经常需要编译和运行 C++ 代码，你可以在 `~/.doom.d/config.el` 中配置一个快捷键来自动化此过程：
    
    ```
    (defun compile-and-run-cpp ()
      (interactive)
      (let ((output-file (concat (file-name-base (buffer-file-name)) ".out")))
        (compile (format "g++ %s -o %s && ./%s" (buffer-file-name) output-file output-file))))
    
    (map! :leader
          :desc "Compile and Run C++ file"
          "c r" 'compile-and-run-cpp)
    
    ```
    
    保存并同步你的 Doom 配置 (`doom sync`)。现在，你可以在任何 C++ 文件中使用 `SPC c r` (在 `evil` 模式下) 来编译和运行你的代码。
    

# Doom Emacs配置Python开发环境步骤

配置 Doom Emacs 用于 Python 开发的步骤与配置 C++ 环境类似，但需要启用和配置一些与 Python 相关的模块。以下是步骤：

1. **安装 Doom Emacs**：
    
2. **启用必要的 Doom 模块**： 在你的 `~/.doom.d/init.el` 文件中，确保以下模块已被启用（取消前面的注释）：
    
    ```
    :lang
    (python +lsp)
    
    ```
    
    这将启用 Python 支持并选择 LSP (Language Server Protocol) 作为后端。
    
3. **安装 Python Language Server**：
    
    - `pyright` 和 `pyls` 是两个流行的选择。`pyright` 由 Microsoft 维护，性能很好。
        
    - 例如，对于 `pyright`，首先需要全局安装它：
        
        ```bash
        npm install -g pyright
        
        ```
        
4. **配置 LSP**： 如果你使用的是 `pyright`，Doom Emacs 通常会自动检测并使用它。但为了确保，你可以在 `~/.doom.d/config.el` 中加入以下配置：
    
    ```
    (after! lsp-mode
      (set-lsp-priority! 'pyright 1))  ; set higher priority
    
    ```
    
5. **虚拟环境管理（可选）**： 如果你使用 `virtualenv`、`venv` 或 `conda` 等工具来管理 Python 虚拟环境，Doom Emacs 通过 `pyvenv` 模块支持它们。确保你的虚拟环境被正确地激活，LSP 会使用这个环境的 Python 解释器和库。
    
6. **其它配置（可选）**： 根据你的需求，你可以加入其他与 Python 开发相关的配置，例如自动代码格式化、代码片段、测试等。
    
    例如，为了使用 `black` 进行代码格式化，确保你已经在你的虚拟环境或全局环境中安装了 `black`，然后在 `~/.doom.d/config.el` 中加入以下配置：
    
    ```
    (after! python
      (set-formatter! 'python-mode #'black))
    
    ```
    
7. **更新 Doom Emacs**： 在修改完配置文件后，确保在终端中运行以下命令以更新你的 Doom Emacs 配置：
    
    ```bash
    doom sync
    
    ```
    
8. **重启 Emacs**： 退出并重新启动 Doom Emacs，此时 Python 开发环境应该已经配置完毕。
    

### 配置完python 环境后,如何运行py文件

在 Doom Emacs 中配置完 Python 开发环境后，你可以使用多种方式运行 Python 文件：

1. **使用内建的 `python-mode`**:
    
    - 打开你的 Python 文件。
    - 使用 `M-x` (通常是 `Alt + x` 或 `Space x`) 打开命令执行器。
    - 输入 `run-python` 并按 `Enter`。这将在 Emacs 的底部窗口中启动一个 Python REPL。
    - 在你的 Python 文件中，将光标放到你想运行的代码行或代码块上。
    - 按 `C-c C-c` (通常是 `Ctrl + c` 然后再按 `Ctrl + c`)。这将发送当前行或当前选择的代码块到 REPL 中执行。
2. **使用  `vterm`**:
    
    如果你喜欢在终端环境中运行 Python 文件，你可以使用 Doom Emacs 的内置终端：
    
    - 使用 `M-x` 打开命令执行器并输入 `vterm` (如果你启用了 `vterm` 模块)。
    - 在打开的终端窗口中，直接运行 `python your_file.py`。
3. **使用 Debugger (如 `pdb`)**:
    
    如果你想使用 Python 的内置 debugger `pdb`，你可以在代码中加入 `import pdb; pdb.set_trace()`，然后按上述方法运行文件。当执行到这一行时，代码会进入调试模式。