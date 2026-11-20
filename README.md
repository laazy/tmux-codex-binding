# tmux-codex-binding

## 中文

把 Codex 对话和 tmux 窗口、窗格关联起来。按 tmux 前缀键，再按 `c`，就会新建窗口并立即启动 Codex。你也可以用分屏快捷键、中文标点别名或 tmux 菜单，在分屏中启动 Codex。

按推荐方式安装后，新窗口和分屏默认都从你选定的同一个 Home Repo 启动，例如 `~/workspace/home`。你也可以选择让它们沿用当前窗格的目录。

- Codex 自动生成标题或通过 `/rename` 改名后，tmux 会同步窗口标题，最多显示 16 列。分屏中的各个 Codex 也有自己的窗格标题。
- 即使多个对话从同一目录启动，也会通过各自的会话 UUID 区分。你可以用记录的 UUID 手动续聊。已有的通用 `codex` 窗口也可以同步标题。
- 每个 tmux server 只需一个监听服务。启动器支持为 Codex 单独配置代理，并会在启动失败的窗格中保留错误信息。

这个工具适合搭配 Matt Pocock 的 Home Repo Pattern。每个 Codex 对话都从同一个 Home Repo 出发，共用其中的技能、`AGENTS.md` 和文档，再按仓库里的指引找到要工作的项目。 [The Home Repo Pattern](https://www.aihero.dev/the-home-repo-pattern)

### 让 Agent 安装

把下面的提示词复制给能够访问你终端的 Agent。

```text
请读取 https://github.com/laazy/tmux-codex-binding/blob/main/AGENTS.md，按指南把 tmux-codex-binding 安装到我当前的 tmux server。先问我 Codex 的默认启动目录。保留我已有的会话和快捷键设置，并验证新开的 Codex 窗口能自动更新标题。
```

## English

Connect Codex conversations to tmux windows and panes. Press your tmux prefix, then `c`, to open a new window and launch Codex immediately. You can also launch Codex in a split using the split shortcuts, Chinese punctuation aliases, or tmux menus.

With the recommended installation, new windows and splits all start in the same Home Repo you choose, such as `~/workspace/home`. You can instead have them inherit the current pane's directory.

- When Codex generates a title or you change it with `/rename`, tmux updates the window title, displaying up to 16 columns. Each Codex conversation in a split also has its own pane title.
- Conversations stay distinct by session UUID, even when they start in the same directory. You can use a recorded UUID to resume a conversation manually. Existing generic `codex` windows can also receive title updates.
- One watcher serves the entire tmux server. The launcher supports a separate proxy for Codex and leaves startup errors visible in the pane if launch fails.

This tool fits Matt Pocock's Home Repo Pattern. Every Codex conversation starts with the same skills, `AGENTS.md`, and docs, then follows the Home Repo's pointers to the project you want to work on. [The Home Repo Pattern](https://www.aihero.dev/the-home-repo-pattern)

### Install with an agent

Copy this prompt into an agent that can access your terminal.

```text
Read https://github.com/laazy/tmux-codex-binding/blob/main/AGENTS.md and follow the guide to install tmux-codex-binding on my current tmux server. Ask me which directory Codex should open in by default. Preserve my existing sessions and key settings, and verify that a new Codex window updates its title automatically.
```
