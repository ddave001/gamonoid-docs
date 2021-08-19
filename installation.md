---
description: How to install gamonoid framework
---

# Installation
---
description: This section covers all the steps needed to manually configure Gamonoid on your server.
---

## Download and Extract Gamonoid Latest Release
1. You can download Gamonoid from \([https://github.com/gamonoid/gamonoidapp](https://github.com/gamonoid/gamonoidapp)\).
2. Extract Gamonoid to public web directory root on your web server.

**Let us assume your public web directroy root to be \(/var/www/\)**

## Create a MySQL Database

Create a database and a user by using the below mysql queries.

```text
mysql> create database gamonoid;
mysql> create user 'gamonoid_user'@'localhost' identified by 'gamonoid_pwd';
mysql> grant all on gamonoid.* to 'gamonoid_user'@'localhost';
```
## Creating the configuration file

Inside `gamonoidapp/app/directory` you will find a file named **config.sample.php**. 

Rename **config.sample.php** as **config.php** and start updating it.

The **config.php** will look like this:
```text
<?php 
ini_set('error_log', '_LOG_');
define('APP_NAME', 'Ice Framework');
define('FB_URL', 'Ice Framework');
define('TWITTER_URL', 'Ice Framework');
define('CLIENT_NAME', '_CLIENT_');
define('APP_BASE_PATH', '_APP_BASE_PATH_');
define('CLIENT_BASE_PATH', '_CLIENT_BASE_PATH_');
define('BASE_URL','_BASE_URL_');
define('CLIENT_BASE_URL','_CLIENTBASE_URL_');
define('APP_DB', '_APP_DB_');
define('APP_USERNAME', '_APP_USERNAME_');
define('APP_PASSWORD', '_APP_PASSWORD_');
define('APP_HOST', '_APP_HOST_');
define('APP_CON_STR', 'mysqli://'.APP_USERNAME.':'.APP_PASSWORD.'@'.APP_HOST.'/'.APP_DB);
//file upload
define('FILE_TYPES', 'jpg,png,jpeg');
define('MAX_FILE_SIZE_KB', 10 * 1024);
//Home Links
define('HOME_LINK_ADMIN', CLIENT_BASE_URL."?g=admin&n=dashboard&m=admin_Admin");
define('HOME_LINK_OTHERS', CLIENT_BASE_URL."?g=modules&n=dashboard&m=module_My_Account");
```
Now start updating the file.

You can delete the default values and add your company's social media urls.

This is an updated example:

**By default CLIENT\_NAME should be app**

```text
define('APP_NAME', 'Gamonoid - Your Company Name');
define('FB_URL', 'https://facebook.com/yourcompany');
define('TWITTER_URL', 'https://twitter.com/yourhandle');
define('CLIENT_NAME', 'app');
```
Next find out the exact path of your gamonoid installation and url to your gamonoid installation before updating the urls.

Let us assume that the path to gamonoid to be : **/var/www/gamonoid/** and gamonoid url to be [http://your-company-domain.com/gamonoid](http://your-company-domain.com/gamonoid).

Now let's see how we can update the urls.

The updated urls should look like this:

```text
define('APP_BASE_PATH', '/var/www/gamonoid/core/');
define('CLIENT_BASE_PATH', '/var/www/gamonoid/app/');
define('BASE_URL','http://your-company-domain.com/gamonoid/web/');
define('CLIENT_BASE_URL','http://your-company-domain.com/gamonoid/app/');
```

**If you are using windows note the path should be specified with forward slash as shown below.**

```text
define('APP_BASE_PATH', 'C:/xampp/htdocs/gamonoid/core/');
```
Now you can update the database configurations:

```text
define('APP_DB', 'icehrm');
define('APP_USERNAME', 'icehrm_user');
define('APP_PASSWORD', 'icehrm_pwd');
define('APP_HOST', 'localhost');
```

