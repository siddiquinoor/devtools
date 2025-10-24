# Create new branch with an existing branch

    git checkout -b new_branch master

# How to revert to any branch (Ref: https://stackoverflow.com/questions/1817766/how-to-revert-to-origins-master-branchs-version-of-file)

Assuming you did not commit the file, or add it to the index, then:

    git checkout -- filename

Assuming you added it to the index, but did not commit it, then:

    git reset HEAD filename
    git checkout -- filename

Assuming you did commit it, then:

    git checkout origin/master filename

Assuming you want to blow away all commits from your branch (VERY DESTRUCTIVE):

    git reset --hard origin/master


# Delete branch from local or remote

To remove a local branch from your machine

    git branch -d {local_branch}

(use -D instead to force deleting the branch without checking merged status);

to remove a remote branch from the server:

    git push origin -d {remote_branch}