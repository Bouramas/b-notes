## FZF - Command line fuzzy finder

More information here:
https://github.com/junegunn/fzf

    // Search with preview
    fzf --preview="bat --color=always {}"
    - hit enter
    - you will be able to search through your files and see a preview as well using bat

    // autocomplete for cd
    cd dir/**
    - hit tab
    - you will be able to search with autocomplete

    // Kill a process
    kill -9 **
    - hit tab
    - you will be able to search through the processes and delete the one you want

    // Remove an alias
    unalias **
    - hit tab
    - you will be able to search through your aliases and remove the one you don't need anymore
