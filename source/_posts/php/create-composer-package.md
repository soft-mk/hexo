---
title: 创建 composer 包
date: 2021-10-22 17:34:22

categories:
- PHP

tags:
- PHP
- 开发
---

- 创建一个 github 项目
- 将项目克隆到本地
- 进入项目并初始化 composer
	```php
	//初始化
	$ composer init
	  Welcome to the Composer config generator
	This command will guide you through creating your composer.json config.
	
	//项目命名空间 matching: [a-z0-9_.-]+/[a-z0-9_.-]+
	Package name (<vendor>/<name>) [administrator/php]: mk2920/php
	//项目描述
	Description []:   test composer package
	Author [MK <adai.kimi@gmail.com>, n to skip]:
	//最低稳定版本，stable, RC, beta, alpha, dev
	Minimum Stability []: dev
	//项目类型
	Package Type (e.g. library, project, metapackage, composer-plugin) []: library
	//授权类型
	License []:
	
	Define your dependencies.
	//项目依赖
	Would you like to define your dependencies (require) interactively [yes]?
	Search for a package: php
	Enter the version constraint to require (or leave blank to use the latest version): 7.4
	Search for a package:
	Would you like to define your dev dependencies (require-dev) interactively [yes]?
	Search for a package:
	Add PSR-4 autoload mapping? Maps namespace "Mk2920\Php" to the entered relative path. [src/, n to skip]:
	
	{
	    "name": "mk2920/php",
	    "description": "test composer package",
	    "require": {
	        "php": "7.3"
	    },
	    "autoload": {
	        "psr-4": {
	            "Mk2920\\Php\\": "src/"
	        }
	    },
	    "authors": [
	        {
	            "name": "MK",
	            "email": "adai.kimi@gmail.com"
	        }
	    ],
	    "minimum-stability": "dev"
	}
	//是否生成 composer.json
	Do you confirm generation [yes]?
	Would you like the vendor directory added to your .gitignore [yes]?
	Would you like to install dependencies now [yes]?
	Loading composer repositories with package information
	Updating dependencies

	PSR-4 autoloading configured. Use "namespace Mk2920\Php;" in src/
	Include the Composer autoloader with: require 'vendor/autoload.php';

	```
- 开发包
- 上传代码到 git
- 
	
