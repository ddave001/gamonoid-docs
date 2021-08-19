---
description: >-
  This section covers the steps needed to create a simple extension.
---

# Getting started

## Introduction

By using Gamonoid, developers can create personalized extensions. This document will guide you on how to create a simple extension to list down your tasks.

* Create the directory `gamonoidapp/extensions` if it doesn't already exists.
* Create a directory named `tasks` inside `gamonoidapp/extensions`.

### Adding the meta.json file

```text
📦extensions
 ┣ 📂tasks
 ┃ ┗ 📜meta.json
 ┗
```

The meta.json file for the tasks extension is given below:

```javascript
{
    "label": "My Tasks",
    "menu": ["Tasks", "fa-list"],
    "icon": "fa-tasks",
    "user_levels": [
        "Admin",
        "Manager",
        "User"
    ],
    "model_namespace": "\\Tasks\\Model",
    "manager": "\\Tasks\\Extension",
    "headless": false
}
```
* **label** - The name of the item that will be created under the main menu.
* **menu** - The name of the main menu and the icon for the main menu.
* **user_levels** - The user levels that can use and see the extension.
* **model_namespace** - The namespace which will hold the database model classes.
* **manager** - The main class which controls the extension.
* **headless** - If headless is set to true there will be no UI visibility.

### Adding the extension manager class

Create Extension.php inside `gamonoidapp/extensions/tasks/src/Tasks`

```text
 📦extensions
 ┣ 📂tasks
 ┃ ┣ 📂src
 ┃ ┃ ┗ 📂Tasks
 ┃ ┃ ┃ ┗ 📜Extension.php
 ┃ ┗ 📜meta.json
 ┗ 
```
The Extension.php file should look like:

```php
<?php
namespace Tasks;

use Classes\IceExtension;

class Extension extends IceExtension
{

    public function install() {

    }

    public function uninstall() {

    }

    public function setupModuleClassDefinitions()
    {

    }

    public function setupRestEndPoints()
    {

    }
}
```
### Adding Extension include file

{% hint style="warning" %}
Every extension must have an include file. Thie include file must have the same name as the extension.
{% endhint %}

The include file for the tasks extension will be tasks.php and the directory should look like this:

```text
📦extensions
 ┣ 📂tasks
 ┃ ┣ 📂src
 ┃ ┃ ┗ 📂Tasks
 ┃ ┃ ┃ ┗ 📜Extension.php
 ┃ ┣ 📜meta.json
 ┃ ┗ 📜tasks.php
 ┗ 
 ```

 **tasks.php** should look like this:

```text
<?php

require_once __DIR__.'/src/Tasks/Extension.php';
```
### Adding the view file

{% hint style="warning" %}
Every extension must have a view file if headless mode is set to false.
{% endhint %}

The view file should be in `extensions/tasks/web/index.php`

```text
📦extensions
 ┣ 📂tasks
 ┃ ┣ 📂src
 ┃ ┃ ┗ 📂Tasks
 ┃ ┃ ┃ ┗ 📜Extension.php
 ┃ ┣ 📂web
 ┃ ┃ ┗ 📜index.php
 ┃ ┣ 📜meta.json
 ┃ ┗ 📜tasks.php
 ┗
```
**index.php**

```php
<?php
$user = \Classes\BaseService::getInstance()->getCurrentUser();
echo "Welcome ".$user->username;
```
## Load your first extension

Refresh gamonoid and you should see the **My tasks** extension in the menu.

![](../.gitbook/images/gamonoidapp-tasks-extension.PNG)