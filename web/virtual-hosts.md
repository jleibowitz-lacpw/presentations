---
marp: true
theme: default
paginate: true
---

# Nginx Demo on WSL (Ubuntu 24.04)

Loosely adapted from DigitalOcean's tutorial

---

## Step 1: Install Nginx

sudo apt update  
sudo apt install nginx

---

## Step 2: Set Up UFW

sudo ufw allow 'Nginx HTTP'  
sudo ufw enable

---

## Step 3: Test Nginx

Visit in your browser:  
http://localhost:80  

You should see the "Welcome to Nginx" page.

---

## Step 4: Create Web Root Directories

sudo mkdir -p /var/www/ferns/html  
sudo mkdir -p /var/www/cactus/html

---

## Step 5: Edit Hosts File (Windows)

Add to C:\Windows\System32\drivers\etc\hosts:

127.0.0.1 ferns.internal  
127.0.0.1 cactus.internal  

.internal is reserved for local use.

---

## Step 6: Set Ownership

```
sudo chown -R $USER:$USER /var/www/ferns/html  
sudo chown -R $USER:$USER /var/www/cactus/html
```

---

## Step 7: Add index.html Files

```
echo "<h1>Ferns Site</h1>" > /var/www/ferns/html/index.html  
echo "<h1>Cactus Site</h1>" > /var/www/cactus/html/index.html
```

---

## Step 8: Create Server Blocks

Create `/etc/nginx/sites-available/ferns`:

```
server {  
 listen 80;  
 server_name ferns.internal;  
 root /var/www/ferns/html;  
 index index.html;  
}
```
Repeat for cactus.

---

## Step 9: Enable Sites

```
sudo ln -s /etc/nginx/sites-available/ferns /etc/nginx/sites-enabled/  
sudo ln -s /etc/nginx/sites-available/cactus /etc/nginx/sites-enabled/  
```

Then reload Nginx:  
`sudo systemctl reload nginx`

---

## Step 10: Test It

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

