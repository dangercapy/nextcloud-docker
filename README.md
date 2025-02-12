This is my self-made Nextcloud Docker instance.

This currently supports an almost complete setup just from the compose file itself. It is recommended to run this behind an NGINX reverse proxy, to use SSL on the site.

An example configuration for this can be found at ./nextcloud.conf.

You should edit a lot of things in the docker compose file before starting the container! If you don't do this you'll make it harder for yourself to get started.

##SETUP GUIDE (for beginners):
Install the latest debian edition on a machine, using storage that fits your needs, in my case i use LVM to make it easier to extend my disk. If you are going to expose the machine to the internet, use good security measures and common sense.

Install git, docker and docker-compose to your machine:
```
sudo apt update && sudo apt upgrade -y && sudo apt install docker.io docker-compose git
```

Next create a user for docker:
```
sudo useradd --create-home dockeruser
```
Next add the user to the docker group:
```
sudo usermod -aG docker dockeruser
```
Now it's time to login to the dockeruser:
```
su dockeruser
```
Now clone this repo: (change the url to the one of the git page).
```
git clone (url of this page)
```
Go in to the newly created folder:
```
cd nextcloud-docker
```
It's time to edit the config!
```
nano docker-compose.yml
```
In here you can find a lot of settings, some optional.

For a basic explanation,
Lets start with the db container (found under db:):
```
- MYSQL_ROOT_PASSWORD=(create a strong root user password here, using special characters sometimes breaks the login)
- MYSQL_PASSWORD=(Create a strong password for your nextcloud database user, using special characters sometimes breaks the login)
- MYSQL_USER=(username of your choice)
```
Were done with the db now. Time to get to the app!
This is found under app:
```
- MYSQL_PASSWORD=(the mysql user password you came up with earlier)
- MYSQL_USER=(the username you came up with earlier)
- NEXTCLOUD_ADMIN_USER=(username for your web interface admin)
- NEXTCLOUD_ADMIN_PASSWORD=(password for your web interface admin)\
- NEXTCLOUD_TRUSTED_DOMAINS=(read the message under this rule)
```
The option here is only important if you use a domain name! If you don't know what this does, comment it out by placing a # infront of it like:
```
 # - NEXTCLOUD_TRUSTED_DOMAINS=
```

If you use a mail server/service like sendgrid you can fill in the underneath, else comment it out like we did with the above option.

```
- SMTP_HOST=
- SMTP_SECURE=
- SMTP_PORT=
- SMTP_AUTHTYPE=
- SMTP_NAME=
- SMTP_PASSWORD=
- MAIL_FROM_ADDRESS=
```
Comment this out if you don't use SSL certificates!
```
- OVERWRITEPROTOCOL=https
```
Change these values to a upload "Max file size".
```
- PHP_UPLOAD_LIMIT=2G
- PHP_MEMORY_LIMIT=2G
```
Next, we go to the cron container:
```
- NEXTCLOUD_CONTAINER_NAME=(If you changed the container_name inside the app, put it here. else do NOT touch this.)
```
That's it! Now to starting and testing the container! Save the file, and go back to the shell.
```
docker-compose up
```
Now you are reading what the machine does live, make sure everything starts, and open your webbrowser, navigate to the ip/url you use for NextCloud! You should now be able to login to your created administator account.
If you receive any errors, follow nextcloud's original docs.
If everything works, press
```
 ctrl + c
```
and start the container using the daemon by running:
```
 docker-compose up -d.
```

For Environment variables I recommend following: https://hub.docker.com/_/nextcloud/

Sources: https://hub.docker.com/_/mariadb https://hub.docker.com/_/nextcloud/ https://github.com/rcdailey/nextcloud-cronjob https://hub.docker.com/_/redis
