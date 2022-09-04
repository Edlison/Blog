---
title: Deploy registry via docker
categories: 
- VPS
tags: 
- self-hosted
- registry
---

# Intro

部署docker仓库

<!--more-->

# Compose

```yaml
version: '3.3'

services:
  registry:
    image: registry
    container_name: registry
    environment:
    - REGISTRY_AUTH=htpasswd
    - REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm
    - REGISTRY_AUTH_HTPASSWD_PATH=/auth/.htpasswd
    volumes:
      - ./auth:/auth
      - ./data:/var/lib/registry
    ports:
      - 10008:5000
```

配置密码 需要安装`apache-utils2`

```sh
htpasswd -Bbn edlison yourpasswd > auth/.htpasswd
```

# 删除仓库

1. 直接删除文件夹

```sh
rm -rf ./data/docker/registry/v2/repositories/<镜像名>
```

2. 执行垃圾回收

```sh
docker exec registry registry garbage-collect /etc/docker/registry/config.yml
```

# UI

主要有3种UI界面: konradkleine/docker-registry-frontend, hyper/docker-registry-web, Portus

## Frontend

```yaml
registry-frontend:
  image: konradkleine/docker-registry-frontend:v2
  container_name: registry-frontend
  environment:
    - ENV_DOCKER_REGISTRY_HOST=host
    - ENV_DOCKER_REGISTRY_PORT=22000
  ports:
    - 10008:80
```

如果registry开启了http验证, 前端就不能连接了, 可以通过拼接http验证的url访问, 但是进入后会暴露密钥.

## Web

```yml
registry-web:
  image: hyper/docker-registry-web:v2
  container_name: registry-web
  volumes:
    - ./config/registry-web.yml:/conf/config.yml:ro
    - ./auth/auth.key:/conf/auth.key
    - ./db:/data
  ports:
    - 10008:8080
```

web通过token验证

生成token密钥

```sh
openssl req -new -newkey rsa:4096 -days 365 -subj "/CN=localhost" \
        -nodes -x509 -keyout auth/auth.key -out auth/auth.cert
```

registry配置文件`registry.yml`

```yaml
version: 0.1

storage:
  filesystem:
    rootdirectory: /var/lib/registry

http:
  addr: 0.0.0.0:5000

auth:
  token:
    # external url to docker-web authentication endpoint
    realm: http://registry-web:8080/api/auth
    # should be same as registry.name of registry-web
    service: localhost:5000
    # should be same as registry.auth.issuer of registry-web
    issuer: 'my issuer'
    # path to auth certificate
    rootcertbundle: /auth/auth.cert
```

web配置文件`registry-web.yml`

```yaml
registry:
  # Docker registry url
  url: http://registry:5000/v2
  # Docker registry fqdn
  name: localhost:5000
  # To allow image delete, should be false
  readonly: false
  auth:
    # Enable authentication
    enabled: true
    # Token issuer
    # should equals to auth.token.issuer of docker registry
    issuer: 'my issuer'
    # Private key for token signing
    # certificate used on auth.token.rootcertbundle should signed by this key
    key: /conf/auth.key
```

在验证上还是有点问题, 而且和front差不多, 但是是用Java写的, 有点重.

# Config

```yaml
version: 0.1
log:
  accesslog:
    disabled: true
  level: debug
  formatter: text
  fields:
    service: registry
    environment: staging
  hooks:
    - type: mail
      disabled: true
      levels:
        - panic
      options:
        smtp:
          addr: mail.example.com:25
          username: mailuser
          password: password
          insecure: true
        from: sender@example.com
        to:
          - errors@example.com
loglevel: debug # deprecated: use "log"
storage:
  filesystem:
    rootdirectory: /var/lib/registry
    maxthreads: 100
  azure:
    accountname: accountname
    accountkey: base64encodedaccountkey
    container: containername
  gcs:
    bucket: bucketname
    keyfile: /path/to/keyfile
    credentials:
      type: service_account
      project_id: project_id_string
      private_key_id: private_key_id_string
      private_key: private_key_string
      client_email: client@example.com
      client_id: client_id_string
      auth_uri: http://example.com/auth_uri
      token_uri: http://example.com/token_uri
      auth_provider_x509_cert_url: http://example.com/provider_cert_url
      client_x509_cert_url: http://example.com/client_cert_url
    rootdirectory: /gcs/object/name/prefix
    chunksize: 5242880
  s3:
    accesskey: awsaccesskey
    secretkey: awssecretkey
    region: us-west-1
    regionendpoint: http://myobjects.local
    bucket: bucketname
    encrypt: true
    keyid: mykeyid
    secure: true
    v4auth: true
    chunksize: 5242880
    multipartcopychunksize: 33554432
    multipartcopymaxconcurrency: 100
    multipartcopythresholdsize: 33554432
    rootdirectory: /s3/object/name/prefix
  swift:
    username: username
    password: password
    authurl: https://storage.myprovider.com/auth/v1.0 or https://storage.myprovider.com/v2.0 or https://storage.myprovider.com/v3/auth
    tenant: tenantname
    tenantid: tenantid
    domain: domain name for Openstack Identity v3 API
    domainid: domain id for Openstack Identity v3 API
    insecureskipverify: true
    region: fr
    container: containername
    rootdirectory: /swift/object/name/prefix
  oss:
    accesskeyid: accesskeyid
    accesskeysecret: accesskeysecret
    region: OSS region name
    endpoint: optional endpoints
    internal: optional internal endpoint
    bucket: OSS bucket
    encrypt: optional data encryption setting
    secure: optional ssl setting
    chunksize: optional size valye
    rootdirectory: optional root directory
  inmemory:  # This driver takes no parameters
  delete:
    enabled: false
  redirect:
    disable: false
  cache:
    blobdescriptor: redis
  maintenance:
    uploadpurging:
      enabled: true
      age: 168h
      interval: 24h
      dryrun: false
    readonly:
      enabled: false
auth:
  silly:
    realm: silly-realm
    service: silly-service
  token:
    autoredirect: true
    realm: token-realm
    service: token-service
    issuer: registry-token-issuer
    rootcertbundle: /root/certs/bundle
  htpasswd:
    realm: basic-realm
    path: /path/to/htpasswd
middleware:
  registry:
    - name: ARegistryMiddleware
      options:
        foo: bar
  repository:
    - name: ARepositoryMiddleware
      options:
        foo: bar
  storage:
    - name: cloudfront
      options:
        baseurl: https://my.cloudfronted.domain.com/
        privatekey: /path/to/pem
        keypairid: cloudfrontkeypairid
        duration: 3000s
        ipfilteredby: awsregion
        awsregion: us-east-1, use-east-2
        updatefrenquency: 12h
        iprangesurl: https://ip-ranges.amazonaws.com/ip-ranges.json
  storage:
    - name: redirect
      options:
        baseurl: https://example.com/
reporting:
  bugsnag:
    apikey: bugsnagapikey
    releasestage: bugsnagreleasestage
    endpoint: bugsnagendpoint
  newrelic:
    licensekey: newreliclicensekey
    name: newrelicname
    verbose: true
http:
  addr: localhost:5000
  prefix: /my/nested/registry/
  host: https://myregistryaddress.org:5000
  secret: asecretforlocaldevelopment
  relativeurls: false
  draintimeout: 60s
  tls:
    certificate: /path/to/x509/public
    key: /path/to/x509/private
    clientcas:
      - /path/to/ca.pem
      - /path/to/another/ca.pem
    letsencrypt:
      cachefile: /path/to/cache-file
      email: emailused@letsencrypt.com
      hosts: [myregistryaddress.org]
  debug:
    addr: localhost:5001
    prometheus:
      enabled: true
      path: /metrics
  headers:
    X-Content-Type-Options: [nosniff]
  http2:
    disabled: false
notifications:
  events:
    includereferences: true
  endpoints:
    - name: alistener
      disabled: false
      url: https://my.listener.com/event
      headers: <http.Header>
      timeout: 1s
      threshold: 10
      backoff: 1s
      ignoredmediatypes:
        - application/octet-stream
      ignore:
        mediatypes:
           - application/octet-stream
        actions:
           - pull
redis:
  addr: localhost:6379
  password: asecret
  db: 0
  dialtimeout: 10ms
  readtimeout: 10ms
  writetimeout: 10ms
  pool:
    maxidle: 16
    maxactive: 64
    idletimeout: 300s
health:
  storagedriver:
    enabled: true
    interval: 10s
    threshold: 3
  file:
    - file: /path/to/checked/file
      interval: 10s
  http:
    - uri: http://server.to.check/must/return/200
      headers:
        Authorization: [Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==]
      statuscode: 200
      timeout: 3s
      interval: 10s
      threshold: 3
  tcp:
    - addr: redis-server.domain.com:6379
      timeout: 3s
      interval: 10s
      threshold: 3
proxy:
  remoteurl: https://registry-1.docker.io
  username: [username]
  password: [password]
compatibility:
  schema1:
    signingkeyfile: /etc/registry/key.json
    enabled: true
validation:
  manifests:
    urls:
      allow:
        - ^https?://([^/]+\.)*example\.com/
      deny:
        - ^https?://www\.example\.com/
```



# 注意

两个容器连接后, 如果内部连接, 不能访问映射在host上的端口, 而是要访问容器的端口.

这两个前端页面都需要指定`:v2`

---

References

https://docs.docker.com/registry/configuration

https://registry.hub.docker.com/r/konradkleine/docker-registry-frontend

https://www.jianshu.com/p/55ee4b6a72b6

https://blog.csdn.net/securitit/article/details/109671914

