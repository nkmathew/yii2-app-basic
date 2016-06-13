[![Build Status][svg]][repo]

### Yii 2 Basic Project Template with Database Support

A custom yii project template derived from [yiisoft/yii2-app-basic][original] that's
supposed to save you the time of adding authentication to a project created using
the basic template.

All of the authentication code is borrowed directly from the advanced template
which at first glance seems like the better option until you consider that most of
the time you're not going to need separate backend and frontend components.

You're eventually going to trim it down e.g deleting the backend folder, moving
files from the common folder to the frontend component and start updating the
namespaces at which point you will have broken all the unit tests and maybe
contemplating rage quitting. Bit dramatic but yeah it happens, especially if it's
your first time with yii.

### Installation Steps

+ Ensure you have a web server with `php >=5.4.0` installed
+ Download and extract archive:
```
wget https://github.com/nkmathew/yii2-app-basic-with-db/archive/master.zip -O master.zip
7z x master.zip
rm master.zip
```
+ Rename the resulting folder, `yii2-app-basic-with-db-master` to your project name,
  e.g `my-web-app`
+ `cd my-web-app`
+ Install dependencies with composer: `composer install --prefer-dist`
+ Create the database:
```sql
CREATE DATABASE `my_web_app` /*!40100 COLLATE 'utf8mb4_unicode_ci' */
```
+ Update the database name in `config/db.php` together with the username and
  password if not the default root user.
```php
return [
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=localhost;dbname=my_web_app',
    'username' => 'root',
    'password' => '',
    'charset' => 'utf8',
];
```
+ Create user tables by running `yii migrate`
+ Change the secret cookie validation key in `config/web.php` to some random string.
  You can generate the string with something like `uuidgen` available in Linux
  natively and through Cygwin in Windows:
```php
'request' => [
    // !!! insert a secret key in the following (if it is empty) - this is required
    // by cookie validation
    'cookieValidationKey' => '868c6cbe-8541-4d84-9a61-2585cbc88cb7',
],
```
+ Put the project in version control: `git init`
+ Commit all the files:
```shell
git add .
git commit -m "Initial commit"
```
+ You can now do your customizations and addition of new functionality after which
  you can run a server with `yii serve` while still in the root folder or with
  `php -S localhost:8080` if in the `web` folder
+ Refer to `tests/README.md` for information on running test suites

### List of Changes
+ Models, controllers, view layouts and unit tests all replaced with those from the
  advanced template
+ Pretty urls enabled
+ Some subjective code fromatting applied:
  - Empty lines separating statements removed
  - Indentation of elements within body, html and head tags, cause why not
  - Optimizing imports(done by PhpStorm)

### Directory Structure

     assets/             contains assets definition
     commands/           contains console commands (controllers)
     config/             contains application configurations
     controllers/        contains Web controller classes
     mail/               contains view files for e-mails
     migrations/         contains database migrations
     models/             contains model classes
     runtime/            contains files generated during runtime
     tests/              contains various tests for the basic application
     vendor/             contains dependent 3rd-party packages
     views/              contains view files for the Web application
     web/                contains the entry script and Web resources
     widgets/            contains frontend widgets

[original]: https://github.com/nkmathew/yii2-app-basic-with-db
[svg]: https://travis-ci.org/nkmathew/yii2-app-basic-with-db.svg?branch=master
[repo]: https://travis-ci.org/nkmathew/yii2-app-basic-with-db
