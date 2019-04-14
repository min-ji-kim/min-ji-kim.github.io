# Nginx Docker 설치하기
> Nginx Docker를 설치하고 127.0.0.1에 접속시 보여줄 index.html 파일을 설정한다.


### Nginx Docker 설치 명령어
```bash
~$ sudo docker pull nginx:latest
```
### Nginx index 파일 설정
>Nginx Docker와 vloume 설정 할 폴더 및 파일 생성 
```bash
~$ mkdir share
~$ cd share
~$ mkdir nginx
~$ cd nginx
~$ mkdir html
~$ pwd
/home/mint/share/nginx/html
~$ vi index.html
wow Hello Docker
```
### Nginx Docker 컨테이너 실행
```bash
~$ docker run --name nginx-test -v /home/mint/share/nginx/html:/usr/share/nginx/html:ro -d -p 80:80 nginx

# 명령어 설명
run nginx : nginx 이미지에 option 을 주면서 실행
--name : docker container 이름 설정
-v : local 에 있는 /home/mint/nginx/html 폴더를 nginx docker의 /usr/share/nginx/html 폴더와 mount
-d : background에서 실행
-d : 포트 설정 local 80 port: nginx container 80 port
```
### localhost 접속하여 확인 
![docker](https://dl.dropboxusercontent.com/s/r6amw8e9jvm0ste/docker.JPG)



### Nginx Docker 기본 설정파일 
>local host(127.0.0.1)로 접속 시 `root`에 지정된 /usr/share/nginx/html 폴더를 확인하며, 
>`index` 로 설정된 index.html, index.htm 파일이 있는 경우 해당 파일을 띄운다.
```bash
~$ cat /etc/nginx/conf.d/default.conf

server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```

>참고 URL : https://hub.docker.com/_/nginx