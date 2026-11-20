# tmux-codex-binding

## 中文

**把 Codex 对话绑定到 tmux 窗口和窗格。** 按 tmux 前缀键再按 `c`，新窗口会直接启动 Codex。也可以用分屏快捷键、中文标点别名或 tmux 菜单打开另一个 Codex。

按推荐方式安装后，新窗口和分屏默认都从你选定的同一个目录启动，比如 `~/workspace/home`。也可以选择沿用当前窗格的目录。

- Codex 自动取名或用 `/rename` 改名后，tmux 同步显示最多 16 列的窗口标题。分屏中的 Codex 各自保留窗格标题。
- 即使多个对话从同一个目录启动，也会按会话 ID 绑定。可以用记录的 ID 手动续聊。已有的通用 `codex` 窗口也可以同步标题。
- 一个同步服务覆盖整个 tmux server。启动器支持单独配置代理，启动失败时会在窗格里保留错误。

这个工具是为了配合 Matt Pocock 的 Home Repo Pattern。让每个 Codex 对话从同一个 Home Repo 出发，共用其中的技能、`AGENTS.md` 和文档，再通过仓库指引找到实际要工作的项目。 [The Home Repo Pattern](https://www.aihero.dev/the-home-repo-pattern)

### 让 Agent 安装

把下面这句话复制给能访问你终端的 Agent。

```text
请读取 https://github.com/laazy/tmux-codex-binding/blob/main/AGENTS.md，按指南把 tmux-codex-binding 安装到我当前的 tmux server。先问我 Codex 的默认启动目录。保留我已有的会话和快捷键设置，并验证新开的 Codex 窗口能自动更新标题。
```

## English

**Bind Codex conversations to tmux windows and panes.** Press the tmux prefix then `c` to launch Codex directly in a new window. Open another Codex in a split using the split shortcuts, Chinese punctuation aliases, or tmux menus.

With the recommended setup, new windows and splits start Codex in the same directory you choose, such as `~/workspace/home`. You can also choose to inherit the current pane's directory.

- tmux mirrors Codex's saved title, including changes from `/rename`, in a window label up to 16 columns wide. Codex conversations in splits get their own pane titles.
- Conversations started in the same directory stay distinct through their session IDs, which you can use to resume manually. Existing windows still named `codex` can also pick up titles.
- One service handles all sessions on the tmux server. The launcher supports a Codex-specific proxy and keeps startup errors visible in failed panes.

This tool is designed for Matt Pocock's Home Repo Pattern. Start each conversation in one Home Repo, share its skills, `AGENTS.md`, and docs, and follow its pointers to the repositories where the work belongs. [The Home Repo Pattern](https://www.aihero.dev/the-home-repo-pattern)

### Install with an agent

Copy this prompt into an agent that can access your terminal.

```text
Read https://github.com/laazy/tmux-codex-binding/blob/main/AGENTS.md and follow the guide to install tmux-codex-binding on my current tmux server. Ask me which directory Codex should open in by default. Preserve my existing sessions and key settings, and verify that a new Codex window updates its title automatically.
```
