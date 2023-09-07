## Magento 2 MySQL Cluster
# Installation Instructions

1. composer require `MST/m2-mysql-cluster`
2. add configuration into app/etc/env.php

Navigate to section `db -> connection -> default`

add a new section in default:

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

Add there as many slave servers as you need.

3. `bin/magento deploy:mode:set production`
 
