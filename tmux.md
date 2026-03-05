# TMUX

## Send a command to all windows, panels

```bash
tmux list-panes -a -F '#{pane_id}' | xargs -I{} tmux send-keys -t {} "cd $(pwd)"
```

as alias:
```bash
alias tcd='tmux list-panes -F "#{pane_id} #{pane_active}" | awk "\$2==0{print \$1}" | xargs -I{} tmux send-keys -t {} "cd $(pwd)" Enter'
```

One thing to note: send-keys literally types the command into each pane, so if a pane is running something (like vim or a process), it'll inject text there — which you probably don't want. There's no built-in tmux command to change a pane's working directory after creation.
