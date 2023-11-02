Nginx + PHP-fpm + Mysql + PhpMyAdmin
====

Docker Compose template for yii2 or simple php web app.

Docker Compose config
----

Edit .env, for example change project name to your desired project name.

Run Docker Compose
----

```
docker compose up -d
```

Enter into php container console
----

```
docker exec -it <project_name>-php-1 bash
```

Where <project_name> is your project name seted up within .env file.

Install Yii2 inside php container
----

```
composer create-project --prefer-dist yiisoft/yii2-app-advanced app
```

Initialize Yii2 environment
----

```
cd app
php init
```

Change files permissions
----

New files created with root priveleges. You can change owner to www-data, which equivalents to user 1000 from host machine.

```
chown -R www-data:www-data /var/www/app
```

If you need to use user with another id or group id, go to .env file and replace USER_ID and/or GROUP_ID value whith correct one. Then reup Docker Compose with --build option.

```
docker compose up -d --build
```

Setup Yii2 db config file
----
Edit common/config/main-local.php:

```php
return [
    'components' => [
        // ...
        'db' => [
            'class' => 'yii\db\Connection',
            // change host, dbname, username and password to your credentials
            'dsn' => 'mysql:host=mysql;dbname=db',
            'username' => 'db',
            'password' => 'secret',
            'charset' => 'utf8',
        ],
        // ...
    ],
];
```

Run initializing Yii2 migrations
----

```
php yii migrate
```
