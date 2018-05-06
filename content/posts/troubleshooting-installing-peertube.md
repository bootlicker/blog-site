---
title: "Troubleshooting Installing Peertube"
date: 2018-05-06T16:45:03+10:00
draft: False
---

I had a lot of trouble following the peertube installation instructions. I found a lot of the instructions were not clear, and that the steps did not flow properly and were not logically connected.

Please find some troubleshooting help that may aid you as you attempt to install peertube.

# Installation

1. ALWAYS use the most up to date installation guide. At the time I am publishing this, it is [this](https://github.com/Chocobozzz/PeerTube/blob/develop/support/doc/production.md). 
2. When this guide says `install peertube`, and then digresses about CentOS, keep reading the guide to find the instructions about how to install peertube. I thought the following instructions after the digression about CentOS were CentOS-specific, but they are not. DO NOT look at earlier guides which tell you to clone the github repo and compile. ALWAYS follow these commands in order to install peertube:
  - `$ cd ../ && sudo -u peertube ln -s versions/peertube-${VERSION} ./peertube-latest`
  - `$ cd ./peertube-latest && sudo -H -u peertube yarn install --production --pure-lockfile`
3. The peertube-latest folder belongs at `/var/www/peertube/peertube-latest/`, not `/var/www/peertube/versions/../peertube-latest/`.

# Configuration

1. Put `production.yaml` in `/var/www/peertube/config`, not `/var/www/peertube/peertube-latest/config`.
2. Remove the `'` symbols from the Peertube Title, Short Description, Terms, and Description context markers, YAML does not parse them, it will throw errors. Generally, I have found YAML to be a complete and utter dick to parse files properly. It is very strict about whitespace and will completely false to parse a file if you do not format it 110% correctly. This is very silly. I do not like YAML.
3. Make sure you're careful with you generate the SSL certificate using `certbot`, because:
  1. Debian Stable, 9, does not have the latest version. Adding the certbot repos and then installing their package will perhaps install the Apache versions, AND Apache and PHP7-FPM this will cause major headaches
  2. If you choose too many of the automated options, certbot will add `server{}` context blocks to your /etc/nginx/sites-available/default vhost file, and this will cause nginx to report that your peertube domain has duplicate conflicting content blocks attached to the same ports and same domains
4. *IF* you are using a subdomain address for your peertube instance, make sure you understand how to configure DNS properly. A simple CNAME entry with a structure like this:
  - `subdomain CNAME domain.net`
should suffice. ALWAYS use your VPS's name servers.
5. Do _NOT_ automatically install the apache-python certbot packages when you install certbot on Debian 9 from the official repos. It will pull in apache and PHP7-FPM which will listen on port 9000, and give you 502 Gateway Error HTTP messages when you run peertube.service and reload nginx.service.
6. The username of the PSQL database MUST be `peertube` and the name of the PSQL database MUST be `peertube_prod`. This is hardwired into the peertube software.
