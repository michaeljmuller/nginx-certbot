# Reverse proxy, encryption, and password protection

This project is a fork of [wmnd's repo](https://github.com/wmnnd/nginx-certbot).

I've made the following changes:

1) substituted in my own hostnames
2) adjusted the init-letsencrypt.sh script to use `docker compose` instead of `docker-compose`.
3) added a volume to the nginx container for htpasswd
4) added my htpasswd file to .gitignore so it doesn't get checked in
5) added basic authentication to the server in nginx's configuration
6) added an extra_host entry for my server's internal IP address (so that nginx can forward connections there)

Since the nginx container exposes and listens on privelged ports (80 and 443), it must be run as root.

Running as root makes mounting volumes simpler, since everyone's UID and GID is 1.

My installation steps are as follows (all performed as root):

- clone this project to /opt/nginx-certbot 
- create an htpasswd file with `htpasswd -c /opt/nginx-certbot/data/htpasswd mmuller`
- run the init script: `./init-letsencrypt.sh`
- start the proxy: `docker compose up`

