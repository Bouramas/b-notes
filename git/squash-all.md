
## Squash all commits into one

You can create a squash-all commit right from HEAD, without rebasing at all:

    git reset $(git commit-tree HEAD^{tree} -m "A new start")

