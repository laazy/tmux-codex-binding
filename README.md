# tmux-codex-binding

## 中文

把 tmux 窗口当作 Codex 任务入口。新窗口和分屏可直接打开 Codex。主 Codex 自动取名或改名后，tmux 窗口显示对应的短标题。并排开的 Codex 各自保留窗格标题。

已有的 Codex 窗口也可以接入。绑定会记录会话 ID，方便通过原对话续聊。Codex 启动出错时，窗格会保留错误信息。

[交给 Agent 安装和配置](AGENTS.md)

## English

Use tmux windows as entry points for Codex tasks. Open Codex in a new window or a split. When the main conversation gets a name or is renamed, tmux shows a short version in the window list. Side-by-side Codex conversations keep their own pane titles.

Existing Codex windows can join in. The binding records the conversation ID so you can resume the same conversation. A startup failure leaves the error visible in the pane.

[Give your agent the setup guide](AGENTS.md)
