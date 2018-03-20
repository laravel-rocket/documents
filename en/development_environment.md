# Development environment

This document describe how to prepare development environment.

## How to set up ( Use PHP built-in server )

PHP has built-in server

### check out this repository

```bash
% git clone [git repository url]
% cd repository-dir
```

### install needed packages

Install packages as below if needed.

#### Ubuntu:

```bash
% sudo aptitude install php7.1 php7.1-mcrypt php7.1-curl php7.1-mysql mysql-server php7.1-imagick
```

#### MacOS:
```bash
% brew install php71 php71-imagick php71-mcrypt mysql
```

### download composer and update modules

If you didn't install composer on your environment yet, need to install.


```bash
% curl -s http://getcomposer.org/installer | php
% php composer.phar update
```

### have a cup of coffee

composer update takes a few minutes.

### copy .env.example to .env and modify it

Copy sample env file first

```bash
% cp .env.example .env
```

Then you need to update mysql server setting and aws. If you use `local` on


### check if laravel recognizes your environment as "local"

```bash
% php artisan env
Current application environment: local
```

### run migration and do seeding

You need to create database ( any name you like ) on your mysql server first and modify DB_DATABASE, DB_USERNAME and DB_PASSWORD in .env file, then execute the following commands.

```bash
% php artisan migrate
% php artisan db:seed
```

### run server on local

```bash
% php artisan serve
Laravel development server started on http://localhost:8000
```

### Access to lcoal server

Default URL is: http://localhost:8000

Does it work ?
