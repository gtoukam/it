

- NGINX configuration file is that it appears to be organized in a treelike structure, defined by sets of brackets ‘{ }’
- The block that these brackets define are called “contexts”.
- Specific value defined in context is called Directive.

## Main Contex
- Main Context: The most general context is the “main” or “global” context. It
is the only context that is not contained within the typical context blocks. 
- The main context represents the broadest environment for Nginx
configuration. It is used to configure details that affect the entire
application on a basic level. 
- Some common details that are configured in the main context are the user
and group to run the worker processes as, the number of workers, and the
file to save the main process’s PID.
```sh
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;
```

## Events Context
- Events Context: The “events” context is contained within the “main”
context. It is used to set global options that affect how Nginx handles
connections at a general level.
- Nginx uses an event-based connection processing model, so the directives
defined within this context determine how worker processes should handle
connections.
```s
events {
        worker_connections 768;
        # multi_accept on;
}
```
## HTTP Context
- HTTP Context: This context will contain all of the directives and other
contexts necessary to define how the program will handle HTTP or
HTTPS connections. 
- HTTP context is a sibling of the events context, so they should be
listed side-by-side, rather than nested.

## Server Context
- Server Context: This context is declared within the “http” context.
- User can have as many server blocks as you need, each of which can
handle a specific subset of connections. 

## Location Context
- Location Context: Location blocks live within server contexts and,
unlike server blocks, can be nested inside one another.
- This can be useful for creating a more general location context to catch
a certain subset of traffic, and then further processing it based on
more specific criteria with additional contexts inside.

## Upstream Context
- Upstream Context: This context is used to define and
configure “upstream” servers.
- The upstream context should be placed within the http
context, outside of any specific server contexts.
- This context defines a named pool of servers that Nginx
can then proxy requests to.

## Mail Context
- Mail Context: Function of the mail context is to provide an
area for configuring a mail proxying solution on the server. 
- The mail context is defined within the “main” or “global”
context

```t
## Main Context
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;

## Events Context
events {
    worker_connections 1024;
}

## HTTP Context
http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    log_format main '$remote_addr - $remote_user [$time_local] '
        '$request $status $body_bytes_sent '
        '"$http_referer" "$http_user_agent"';

    access_log /var/log/nginx/access.log main;

    sendfile on;
    tcp_nopush on;
    keepalive_timeout 65;

    ## Upstream Context
    upstream backend {
        server backend1.example.com;
        server backend2.example.com;
    }

    ## Server Context
    server {
        listen 80;
        server_name example.com;

        ## Location Context:
        location / {
            proxy_pass http://backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        error_page 404 /404.html;
        error_page 500 502 503 504 /50x.html;

        location = /50x.html {
            root /usr/share/nginx/html;
        }
    }
}

## Mail Context
mail {
    auth_http localhost:9000/auth;
    smtp_capabilities "SIZE 10485760";
    server {
        listen 25;
        protocol smtp;
        proxy on;
    }
}
```

## location_match
Defines what Nginx should check the request URI against
- `(none)`: If no modifiers are present, the location is interpreted as a prefix match. This
means that the location given will be matched against the beginning of the request
URI to determine a match. 
- `=: If` an equal sign is used, this block will be considered a match if the request URI
exactly matches the location given.
`~:` If a tilde modifier is present, this location will be interpreted as a case-sensitive
regular expression match.
- `~*:` If a tilde and asterisk modifier is used, the location block will be interpreted as a
case-insensitive regular expression match.
- `^~:` If a carat and tilde modifier is present, and if this block is selected as the best
non-regular expression match, regular expression matching will not take place.

## Priority of Modifiers
1. Exact Match = URI
2. Preferential Prefix Match ^~ URI
3. REGEX Match. ~* URI






## install nginx on ubuntu
```sh
apt update
apt install nginx -y
systemctl status nginx
systemctl enable nginx
systemctl reload nginx
ps aux |grep nginx
ls -l /etc/nginx/
```

nginx -t
cat /var/log/nginx/*









































