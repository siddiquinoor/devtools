# Create Repository in AWS CodeCommit and configure local PC to work on them

## Step 1: Register SSH Public Key

### Upload SSH public key to IAM user.
1. Go to specific IAM user
1. Find the Security Credentials Tab
1. To upload public key under "SSH public keys for AWS CodeCommit" follow this link:

#### Ref: https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-ssh-unixes.html

IMPORTANT: Once upload the SSH Key copy the SSH Key ID from AWS console something similar to: *`APKAEIBAERJR2EXAMPLE`*


## Step 2: Edit Local SSH Configuration

Edit your SSH configuration file named config in your local ~/.ssh directory. Add the following lines to the file, where the value for User is the SSH Key ID you copied in Step 2.

    Host git-codecommit.*.amazonaws.com
    User Your-IAM-SSH-Key-ID-Here
    IdentityFile ~/.ssh/Your-Private-Key-File-Name-Here

Once you have saved the file, make sure it has the right permissions by running the following command in the ~/.ssh directory.

    chmod 600 config


## Step 3: Now clone the repositoty

    git clone ssh://git-codecommit.<region>.amazonaws.com/v1/repos/<repo_name>

