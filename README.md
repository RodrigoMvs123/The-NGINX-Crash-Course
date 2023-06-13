# The-NGINX-Crash-Course

https://www.youtube.com/watch?v=7VAI73roXaY

Nginx
It is a server that is gonna to serve web content to our browser

Airbnb.ca
Inspect 
Network
Refresh
Headers 
Server: nginx

A request over the internet is made to a server that airbnb is hosted on ( AWS Server ) and it will process the request and send it back to the computer. 

Reverse Proxy 
Computer   Internet   Nginx   Server     
->                    ->           N             <-

Load Balancer 
https://www.nginx.com/resources/glossary/round-robin-load-balancing/ 
                                             ->   Server
Computer   Internet   Nginx  ->   Server     
->                   ->            N    ->    Server          
                      <-                                 <-

Encryption 
HTTPS
The server is encrypting the data that is been send ( and un encrypting ) 

Nginx
Load Balancer 
                                             ->   Server
Computer   Internet   Nginx  ->   Server     
->                   ->            N    ->    Server          
                      <-       encryption         <-

NGINX
Installation
https://www.nginx.com/resources/wiki/start/topics/tutorials/install/ ( Mac OS )

Homebrew 
Installation 
https://docs.brew.sh/Installation

Mac OS 
Terminal
laithharb@Leiths-iMac nginx % cd ~
laithharb@Leiths-iMac ~ % cd /usr/local/etc/nginx
laithharb@Leiths-iMac nginx % ls
fastcgi.conf          mime.types             servers 
…
laithharb@Leiths-iMac nginx % code .

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf

Mac OS 
Terminal
laithharb@Leiths-iMac % nginx
laithharb@Leiths-iMac %

Web Browser 
localhost:8080
Welcome to Nginx ! 
…
Inspect 
Network
Refresh
Headers ( localhost ) 
Server: nginx/1/21/6

Nginx Terminology

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf ( Example ) 
# user nobody;
worker_process 1;

#error_log logs/error.log;
#error_log logs/error.log notice;
#error_log logs/error.log info;

# pid logs/nginx.pid;


events {
       worker_connections 1024;
}

http {
       include           mime.types;
       default_type  application/octet-stream;
}

# log_format main ‘$remote_addr - $remote_user [$time-local] “$request” ’
#                                                       ‘$status $body_bytes_sent “$http_referer” ’
#                                                         ‘ “$http_user_agent” “http_x_forwarded_for” ’;

# access_log logs/access.log main;

sendfile          on;
# tcp_nopush on;

# keepalive_timeout 0;
keepalive_timeout    65;

# gzip on;

server {
       listen              8080;
       server_name localhost;

       #charsetkoi8-r;

       #access_log logs/host.access.log main;

       location / {
              root    html;
              index  index.html index.htm;
       }

# error_page 404 /404.html;

# redirect server error pages to the static page /50x.html
#
erro_page 500 502 503 504 /50x.html
localhost = /50x.html {
       root html;
}

# proxy the PHP scripts to Apache listening on 127.0.0.1:80
#
# location ~\ .php$ {
#      proxy_pass http://127.0.0.1; 
#}

# pass the PHP script to FastCGI server listening on 127.0.0.1:9000
#
# location ~\.php$ {
#      root                          html;
#      fastcgi_pass            127.0.0.1:9000;
#      fastcgi_index            index.php; 
#      fast_param               SCRIPT_FILENAME /scripts$fastcgi_script_name;
#      include                     fastcgi_param;
#}

# deny access to .htaccess files, if Apache´s document root
# concurs with nginx´s one
#
# location ~ /\.ht {
       deny all;
#}

}

# another virtual host using mix of IP-, name-, and port-based configuration 
#
# server {
#      listen             8000;
#      listen             somename:8080;
#      server_name somename alias another.alias;

#      location / {
#      listen             html;
#      index             index.html index.htm;
#      }
#}

# HTTPS server
# 
# server {
#      listen             443 ssl;
#      server_name localhost;

#      ssl_certificate         cert.pem;
#      ssl_certificate_key  cert.key;

#      ssl_session_cache    shared:SSl:1m;
#      ssl_session_timeout    5m;

#      ssl_ciphers HIGH: !aNULL: MD5;
#      ssl_prefer_server_ciphers on;

#       location / {
#              root html;
#              index index.html index.htm; 
#      }
#}
include servers/*;
}

Nginx Serving Static Content

Web Browser
HTTP Files
Index Files
Images

Mac OS 
Terminal
laithharb@Leiths-iMac % Desktop
laithharb@Leiths-iMac Desktop % mkdir mysite
laithharb@Leiths-iMac Desktop % cd mysite
laithharb@Leiths-iMac Desktop % code.
laithharb@Leiths-iMac Desktop % 

Visual Studio Code
Explorer 
MYSITE
index.html

index.html
<html>
       <body>
             <h1>Hello my friends. I am served from NGINX</h1>
       </body>
</html>


Visual Studio Code
Explorer 
NGINX
Servers
nginx.conf 

nginx.conf
http {
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;
       }
}

events {}

Web Browser
localhost:8080
Refresh
Welcome to nginx !
…

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx % 

Web Browser
localhost:8080
Refresh
Hello my friends. I am served from NGINX

NGINX Mime Types

Visual Studio Code
Explorer 
MYSITE
index.html
styles.css

styles.css
h1 {
       background-color: pink;
       color: aqua;
}


Visual Studio Code
Explorer 
MYSITE
index.html

index.html
<!DOCKTYPE html>
<html>
       <head>
              <meta char=set“UTF-8”/>
              <title>My NGINX project</title>
              <link hel=“stylesheet” href=“./styles.css”
       </head>
         <body>
             <h1>Hello my friends. I am served from NGINX</h1>
       </body>
</html>

Web Browser
localhost:8080
Refresh
Hello my friends. I am served from NGINX

Inspect 
Network
Refresh
Refresh
localhost
styles.css

styles.css
…
Content-Type: text-plain ( text/css )

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       types {
              text/css                 css;
              text/html                html;
       }

       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx % 

Web Browser
localhost:8080
Refresh
Hello my friends. I am served from NGINX

Inspect 
Network
Refresh
Refresh
localhost
styles.css

styles.css
…
Content-Type: text/css ( cmd shift r )

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;
       }
}

events{}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080
Refresh
Hello my friends. I am served from NGINX

Inspect 
Network
Refresh
Refresh
localhost
styles.css

styles.css
…
Content-Type: text/css

NGINX Location Block

Visual Studio Code
Explorer 
MYSITE
>fruits
index.html
index.html
styles.css

index.html
<!DOCKTYPE html>
<html>
       <head>
              <meta char=set“UTF-8”/>
              <title>My NGINX project</title>
       </head>
         <body>
             <ul>
                    <li>Mango</li> 
                    <li>Strawberry</li>
                    <li>Watermelon</li>                     
             </ul>
       </body>
</html>

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080/fruits/
Mango
Strawberry
Watermelon

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }

              location /carbs {
                     alias /Users/laithharb/Desktop/mysite/fruits;
              }              
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080/carbs/
Mango
Strawberry
Watermelon

Visual Studio Code
Explorer 
MYSITE
>fruits
index.html
>vegetables
veggies.html
index.html
styles.css

veggies.html
<!DOCKTYPE html>
<html>
       <head>
              <meta char=set“UTF-8”/>
              <title>My NGINX project</title>
       </head>
         <body>
             <ul>
                    <li>Lettuce</li> 
                    <li>Eggplant</li>
                    <li>Onion</li>                     
             </ul>
       </body>
</html>

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }

              location /carbs {
                     alias /Users/laithharb/Desktop/mysite/fruits;
              }
           
              location /vegetables {
                     root /Users/laithharb/Desktop/mysite;
                     try_files vegetables/veggies.html /index.html =404;             
              }             
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080/vegetables/
Lettuce
Eggplant
Onion

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              location ~* /count/[0-9] {
                     root /Users/laithharb/Desktop/mysite;
                     try_files /index.html =404;
              }

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }

              location /carbs {
                     alias /Users/laithharb/Desktop/mysite/fruits;
              }
           
              location /vegetables {
                     root /Users/laithharb/Desktop/mysite;
                     try_files vegetables/veggies.html /index.html =404;             
              }             
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080/5/
Hello my friends. I am served from NGINX

NGINX Redirect and Rewrites 

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              location ~* /count/[0-9] {
                     root /Users/laithharb/Desktop/mysite;
                     try_files /index.html =404;
              }

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }

              location /carbs {
                     alias /Users/laithharb/Desktop/mysite/fruits;
              }
           
              location /vegetables {
                     root /Users/laithharb/Desktop/mysite;
                     try_files vegetables/veggies.html /index.html =404;             
              }             
 
              location /crops {
                     return 307 /fruits;
              }
 
       }
}

events {}


Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080/crops/
Mango
Strawberry
Onion

Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              rewrite ^/number/(\w+) /count/$1;

              location ~* /count/[0-9] {
                     root /Users/laithharb/Desktop/mysite;
                     try_files /index.html =404;
              }

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }

              location /carbs {
                     alias /Users/laithharb/Desktop/mysite/fruits;
              }
           
              location /vegetables {
                     root /Users/laithharb/Desktop/mysite;
                     try_files vegetables/veggies.html /index.html =404;             
              }             
 
              location /crops {
                     return 307 /fruits;
              }
 
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx %

Web Browser
localhost:8080/number/3
Hello my friends. I am served from NGINX

NGINX Load Balancer

Load Balancer 
https://www.nginx.com/resources/glossary/round-robin-load-balancing/ 
                                             ->   Server
Computer   Internet   Nginx  ->   Server     
->                   ->            N    ->    Server          
                      <-                                 <-

Visual Studio Code
Explorer 
MYSITE
>fruits
index.html
>server
index.js
>vegetables
veggies.html
index.html
styles.css

index.js

Visual Studio Code
Terminal
laithharb@Leiths-iMac mysite % cd server
laithharb@Leiths-iMac mysite % npm init
Press ^C at any time to quit.
laithharb@Leiths-iMac mysite % npm init -y
laithharb@Leiths-iMac mysite % npm install express ( The server )

Visual Studio Code
Explorer 
MYSITE
>fruits
index.html
>server
index.js
>vegetables
veggies.html
index.html
styles.css

index.js
const express = require(“express”)

const app = express ()

app.get(“/”, (req, res) => {
       res.send(“I am a endpoint”)
})

app.listen(7777, () => {
       console.log(“listening on port 7777”)
})

Visual Studio Code
Explorer 
MYSITE
>fruits
index.html
>server
index.js
{} package.json
>vegetables
veggies.html
index.html
styles.css

package.json

{
   “name”
  “ version”
   “description”
   “main”
   “scripts {
       “echo \ “Error: no test specified\” && exit 1”,
       “start”: “node index”
},

Visual Studio Code
Terminal
laithharb@Leiths-iMac server % npm run start
Listening on port 7777

Web Browser
localhost:7777
I am a endpoint

Visual Studio Code
Explorer 
MYSITE
>fruits
index.html
>server
Dockerfile
index.js
{} package.json
>vegetables
veggies.html
index.html
styles.css

https://nodejs.org/en/docs/guides/nodejs-docker-webapp 

Dockerfile
FROM node:16

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies 
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install 
# If you are building your code for production 
# Run npm-ci - -only=production

# Bundle app source
COPY . .

EXPOSE 7777
CMD[“npm”, “run”, “start”]


Visual Studio Code
Terminal
laithharb@Leiths-iMac mysite % cd server
laithharb@Leiths-iMac server % docker build . -t myserver
laithharb@Leiths-iMac server % docker run -p 1111:7777 -d myserver
laithharb@Leiths-iMac server % 


Docker 
Container / Apps
wisardy_mendeleev myserver
RUNNING PORT: 1111

Web Browser 
localhost:1111
I am a endpoint


Visual Studio Code
Terminal
laithharb@Leiths-iMac server % docker run -p 2222:7777 -d myserver
laithharb@Leiths-iMac server % docker run -p 3333:7777 -d myserver
laithharb@Leiths-iMac server % docker run -p 4444:7777 -d myserver
laithharb@Leiths-iMac server % 


Visual Studio Code
Explorer 
NGINX
Servers
mime.types
nginx.conf 

nginx.conf
http {

       include mime.types; 

       upstream backendserver {
              server 127.0.0.1:1111;
              server 127.0.0.1:2222;
              server 127.0.0.1:3333;
              server 127.0.0.1:4444;
       }
                  
       server {
              listen 8080;
              root /Users/laithharb/Desktop/mysite;

              rewrite ^/number/(\w+) /count/$1;

             location / {
                    proxy_pass http://backendserver/;
             }

              location ~* /count/[0-9] {
                     root /Users/laithharb/Desktop/mysite;
                     try_files /index.html =404;
              }

              location /fruits {
                     root /Users/laithharb/Desktop/mysite;
              }

              location /carbs {
                     alias /Users/laithharb/Desktop/mysite/fruits;
              }
           
              location /vegetables {
                     root /Users/laithharb/Desktop/mysite;
                     try_files vegetables/veggies.html /index.html =404;             
              }             
 
              location /crops {
                     return 307 /fruits;
              }
 
       }
}

events {}

Visual Studio Code
Terminal
laithharb@Leiths-iMac nginx % nginx -s reload
laithharb@Leiths-iMac nginx % 

Web Browser
localhost:8080
I am a endpoint
