# Agent guide for tmux-codex-binding

Install this for a user who wants Codex conversations tied to the tmux windows and panes where they run. Preserve their active sessions, shell conventions, and launch policy.

## What the binding does

| User action | Result |
| --- | --- |
| Prefix then c | Open a window named codex and start Codex in its main pane. |
| Prefix then backslash or hyphen | Open a side-by-side or stacked Codex pane. The aliases 、, ＼, and － do the same. |
| Open Codex from a tmux menu | Optional menu integration covers New After, New At End, New Window, Horizontal Split, and Vertical Split wherever those actions exist in the supplied menus. |
| Send the first message | After Codex saves its auto-generated title, show it in the tmux window. Limit the window label to 16 display columns, counting wide Chinese characters as two columns. Use … for truncation. |
| Use /rename in Codex | Update the bound title. The main Codex owns the window label. Codex in a split sets its own pane title. |
| Run several Codex conversations in one directory | Match managed conversations by UUID. Saved titles stay distinct even when names or working directories coincide. |
| Use an already-running Codex | The service can adopt an existing generic codex window using its pane title. It preserves custom window names and leaves legacy UUIDs unset when it cannot establish identity. |
| Codex fails to launch | Retain the failed pane and its error output. |
| Codex exits successfully | tmux closes its pane in the sample configuration. Window UUID metadata lives with the window and is useful for resuming while that window still exists. |

## Install into the user's tmux

1. Inspect the target server and its config. Use the current socket when the user names their current server. Check the existing prefix, new-window and split bindings, launch directory, Codex command, proxy policy, and menu customizations. Linux with /proc, Python 3, and tmux 3.2 or later are required. The Codex CLI must support --no-daemon and the thread-name terminal title setting.
2. Install the executable and sample bindings. Run from the repository root.

~~~sh
install -Dm755 tmux-codex-binding ~/.local/bin/tmux-codex-binding
install -Dm644 tmux.conf ~/.config/tmux/codex-binding.conf
~~~

3. Back up the existing config and add the following line to the config used by the target server. The sample keeps the user's current prefix and opens Codex in the source pane's directory. To reproduce the configuration from this project, set the working directory for all launch bindings to ~/workspace/home. Preserve a user's other key bindings and hook declarations.

~~~tmux
source-file ~/.config/tmux/codex-binding.conf
~~~

4. The sample launcher uses --yolo, which disables Codex approvals and sandboxing. Preserve that behavior when the user already requested it. Otherwise match their chosen Codex launch policy by editing the launch arguments. Keep --no-daemon so the pane's Codex process owns the rollout file used to associate it with a UUID.
5. Optional menu integration can be installed separately. Review tmux-menus.conf first. It includes the angle-bracket and Chinese punctuation menu shortcuts and the mouse menus used by the original setup. If the user already has customized menus, merge just the new-window and split-window actions. Keep existing menu labels, targeting, and creation order.

~~~sh
install -Dm644 tmux-menus.conf ~/.config/tmux/codex-binding-menus.conf
~~~

~~~tmux
source-file ~/.config/tmux/codex-binding-menus.conf
~~~

6. If the user's interactive shell wraps Codex in a proxy function, the tmux launcher starts the executable directly and needs the same proxy settings. Use the address already configured for that user. The launcher applies this setting only to Codex and keeps loopback in NO_PROXY.

~~~tmux
set-environment -g TMUX_CODEX_PROXY http://127.0.0.1:PORT
~~~

7. Validate and reload only the intended server. Replace the socket and configuration path with the ones discovered in step 1.

~~~sh
socket=$(tmux display-message -p '#{socket_path}')
tmux -S "$socket" source-file -n ~/.tmux.conf
tmux -S "$socket" source-file ~/.tmux.conf
tmux -S "$socket" list-keys -T prefix c
~~~

## Verify and troubleshoot

Use a disposable window on the chosen server. Open Codex via the prefix binding, send a harmless first message, and confirm that the window remains named codex until the conversation title is saved. Verify that the resulting label is short. Check a split or a second window to ensure it leaves the first window's title alone.

The configuration starts one watcher per tmux socket. A lock prevents duplicate watchers on config reload. The watcher discovers the rollout UUID from the Codex process's open files, caches each Codex home's session_index.jsonl, and records the UUID in the pane's @codex_session_id. A primary pane also records it on the window. For example, these commands retrieve the recorded UUID and resume the conversation from its original working directory. Use the user's selected Codex launch flags when resuming.

~~~sh
tmux show-options -wqv -t 'session:window' @codex_session_id
tmux show-options -pqv -t '%pane_id' @codex_session_id
codex resume '<UUID>'
~~~

There is no automatic post-reboot restoration or preconfigured resume shortcut. The watcher follows managed panes across all sessions on its own server. The display-name fallback for older panes does not infer a UUID from a name.

If a pane dies, capture its output before retrying. An account/read failure with workspace routing discovery timed out can indicate that an interactive-shell proxy was bypassed. Verify the actual local proxy configuration and adjust the launcher environment before respawning the pane.

~~~sh
tmux capture-pane -p -S -60 -t '%pane_id'
tmux respawn-pane -t '%pane_id'
~~~
