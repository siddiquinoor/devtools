## GIT

### 1. Uploading a local repository using GIT

#

#### Initializing Git

    $ git init
    $ git add .
    $ git commit -m "First commit"
    $ git branch -M main

#### Sets the new remote

###### like: https://github.com/siddiquinoor/devtools.git

    $ git remote add origin  <REMOTE_URL>

#### Verifies the new remote URL

    $ git remote -v

#### Pushes the changes in your local repository up to the remote repository you specified as the origin

    $ git push -u origin main

#### List of Branches

    $ git branch -a

#### Switch to other branch

    $ git checkout <branch_name>

## Git Tag

### List all tags

    git tags -l

### Create Tags

   git tag -a v0.0.2 -m "Initial Microservice"

### Push Tags

    git push origin v0.0.2

### Checkout from Tags

    git clone   # clone whole repository
    git tags -l # list all tags
    git checkout tags/v0.0.2

### Even better, checkout and create a branch 

    git checkout tags/v0.0.2 -b new_branch

    

