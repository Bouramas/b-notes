
You can add the following one-liner in your list of aliases in order to easily 
checkout with autocompletion while seeing the last commit of each branch:

Prerequisites:
    - Install fzf

Source: https://junegunn.github.io/fzf/getting-started/

git branch | fzf --preview 'git show --color=always {-1}' \
                 --bind 'enter:become(git checkout {-1})' \
                 --height 40% --layout reverse
