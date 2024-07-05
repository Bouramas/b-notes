
## Ancestor branch

### Find the name of the ancestor's branch for the current branch.
    
    ancestor() {
      git show-branch -a \
      | sed "s/].*//" \
      | grep "\*" \
      | grep -v "$(git rev-parse --abbrev-ref HEAD)" \
      | head -n1 \
      | sed "s/^.*\[//"
    }