## Terminal Prompt Customisation


Add the following  in your .bash_profile in order to customize your terminal's prompt

    # Git branch in prompt.
    parse_git_branch() {
        git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
    }

    # custom prompt
    export PS1="\[\e[1;36m\] --- ⚡️⚡️⚡️  --- | \w @ \h (\[\e[1;31m\]\u\[\e[1;36m\])|\[\e[1;33m\]\$(parse_git_branch) \[\e[1;36m\]| -- 🌶  -- \n | => \[\e[0m\]"

