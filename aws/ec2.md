# Working with AWS EC2 intance

1. Prerequisites
1. How to Deploy the Next.js App to AWS EC2
1. How to Run the Next.js App in Production Mode
1. How to Run a Next.js App Forever When the Console is Closed
1. What is CodeDeploy?
1. How to Setup Auto-Deployment using CodePipeline and CodeDeploy
1. How to Attach the IAM Role to EC2
1. How to Create the CodePipeline
1. Conclusion

## Prerequisites
1. EC2 machine running Ubuntu
1. Very basic knowledge of EC2 and IAM AWS Services

## How to Deploy the Next.js App to AWS EC2

Let's assume that the Next.js app is ready to deploy.

## Creating EC2 Intance

Use AWS console to create an EC2 intance with the following configuration:
- Enter a name i.e. `GCC Nextapp from GitHub`
- OS Images `Ubuntu`
- Amazon Machine Image (AMI) `Ubuntu SErver 22.04 LTS`
- Architecture `64-bit (x86)`
- Instance type `t3.medium`
- Key pair use the old one or create a new one
- Firewall `Allow all` for the moment (we will remove http later)
- Leave all the rest of the option default
- Launch Intance

Wait for the instance to run.

## If a new .pem is generated then follow this steps
    $ chmod 600 key-pair-name.pem


## Login to EC2 from terminal

    $ ssh -i /path/key-pair-name.pem ubuntu@public_ip_address

## Add a new user into EC2

    $ ssh-keygen -y
    Enter the path of the .pem file
    Copy the ssh-rsa

    $ sudo adduser siddiquinoor
    $ sudo su - siddiquinoor
    $ id
    $ pwd
    $ mkdir .ssh
    $ chmod 700 .ssh
    $ touch .ssh/authorized_keys
    $ chmod 600 .ssh/aurhorized_keys
    $ cat >> .ssh/authorized_keys
    Paste the ssh-rsa text then press Enter and then press ctrl + D

    $ cat .ssh/authorized_keys

## Installing Node Using the Node Version Manager (latest)

    $ sudo apt update
    $ sudo apt install nodejs
    $ node -v    
    $ sudo apt install npm
    $ sudo npm cache clean -f
    $ sudo npm install -g n
    $ sudo n stable

## Clone Git repository into EC2

1. In EC2 Terminal:
    $ ssh-keygen -t rsa -b 4096 -C [your email address]
    $ chmod 600 ~/.ssh/id_rsa
    $ cat ~/.ssh/id_rsa.pub
    Copy the public key

1. Go to Github > Setting > SSH and GPG Keys

1. Create `New SSH Key`

1. Paste the code from `~/.ssh/id_rsa.pub`

1. Give it a name and Save

1. Sometimes it needs to move the public key to “/.ssh/authorized_keys” to make the public key to work in LINUX.

    $ mkdir ~/.ssh  # if you don't have /.ssh/ folder
    $ chmod 700 ~/.ssh
    $ touch ~/.ssh/authorized_keys
    $ chmod 600 ~/.ssh/authorized_keys
    $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

1. Now clone reposity using ssh
    $ git clone git@github.com:apps-technology-gcc/gcc-webapp.git


## Testing Next.js app using `npm run`
1. Navigate to the project and install the dependencies
    $ npm install
    $ npm run dev

    At this moment site should not load because of Security group inbound rules in EC2 instance
## Add inbound rules into EC2
1. Select EC2 Instance 
1. Locate `Security` Tab
1. Click the security groups (something like: sg-0941a7a3234392d732 - launch-wizard-1) 
1. Under Inbound Rules > Edit inbound rules
1. Add Rule
1. Custom TCP | 3000 | 0.0.0.0/0
1. Save Rule

Now refresh the page, site should load !!!!

** Npm install cannot find module 'semver' **
`Exit from terminal and ssh again`

## Install PM2 daemon to run the NodeJS app forever

## Setup PM2

     $ npm install pm2@latest -g

## Now we will need to create/configure an ecosystem.config.js file which will restart the default Next.js server.

    $ Create a file in web root directory `ecosystem.config.js`

    Copy/paste the template and replace the content.

    module.exports = {
    apps: [
        {
        name: 'next-site',
        cwd: ' /home/your-name/my-nextjs-project',
        script: 'npm',
        args: 'start',
        env: {
            NEXT_PUBLIC_...: 'NEXT_PUBLIC_...',
        },
        },
        // optionally a second project
    ],};

And follow this article: https://mxd.codes/articles/hosting-next-js-private-server-pm2-github-webhooks-ci-cd

## PM2 Commands

## Check status

    $ pm2 status

## Run a Node JS (Next.js) app in Development mode

    $ pm2 start npm --name "AnyName" -- run dev
    $ pm2 save

## Kill PM2 Process

    $ pm2 kill

## Auto restart apps on file change (https://pm2.keymetrics.io/docs/usage/watch-and-restart/)

    $ pm2 start npm --name "AnyName" -- run dev --watch

    or via configuration file set the option `watch: true`

## Check log while running watch mode

    $ pm2 log


## Adding Code Deploy (ref: https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html)

1. Create a file named `appspec.yml` in projet root directory and paste the following code
```
version: 0.0
os: linux
hooks:
  ApplicationStart:
    - location: deploy.sh
      timeout: 300
      runas: ubuntu
```

1. Create another file name `deploy.sh` and paste the following code:
```
#!/bin/bash
cd /home/siddiquinoor/gcc-webapp 
git pull origin pipeline
npm install &&
npm build &&
pm2 restart gcc 
```
Change the `cd /path to match with project directory`


1. Run commands
    $ sudo apt update
    $ sudo apt install ruby-full
    $ sudo apt install wget
    $ cd /home/ubuntu
    $ wget https://aws-codedeploy-me-central-1.s3.me-central-1.amazonaws.com/latest/install
    `Note the region above`

    $ chmod +x ./install
    $ sudo ./install auto
    $ sudo service codedeploy-agent status

Now follow this link for Code Deploy:
https://www.freecodecamp.org/news/ci-cd-pipeline-for-nextjs-app-with-aws/



