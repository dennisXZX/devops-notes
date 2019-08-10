### Nginx

#### Build Nginx from source code

Building Nginx from source gives you the abilities to config Nginx settings and add custom modules, which is not possible if you install Nginx from package manager.

__Steps__

- download Nginx source code from `nginx.org`. (in Ubuntu, you can use `wget https://nginx.org/download/nginx-1.17.0.tar.gz`)

- unzip the source code by `tar -zxvf nginx-1.17.0.tar.gz`

- cd into the nginx folder and run the configure command to config Nginx, such as, `./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid` (you might need to install some other tools in order to complete the configuration)

After configuration, you can run `make` to build the nginx software and `make install` to install nginx at `/etc/nginx`. 

Use `nginx -t` to check if any syntax error in the config file.

#### Configuration

__Order of priority for matching requests__

1. Exact Match `= uri`
2. Preferential Prefix Match `^~ uri`
3. REGEX Match `~* uri`
4. prefix Match `uri`

__Example Nginx Configuration for serving static website__

```
events {}

http {
  # include the mime.types file pre-defined by Nginx in /etc/nginx/mime.types
  include mime.types;

  # set up a server
  server {
    # listening port 80, which is the default port
    listen 80;
    
    # the domain name for the server
    server_name 172.17.0.2;
    
    # root folder for your website
    root /sites/demo;
        
    # set up an exact match location directive
    location = /greet {
      return 200 'hello from NGINX "/greet" location. - EXACT match';
    }
    
    # set up an prefix match location directive, so /hello and /helloworld would match
    location /hello {
      return 200 'hello from NGINX "/greet" location. - PREFIX match';
    }
    
    # set up a prefix match location directive with built-in Nginx variables
    # $arg_name can extract URL param like "http://localhost/inspect?name=dennis"
    location /inspect {
      return 200 "$host\n$uri\n$arg_name";
    }    
    
    # set up an Regex match location directive, so /hello1 and /hello2 would match
    #  '*' indicates it's not case sensitive
    location ~* /hello[0-9] {
      return 200 'hello from NGINX "/greet" location. - REGEX match';
    }
    
    # check static API key
    if ( $arg_apikey != 1234 ) {
      return 401 "Incorrect API key";
    }
    
    # set a $weekend variable
    set $weekend 'No';
    
    # use Regex to check whether the built-in variable $date_local includes 'Saturday' or 'Sunday'
    if ( $date_local ~ 'Saturday|Sunday' ) {
      set $weekend 'Yes';
    }

    # display whether it's weekend or not
    location /is_weekend {
      return 200 $weekend;
    }
    
    # set up a re-write directive
    # any request to '/user/xxx' would be re-directed to '/greet'
    # each re-write would be treated as a completely new request by Nginx
    # so it would go through all the matching rules again
    
    # we can also capture the Regex by `rewrite ^/user/(\w+) /greet/$1;`
    # so now '/user/ken' would be redirected to '/greet/ken'
    
    # you can specify this is the last re-write by 'rewrite ^/user/\w+ /greet last;'
    rewrite ^/user/\w+ /greet;
    
    # set up a re-direct directive
    location /logo {
      return 307 /thumb.png;
    }
    
    # use try_files to catch all invalid uri requests
    # any invalid request would be handled by named location '@friendly_404'
    try_files $uri, @friendly_404;
    
    location @friendly_404 {
      return 404 'Sorry, that file could not be found.';
    }
    
    # specify a logging file
    location /secure {
      # record access log in another file other than the default log file
      access_log /var/nginx/secure.access.log
      
      # disable logging in order to reduce server load
      access_log off;
      
      return 200 'Welcome to secure area.';
    }
    
  }
}
```
