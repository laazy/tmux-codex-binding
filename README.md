# tmux-codex-title

[中文](#中文) · [English](#english)

## 中文

Codex 给对话自动取名后，tmux 窗口也会显示这个名字。窗口名最多占 16 个显示列，超出用 … 截断。之后在 Codex 里用 `/rename` 改名，窗口也会更新。

### 安装和使用

需要 Linux、Python 3、tmux 3.2 或更新版本，以及支持 `--no-daemon` 的 Codex CLI。

~~~sh
git clone https://github.com/laazy/tmux-codex-title.git
cd tmux-codex-title
install -Dm755 tmux-codex-title ~/.local/bin/tmux-codex-title
install -Dm644 tmux.conf ~/.config/tmux/codex-title.conf
~~~

把下面一行加到 `~/.tmux.conf`，然后运行 `tmux source-file ~/.tmux.conf`。

~~~tmux
source-file ~/.config/tmux/codex-title.conf
~~~

按 tmux 前缀键再按 c，在当前目录打开 Codex。发送第一条消息后，等 Codex 保存标题，窗口就会改名。前缀键加反斜杠或减号会打开分屏 Codex，分屏由 Codex 自己更新 pane 标题。要换成固定启动目录，可编辑示例配置里的 `-c` 参数。

启动器使用 `codex --yolo`，会关闭审批和沙箱。可以在脚本的 `launch` 函数里移除 `--yolo`。每个 tmux server 只运行一个同步进程。已运行的 Codex 窗口如果仍叫 codex，服务也会尝试从现有 pane 标题更新它。

## English

Show each Codex conversation's name in its tmux window. The window title is capped at 16 terminal columns, with an ellipsis when truncated. Renaming a conversation with `/rename` updates the window too.

### Install and use

Requires Linux, Python 3, tmux 3.2 or later, and a Codex CLI that supports `--no-daemon`.

~~~sh
git clone https://github.com/laazy/tmux-codex-title.git
cd tmux-codex-title
install -Dm755 tmux-codex-title ~/.local/bin/tmux-codex-title
install -Dm644 tmux.conf ~/.config/tmux/codex-title.conf
~~~

Add this line to `~/.tmux.conf`, then run `tmux source-file ~/.tmux.conf`.

~~~tmux
source-file ~/.config/tmux/codex-title.conf
~~~

Press your tmux prefix followed by c to open Codex in the current directory. Send a message and the window updates once Codex saves its title. Prefix plus backslash or hyphen opens a split whose pane title is managed by Codex. Edit the `-c` arguments in the example config to use a fixed directory.

The launcher uses `codex --yolo`, which disables approvals and sandboxing. You can remove `--yolo` from the `launch` function. One sync process runs per tmux server. For existing windows still named codex, the service also tries to use the pane title.
