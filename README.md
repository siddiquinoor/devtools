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