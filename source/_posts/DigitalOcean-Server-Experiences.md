---
title: DigitalOcean Server Experiences
toc: true
date: 2022-01-30 20:45:05
tags: 
- digitalOcean
- server
- devops
- nginx
- ufw
categories: deploy
---

I bought a 1GB RAM DigitalOcean droplet for $5 a month just to deploy my cryptogame crawler to work without any interruptions.


These are the details which are done to deploy it:


## UFW - NGINX

NGINX does reverse proxy. Which means:\
You can only open port 80 for outside and decide which internal port to go with locations.\
For example:\
A request to website (goes to Port 80 by default) mapped to inner Port 4000 with the code below:

```
    listen 80 default_server;
    listen [::]:80 default_server;
    
    ...
    
    location / {
            proxy_http_version 1.1;
            proxy_cache_bypass $http_upgrade;

            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;

            proxy_pass http://localhost:4000;
    }
```

## UFW 
UFW is abbreviation for <b>Uncomplicated Firewall</b>
```
sudo ufw status
```

Which outputs
```
To                         Action      From
--                         ------      ----
3000                       ALLOW       Anywhere                  
3001                       ALLOW       Anywhere                  
80                         ALLOW       Anywhere                  
22                         ALLOW       Anywhere                  
3000 (v6)                  ALLOW       Anywhere (v6)             
3001 (v6)                  ALLOW       Anywhere (v6)             
80 (v6)                    ALLOW       Anywhere (v6)             
22 (v6)                    ALLOW       Anywhere (v6)   
```
as an example.


Port 22 was open by default which is used by ssh (connecting to this server).\
Port 80 is used by nginx.\
Port 3000 and 3001 is created by me, as i don't want to nginx to route.


## Importing DB
```
sudo -u postgres psql
create database splinterlands;
create user splinterlands_admin;
grant all privileges on database splinterlands to splinterlands_admin;

psql --host=localhost --dbname=splinterlands --username=splinterlands_admin
\i ./schema.sql // this schema was inside the splinterlands repo.
```



## PM2
To run multiple processes, we can use pm2, also as a monitoring tool.

```
npm install pm2@latest -g
pm2 start --name splinterlands_crawler npm -- start // or pm2 start ./bin/www.js
pm2 monit
```

### Killing process
```
pm2 delete splinterlands_crawler 
```

### Other commands
```
sudo service postgresql restart
\du list users
\dt
```