# tmux-codex-binding

## 中文

把 tmux 窗口当作 Codex 任务入口。新窗口和分屏可直接打开 Codex。主 Codex 自动取名或改名后，tmux 窗口显示对应的短标题。并排开的 Codex 各自保留窗格标题。

已有的 Codex 窗口也可以接入。绑定会记录会话 ID，方便通过原对话续聊。Codex 启动出错时，窗格会保留错误信息。

### 让 Agent 安装

把下面这句话复制给能访问你终端的 Agent。

> 请读取 https://github.com/laazy/tmux-codex-binding/blob/main/AGENTS.md，按指南把 tmux-codex-binding 安装到我当前的 tmux server。保留我已有的会话和快捷键设置，并验证新开的 Codex 窗口能自动更新标题。

## English

Use tmux windows as entry points for Codex tasks. Open Codex in a new window or a split. When the main conversation gets a name or is renamed, tmux shows a short version in the window list. Side-by-side Codex conversations keep their own pane titles.

Existing Codex windows can join in. The binding records the conversation ID so you can resume the same conversation. A startup failure leaves the error visible in the pane.

### Install with an agent

Copy this prompt into an agent that can access your terminal.

> Read https://github.com/laazy/tmux-codex-binding/blob/main/AGENTS.md and follow the guide to install tmux-codex-binding on my current tmux server. Preserve my existing sessions and key settings, and verify that a new Codex window updates its title automatically.
