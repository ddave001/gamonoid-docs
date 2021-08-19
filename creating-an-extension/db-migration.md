---
description: >-
  This section covers the steps needed to add a database migration.
---

# Adding a database migration

## Introduction
Migrations can be used to make changes to the gamonoid database. Once you have successfully installed your extension on gamonoid, you can use migrations to make changes to the gamonoid database.

### Adding a simple migration

**Migration.php** should be in `extensions/tasks/src/Tasks`

```text
📦extensions
 ┣ 📂tasks
 ┃ ┣ 📂src
 ┃ ┃ ┗ 📂Tasks
 ┃ ┃ ┃ ┣ 📜Extension.php
 ┃ ┃ ┃ ┗ 📜Migration.php
 ┃ ┣ 📂web
 ┃ ┃ ┗ 📜index.php
 ┃ ┣ 📜meta.json
 ┃ ┗ 📜tasks.php
 ┗ 
 ```

 **Migration.php** should look like:

 ```php
<?php
namespace Tasks;

use Classes\Migration\AbstractMigration;

class Migration extends AbstractMigration
{
    public function up()
    {
        $sql = <<<'SQL'
create table `Tasks` (
    `id` bigint(20) NOT NULL AUTO_INCREMENT,
    `employee` bigint(20) NULL,
    `name` varchar(250) NOT NULL,
    `description` TEXT NULL,
    `attachment` varchar(100) NULL,
    `created` DATETIME default NULL,
    `updated` DATETIME default NULL,
    primary key  (`id`),
    CONSTRAINT `Fk_EmployeeTasks_Employees` FOREIGN KEY (`employee`) REFERENCES `Employees` (`id`) ON DELETE CASCADE ON UPDATE CASCADE
) engine=innodb default charset=utf8;
SQL;
        return $this->executeQuery($sql);
    }

    public function down()
    {
        $sql = <<<'SQL'
DROP TABLE IF EXISTS `Tasks`; 
SQL;
        return $this->executeQuery($sql);
    }
}
```
The above migration will create a table named **Tasks** in the gamonoid database.

**If you want to make changes to the migration make sure the changes are applied manually because the migration will be executed only on the first time the extension is enabled** 

### Executing the migration when installing the extension

Update the **Extension.php** file to execute the migration when the extension is activated for the first time.

```php
<?php
namespace Tasks;

use Classes\IceExtension;

class Extension extends IceExtension
{

    public function install() {
        $migration = new Migration();
        return $migration->up();
    }

    public function uninstall() {
        $migration = new Migration();
        return $migration->down();
    }

    public function setupModuleClassDefinitions()
    {

    }

    public function setupRestEndPoints()
    {

    }
}
```
### Updating the extension include file

The **tasks.php** file should be updated as follows:

```text
<?php

require_once __DIR__.'/src/Tasks/Extension.php';
require_once __DIR__.'/src/Tasks/Migration.php';
```
{% hint style="warning" %}
The migration will not get executed because the extension is already active. For the migration to be executed we have to remove it from the Modules table manually. 
{% endhint %}

Select your gamonoid database and run the below sql query to remove `tasks` from the Modules table manually.

```sql
$> DELETE from Modules where name = 'tasks' and mod_group = 'extension';
```
{% hint style="success" %}
Reload the page and a new Tasks table will be created in your gamonoid database.
{% endhint %}



