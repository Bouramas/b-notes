## TMUX - Terminal Multiplexer
Allowed to have multiple pseudo terminal logins for 1 user tied to a single controlling window
  - persistence
  - session sharing
  - multiple windows & panes

TMUX - Plugin Manager
https://github.com/tmux-plugins/tpm

Sessions / Windows / Panes
In TMUX you can have multiple sessions. Each session can have multiple windows and each window
can have multiple panes.

Notes:
  
LEADER: the leader key is used to prefix tmux shortcuts - currently set to Ctrl+s (default is Ctrl+b)

Install plugins

    LEADER + I - in order to install a plugin

Session Commands:
    
    LEADER + d - detach from session
    LEADER + $ - rename session

Window Commands:

    LEADER + c - create new window
    LEADER + p - previous window
    LEADER + n - next window
    LEADER + 0...9 - select window by number

Pane Commands:

    LEADER + ; - toggle last active pane
    LEADER + % - horizontal split pane
    LEADER + " - vertical split pane
    LEADER + Arrows or hjkl - switch to pane in the direction
    LEADER + { or } - move current pane left or right

General Commands:

    LEADER + ? - SEE ALL SHORTCUTS

Shortcuts:
    
    list sessions -> tmux ls
    kill session -> tmux kill-session -t session_name
    kill all session but the current -> tmux kill-session -a
    attach to last session -> tmux a 
    attach to session -> tmux a -t session_name
