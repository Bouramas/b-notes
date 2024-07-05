## Ignore files already commited

Here is a way to make git forget about a file you've accidentally commited. First, make sure the files you want to ignore are in the .gitignore file and then execute the following:

    git rm -r --cached .
    git add .
    git commit -am "Remove ignored files"

If you do not want to remove everything and want explicitly specify a file or a folder, use the following rm command:

    git rm --cached <file>
    git rm -r --cached <folder>

WARNING: While this will not remove the physical file from your local machine, it will remove the files from other developers' machines on their next git pull.
