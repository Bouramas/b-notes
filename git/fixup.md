
## Fixup commits

Here is a fast way to execute fixup commits. If you're not aware of fixups read [this](https://medium.com/r/?url=https%3A%2F%2Ffle.github.io%2Fgit-tip-keep-your-branch-clean-with-fixup-and-autosquash.html).

You will need to modify your .bash_profile or your .zshr:

# Find the name of the ancestor's branch for the current branch.
    ancestor() {
        git show-branch -a \
        | sed "s/].*//" \
        | grep "\*" \
        | grep -v "$(git rev-parse --abbrev-ref HEAD)" \
        | head -n1 \
        | sed "s/^.*\[//"
    }

# git fixup shortcut
    fixup() {
        local previous_commit=$(git rev-parse HEAD~0)
        git add .
        git commit --fixup="$previous_commit"
        local ancestor_branch=$(ancestor)
        git rebase -i $ancestor_branch --autosquash
    }
Save and exit. 
Open the terminal execute the following in order to reload the above changes:
`source ~/.bash_profile`. Now, assuming you are in a branch named feature-X and that you've already added a commit let's say: feat: adds-new-feature, 
you can add more changes to this commit with the fixup shortcut we just created:
- Change a file
- Type fixup in your terminal and hit Enter.
- you will be prompted to rebase on the ancestor branch with a fixup so just exit the editor with `:wq` and you are done!


See the commit history → `git log --oneline`, nothing there only your 1st commit feat: adds-new-feature