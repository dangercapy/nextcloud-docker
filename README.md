This is my self-made Nextcloud Docker instance.

This currently supports an almost complete setup just from the compose file itself. It is recommended to run this behind an NGINX reverse proxy, to use SSL on the site.

An example configuration for this can be found at ./nextcloud.conf.

You should edit a lot of things in the docker compose file before starting the container! If you don't do this you'll make it harder for yourself to get started.

For Environment variables I recommend following:
https://hub.docker.com/_/nextcloud/

Sources:
https://hub.docker.com/_/mariadb
https://hub.docker.com/_/nextcloud/
https://github.com/rcdailey/nextcloud-cronjob
https://hub.docker.com/_/redis

