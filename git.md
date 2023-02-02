#### git is a free and open source distributed version control system that's responsible for everything GitHub related that happens locally on your computer.

### installation (happy)
`sudo apt-get install git-core`

## setting up

### configuration (file locations)

- system level
  - `/etc/gitconfig`
  - `<path>\GIT\etc\gitconfig`
- user level
  - `~/.gitconfig`
  - `$HOME\.gitconfig`
- project level
  - `<my-project>/.git/config`

### configuration (modifying)
- `git config -- global user.name "first-name last-name"`
- `git config -- global user.email "user@mail.com"`
- `git config -- list`
- `git config -- global color.ui auto`
- use `git config -- local user.email "user@mail.com"` if you want to push with a different email 
    - the project `.git` folder can store `--local user.email` that can be different to `--global`
### retrieving values
- `git config user.email` retrieves the email address
- `git config --global core.editor "code --wait"`
- `git config --global color.ui true`

## setup and init
- `git init` initializes an existing local git repository (hidden .git folder), config file is a project level configuration

## inspect and compare
- `git log` or `git log --oneline` shows the commit history (or, in one line) for currently active branch
- `git lot branchB..branchA` show the commit on branch B that are not in branch A
- `git diff branchB...branchA` show the diff of what is in branchA but not in branchB

## stage and snapshot
- `git status` show modified files in working directory, staged for your next commit
- `git add <file-name>` or `git add .` add file/s as it looks now locally to your next commit (stage)
- `git reset` to move the HEAD to any previous commit, discarding any changes after that commit, keeping working directory unchanged
    - `git reset` <img src = "https://wac-cdn.atlassian.com/dam/jcr:e8a43261-2460-4783-9731-1197dc8959ab/03-04%20Reset%20a%20specific%20commit.png?cdnVersion=747" width =600 height=800 />
- `git reset HEAD <file-name>` remove files from the staging area such that its the previous commit
- `git diff` or `git diff --staged` diff of what is changed (working vs. committed) or (staged vs. committed)
- `git commit -m "<description>"` commit staged content as a new commit snapshot
- `git commit --ammend` overwrite previous commit with the new staged data

## branch and merge
- `git branch` list your branches
- `git branch <branch-name>` create a new branch at the commit
- `git checkout <branch-name>` create and switch to another branch and check it out into your working directory
- `git merge <branch>` merge the specified branch's history to current one (usually master)
- `git rebase -i master` if you have modifications to a commit already at a pull request

## tracking path changes
- `git rm <file>` delete the file from project and stage the removal for commit
- `git mv <existing-path> <new-path>` change an existing file path and stage the move

## temporary commits
- `git stash` save modified and staged changes
- `git stash list` list stack-order of stashed file changes
- `git stash pop` write workign from top of stash stack`
- `git stash drop` discard the changes from top of stash stack


## ignoring patterns (`.gitignore`)
- save a file with desired patterns as .gitigonre with either direct string matches or wildcard globs.
- add a gitignore via vscode
- `/` do not look into subdirectories
- `*.txt` all the files in all subdirectories
- `directory/` ignore a directory