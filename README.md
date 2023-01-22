# nextcloud-docker

This is my nextcloud installation,

I run Nextcloud on a docker container, while nginx is running on the main system.

The nginx.conf is located in /etc/nginx/sites-available/sitename

The docker-compose is located in the home directory of my nextcloud user:

/home/nextcloud/nextcloud/docker-compose.yml

Make sure your nextcloud user has docker rights!

Also make sure you have installed certbot for SSL encryption.
