---
marp: true
theme: default
paginate: true
---

# Nginx Demo on WSL (Ubuntu 24.04)

Loosely adapted from [a tutorial by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04)

---

## Edit Hosts File (Windows)

Add to C:\Windows\System32\drivers\etc\hosts:

```
127.0.0.1 ferns.internal  
127.0.0.1 cactus.internal  
```

`.internal` is a top-level domain reserved for local use but any names can be used. 

---

## Install Nginx (in WSL)

```
sudo apt update  
sudo apt install nginx
```

---

## Set Up UFW

```
sudo ufw allow "Nginx Full" 
sudo ufw enable
```

---

## Test Nginx

Visit in your browser:  
http://localhost:80  

You should see the "Welcome to Nginx" page.

---

## Create Web Root Directories

```
sudo mkdir -p /var/www/ferns/html  
sudo mkdir -p /var/www/cactus/html
```

---

## Set Ownership

```
sudo chown -R $USER:$USER /var/www/ferns/html  
sudo chown -R $USER:$USER /var/www/cactus/html
```

---

## Add index.html Files

```
nano /var/www/ferns/html/index.html  
nano /var/www/cactus/html/index.html
```

---

## Create Server Blocks

Create `/etc/nginx/sites-available/ferns`:

```
server {
        listen 80;
        listen [::]:80;

        root /var/www/ferns/html;
        index index.html index.htm index.nginx-debian.html;

        server_name ferns.internal;
        access_log /var/log/nginx/ferns.access.log;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
Repeat for `cactus`.

---

## Enable Sites

```
sudo ln -s /etc/nginx/sites-available/ferns /etc/nginx/sites-enabled/  
sudo ln -s /etc/nginx/sites-available/cactus /etc/nginx/sites-enabled/  
```

Then reload Nginx:  
`sudo systemctl reload nginx`

---

## Test It

```
curl -H "Host: ferns.internal" http://127.0.0.1  
curl -H "Host: cactus.internal" http://127.0.0.1  
```

Compare with:  
`curl http://127.0.0.1` (returns default server block)

---

## Done!

You now have two local Nginx sites running in WSL:

ferns.internal → /var/www/ferns/html  
cactus.internal → /var/www/cactus/html

---

## LOGS

```
tail -f /var/log/nginx/*.log
```

