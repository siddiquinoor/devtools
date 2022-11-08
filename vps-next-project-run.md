# Install PM2 daemon to run the NodeJS app

## Setup PM2

     $ npm install pm2@latest -g

## Now we will need to create/configure an ecosystem.config.js file which will restart the default Next.js server.

    $ cd ~
    $ pm2 init
    $ sudo nano ecosystem.config.js

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

# PM2 Commands

## Check status

    $ pm2 status

## Run a Node JS (Next.js) app in Development mode

    $ pm2 start npm --name "AnyName" -- run dev

## Kill PM2 Process

    $ pm2 kill
