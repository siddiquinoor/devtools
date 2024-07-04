# Deployment
Extract the archive and put it in the folder you want

    Run cp .env.example .env file to copy example file to .env

Then edit your .env file with DB credentials and other settings.

    Run composer install command
    Run php artisan migrate --seed command.

Notice: seed is important, because it will create the first admin user for you.

    Run php artisan key:generate command.

If you have file/photo fields, 

    run php artisan storage:link command.

And that's it, go to your domain and login:

Default credentials
Username: admin@admin.com
Password: password

For more information, potential errors and related links, you can read more detailed installation guide here


Hosting on AWS

Login SSH:
   
    ssh -i Ec2Eu.pem ec2-user@13.42.41.48

Edit file for Virtual Host

    /etc/httpd/conf/httpd.conf

    <VirtualHost *:80>
        DocumentRoot /var/www/html/ams/public
        ServerName "ams.talent-hub.global"
        ServerAlias "www.ams.talent-hub.global"
    </VirtualHost>

    <Directory "/var/www/html/ams">
        #
        # Possible values for the Options directive are "None", "All",
        # or any combination of:
        #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
        #
        # Note that "MultiViews" must be named *explicitly* --- "Options All"
        # doesn't give it to you.
        #
        # The Options directive is both complicated and important.  Please see
        # http://httpd.apache.org/docs/2.4/mod/core.html#options
        # for more information.
        #
        Options Indexes FollowSymLinks

        #
        # AllowOverride controls what directives may be placed in .htaccess files.
        # It can be "All", "None", or any combination of the keywords:
        #   Options FileInfo AuthConfig Limit
        #
        AllowOverride All

        #
        # Controls who can get stuff from this server.
        #
        Require all granted
    </Directory>

Save and close

Then restart server 

    sudo service httpd restart


Uploading into AWS Repo
    > Create Repo
    git clone https://git-codecommit.eu-west-2.amazonaws.com/v1/repos/ams
    git add .
    git commit -am "Initial commit"
    git push origin master


Downloading into Ec2

    git clone https://git-codecommit.eu-west-2.amazonaws.com/v1/repos/ams

    Modify .env
    sudo chown -R ec2-user:ec2-user /var/www/html/ams/
    composer install
    composer update
    php artisan key:generate
    php artisan migrate
    php artisan migrate --seed
    php artisan storage:link

Install Mysql Server

    sudo yum install -y mariadb105-server
    sudo systemctl enable mariadb
    sudo mysql_secure_installation
    
    Login to Mysql Server
    mysql -uroot -p;

    