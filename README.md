# NAWASHI #




-------------------------------
*EC2 instance Setup*

Select:
Ubuntu 20.0 version

free-tier etc

tick boxes for HTTP, HTTPS

Create Elastic IP

Allocate Elastic IP

Connect to instance

-------------------------------

1. Update apt:
```
sudo apt update
```
2. Install git:
```
sudo apt install git
```
3. Install node:
```
sudo apt install nodejs
```
4. Install npm
```
sudo apt install npm
```
5. Install pm2:
```
sudo npm install pm2@latest -g
```
6. Upgrade nodejs:
```
curl -sL https://deb.nodesource.com/setup_16.x | sudo bash - 
sudo apt install -y nodejs
```
7. Install Nginx:
```
sudo apt install nginx
```
8. Clone the repo: (replace with your repo)
```
git clone https://github.com/Mixlodigital/nawashi.git
```
9. Install dependencies: (Replace with your folder)
```
cd nawashi
npm install
```
10. Run the server using pm2
```
pm2 start npm --name "trading-server" -- start
```
11. Update nginx file:
```
cd /etc/nginx/sites-available

sudo nano default
```
Update with this content
```
# before root
# before index
```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    location / {
        proxy_pass http://localhost:3001;
    }
}
```
Remove
try_files $uri $uri/ =404
```
To exit and save:
```
Ctrl + X --> Y
```

Test to make sure there is no error:

```
sudo nginx -t
```

Restart Nginx:

```
sudo systemctl restart nginx

```
Go back to home directory

```

cd nawashi

cd src 

nano config.js

```

Replace API KEY&PASS

```
Ctrl + X --> Y

```

Open ports 3001, 5000, 5001 in instance security on AWS console

Type server IP into url and check to find 'Welcome to auto-trader'

```
command:
pm2 monit

(this well check packet information)

```

Download/Install Insomnia https://insomnia.rest/

Click 'debug' on panel

Select POST ....Enter IP followed by webhook eg. 35.74.99.21/webhook

Type into message field:

{
  "symbol": "",
  "action": "",
  "quantity": "" ,
  "price": ""
}

Does this say 'ok'?


```

NOTE: to keep the bot running/listening for alerts on the server, the 'screen' command is needed. I have not proceeded further however.

```

