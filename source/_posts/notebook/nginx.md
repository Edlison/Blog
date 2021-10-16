# Nginx

检测配置文件
`nginx -t`

重启服务
`nginx -s reload`

若重启报错 先运行 
`nginx -c /etc/nginx/nginx.conf`

配置目录文件

- /etc/nginx: nginx配置文件目录。所有的nginx配置文件都在这里。
- /etc/nginx/nginx.conf: Nginx的主配置文件. 可以修改他来改变nginx的全局配置。
- /etc/nginx/sites-available/: 这个目录存储每一个网站的”server blocks”。nginx通常不会使用这些配置，除非它们陪连接到 sites-enabled 目录 (see below)。一般所有的server block 配置都在这个目录中设置，然后软连接到别的目录 。
- /etc/nginx/sites-enabled/: 这个目录存储生效的 “server blocks” 配置. 通常,这个配置都是链接到 sites-available目录中的配置文件
- /etc/nginx/snippets: 这个目录主要可以包含在其它nginx配置文件中的配置片段。重复的配置都可以重构为配置片段。

SSL config
```conf
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  api.gfgf.tech;
        root         /usr/share/nginx/html;

	    return 301 https://$server_name$request_uri;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
                proxy_pass http://127.0.0.1:21000;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

    server {
        listen       443 ssl http2 default_server;
        listen       [::]:443 ssl http2 default_server;
        server_name  api.gfgf.tech;
        root         /usr/share/nginx/html;

        ssl_certificate "/root/.acme.sh/api.gfgf.tech/api.gfgf.tech.cer";
        ssl_certificate_key "/root/.acme.sh/api.gfgf.tech/api.gfgf.tech.key";
        ssl_session_cache shared:SSL:1m;
        ssl_session_timeout  10m;
        ssl_ciphers HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
		proxy_pass http://localhost:21000;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
```