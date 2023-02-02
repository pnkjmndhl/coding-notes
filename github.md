### setting github for the first time
#### using empty repo (when you already have work done)
- `git remote add origin url@togithub.com/repo.git` add a git URL as an alias, [alias] is the name of the remote repository `url` that is human readable and used in subsequent pushes
- `git pull origin main --allow-unrelated-histories` when merging an unrelated git repo, this happens when you try to pull for the the first time
- `git push -u origin main`

#### using existing repo
- `git clone <url-to-repo>`  retrieves an entire repository from a hosted location
### share and update
- `git clone <url>` retrieve an entire reposotory from github
- `git remote add <alias> <url>` add a git URL as an alias, [alias] is the name of the remote repository `url` that is human readable and used in subsequent pushes
- `git fetch <alias>` fetch down all the branches from that git repo
- `git merge <alias>/<branch>` merge a remote branch into your current branch to bring it up to date
- `git push <alias> <branch>` transmit local branch commits to the remote repository branch
- `git pull` 
    - fetch and merge any commits from the tracking remote branch, `git fetch` + `git merge`

### rewrite history
- `git rebase <branch>` apply any commits of current branch ahead of specified time
- `git reset --hard <commit>` clear staging area, rewrite working tree from specified commit


### using SSH key or HTTPS
- for HTTPS you are asked for git username and password
- SSH authenticates without exposing your username and password
    - based on the concept of public/private keys (more secure)
    - you need to configure the private repository

### generating public/private keys
- `ssh-keygen`
    - by default saved in `.ssh/` folder
    - enter the filename and passphrase 
        - using a passphrase is complicated (note: without a passphrase, any person with the access to this computer can read the passphrase)
        - donot enter a filename since it creates a file in the current directory
    - the RSA 3072 key is impossible to guess without a private key
    - this command generates 2 files, private key and public key
        - `id-rsa`->private, `id-rsa.pub`->public
- adding ssh key on gitlab
    - profile->SSH keys-> copy and paste (public key)
        - never share your private key
    - use `cat <filename>` to get the contents of the public key file



    




