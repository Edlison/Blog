# Docker-NextCloud


## docker-compose.yml
```yaml
version: '2'

services:
  nextcloud:
    image: nextcloud
    container_name: nextcloud
    volumes:
      - ./nextcloud:/var/www/html
      - ./apps:/var/www/html/custom_apps
      - ./config:/var/www/html/config
      - ./data:/var/www/html/data
      - ./theme:/var/www/html/themes
    ports:
      - 10030:80
```

# trusted_domains

```
'trusted_domains' =>
array (
0 => 'localhost',
1 => 'server1.example.com',
2 => '192.168.1.50',
3 => '[fe80::1:50]',
),
```

