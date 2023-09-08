## Magento 2 MySQL Cluster

Reworking a fork for PHP 8.2 & Magento 2.4.6-p2 - with MariaDB Replication.

# Todo
Have reworked all the code, re-created from the 2.4.6-p2 Framework Adapter/Pdo/Mysql.php
It does connect to all databased, not sure how this was initially meant to be set up by Original owner. But with Maria DB replication - slave is readonly. 

 - Need to rework and tighten what situation the slave(s) can be used.
 - Remove debug logger when done.

# Done
- Rework and combine original to updated Magento Framework Pdo/Mysql.php
- Rework the slave config - as old way wasn't working due to changes in the way Magento handles and retreives information from the env.php file.
- Updated DSN creation.

# Installation Instructions

1. composer require `mst/m2-mysql-cluster`
2. add configuration into app/etc/env.php

Navigate to section `db -> connection -> default`

add a new section in default:
```
'connection' => [
            'default' => [
                'host' => '',
                'dbname' => '',
                'username' => '',
                'password' => '',
                'model' => 'mysql4',
                'engine' => 'innodb',
                'initStatements' => 'SET NAMES utf8;',
                'active' => '1',
                'driver_options' => [
                        1014 => false
                ],
                'slave' => [
                    [
                        'host' => '',
                        'dbname' => '',
                        'username' => '',
                        'password' => '',
                        'model' => 'mysql4',
                        'engine' => 'innodb',
                        'initStatements' => 'SET NAMES utf8;',
                        'active' => '1',
                        'driver_options' => [
                            1014 => false
                        ]
                    ]
                ]
            ]
        ]
```
        
Add as many slave servers as you need in to the slave array..

3. `bin/magento deploy:mode:set production`
 
