docker compose up -d --build

mkdir html
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

docker compose exec app bash
php artisan migrate
php artisan test

ssh-keygen -t ed25519 -C "larave@local-docker.local"

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"


git init
git add .
git commit -m "initial commit"
git remote add origin https://github.com/vs4000portal-yahoo/html.git
git push -u origin main



root@102bcf769830:/var/www/html# git push -u origin mainget remot -v
Pushing to github.com:vs4000portal-yahoo/cicd-001--02.git
error: src refspec mainget does not match any
error: src refspec remot does not match any
error: failed to push some refs to 'github.com:vs4000portal-yahoo/cicd-001--02.git'
root@102bcf769830:/var/www/html# git remote -v
origin	git@github.com:vs4000portal-yahoo/cicd-001--02.git (fetch)
origin	git@github.com:vs4000portal-yahoo/cicd-001--02.git (push)
root@102bcf769830:/var/www/html# git remote rm origin
root@102bcf769830:/var/www/html# git remote -v
root@102bcf769830:/var/www/html# git remote add origin https://github.com/vs4000portal-yahoo/html.git
root@102bcf769830:/var/www/html# git remote -v
origin	https://github.com/vs4000portal-yahoo/html.git (fetch)
origin	https://github.com/vs4000portal-yahoo/html.git (push)






=============================

# git clone git@github.com:vs4000portal-yahoo/html.git
Cloning into 'html'...
The authenticity of host 'github.com (20.27.177.113)' can't be established.
ED25519 key fingerprint is SHA256.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
root@102bcf769830:/var/www/html# ls -la
total 16
drwxr-xr-x 3 root root 4096 Sep 23 01:50 .
drwxr-xr-x 1 root root 4096 Sep 19 00:23 ..
drwxr-xr-x 3 root root 4096 Sep 23 01:50 html
root@102bcf769830:/var/www/html# ls -la html/
total 16
drwxr-xr-x 3 root root 4096 Sep 23 01:50 .
drwxr-xr-x 3 root root 4096 Sep 23 01:50 ..
drwxr-xr-x 8 root root 4096 Sep 23 01:50 .git
-rw-r--r-- 1 root root   18 Sep 23 01:50 README.md
root@102bcf769830:/var/www/html# mv html/README.md .
root@102bcf769830:/var/www/html# mv html/.git .
root@102bcf769830:/var/www/html# ls -la
total 24
drwxr-xr-x 4 root root 4096 Sep 23 01:50 .
drwxr-xr-x 1 root root 4096 Sep 19 00:23 ..
drwxr-xr-x 8 root root 4096 Sep 23 01:50 .git
-rw-r--r-- 1 root root   18 Sep 23 01:50 README.md
drwxr-xr-x 2 root root 4096 Sep 23 01:50 html
root@102bcf769830:/var/www/html# ls -la html/
total 8
drwxr-xr-x 2 root root 4096 Sep 23 01:50 .
drwxr-xr-x 4 root root 4096 Sep 23 01:50 ..
root@102bcf769830:/var/www/html# rmdir html
root@102bcf769830:/var/www/html# ls -la
total 20
drwxr-xr-x 3 root root 4096 Sep 23 01:51 .
drwxr-xr-x 1 root root 4096 Sep 19 00:23 ..
drwxr-xr-x 8 root root 4096 Sep 23 01:50 .git
-rw-r--r-- 1 root root   18 Sep 23 01:50 README.md
root@102bcf769830:/var/www/html# git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean

=================
root@102bcf769830:/var/www/html# cd ..
root@102bcf769830:/var/www# ls -la
total 20
drwxr-xr-x 1 root root 4096 Sep 19 00:23 .
drwxr-xr-x 1 root root 4096 Sep 19 00:23 ..
drwxr-xr-x 3 root root 4096 Sep 23 01:51 html
root@102bcf769830:/var/www# mv html/.git/ .
root@102bcf769830:/var/www# mv html/README.md .
root@102bcf769830:/var/www# cd html/
root@102bcf769830:/var/www/html# composer create-project --prefer-dist laravel/laravel .


# Laravelプロジェクトを作成
composer create-project --prefer-dist laravel/laravel .

# 環境構築
cp .env.example .env
php artisan key:generate
root@102bcf769830:/var/www/html# php artisan key:generate

   INFO  Application key set successfully.  

root@102bcf769830:/var/www/html# php artisan env

   INFO  The application environment is [local].  
ルート一覧
root@102bcf769830:/var/www/html# php artisan route:list

  GET|HEAD  / ................................................................................................. routes/web.php:5
  GET|HEAD  storage/{path} storage.local › vendor/laravel/framework/src/Illuminate/Filesystem/FilesystemServiceProvider.php:111
  PUT       storage/{path} storage.local.upload › vendor/laravel/framework/src/Illuminate/Filesystem/FilesystemServiceProvider.…
  GET|HEAD  up ..................... vendor/laravel/framework/src/Illuminate/Foundation/Configuration/ApplicationBuilder.php:224

                                                                                                              Showing [4] routes

=========================== GitHub ActionsのCI設定を追加
.github/workflows/ci.yml
.env.github
phpunit.xmlへの追記（環境変数）


===============================================Dockerfile
FROM php:8.5-apache

RUN apt-get update && apt-get install -y \
    libzip-dev zip unzip git curl \
    && docker-php-ext-install pdo_mysql zip

ENV APACHE_DOCUMENT_ROOT /var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf

WORKDIR /var/www/html

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer




===============================================
===============================================docker-compose.yml
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: laravel_app
    ports:
      - "8000:80"
    volumes:
      - ./html:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:8.0
    container_name: laravel_db
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: laravel
      MYSQL_USER: laravel
      MYSQL_PASSWORD: laravel
##### End of File #####

===============================================
