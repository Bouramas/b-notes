## TMUX - Terminal Multiplexer
Allowed to have multiple pseudo terminal logins for 1 user tied to a single controlling window
  - persistence
  - session sharing
  - multiple windows & panes

TMUX - Plugin Manager
https://github.com/tmux-plugins/tpm

Notes:
  
LEADER: the leader key is used to prefix tmux shortcuts - currently set to Ctrl+s (default is Ctrl+b)

Commands:

    LEADER + c - create new session
    LEADER + n - next window
    LEADER + " - vertical split pane
    LEADER + Arrows or hjkl - move between panes
    LEADER + ? - SEE ALL SHORTCUTS

Install plugins

    LEADER + I - in order to install a plugin

Shortcuts:
    
    list sessions -> tmux ls
    kill session -> tmux kill-session -t session_name
