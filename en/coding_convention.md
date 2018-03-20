# Coding standards

## Basic rules
* This project's coding rules are based on `PSR-1` & `PSR-2`.
  * Reference: http://www.php-fig.org/
* Naming Space and File Name riles are based on `PSR-4`.
* And indent rules are defined in `.editorconfig` file ( 4 space for one indent ). So we strongly use the editor which support editor config.
  * You can refer http://editorconfig.org/ to know about more
* We are using [PHP CS Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) to fix the code.
  * `.php_cs` file is the configuration file for it
* This is the "Rule". Means need to follow and any kind of exceptions will not be allowed such as "I have no time to follow & check".

## Name Convention

There are several type of cases ( snake_case, kebab-case, camelCase and TitleCase )

|Type|Rule|
|:--|:--|
|Table Name|snake_case|
|Column Name|snake_case|
|Variable Name|camel case|
|JSON( include config & API Response Name)|camel case|
|URL|kebab case|
|Class name|TitleCase|

## Method names

* Method of each classes are for "do something". So name of the method must be meaningful. It may named as "Verb" + "Object".
  * Example: `getName`, `parseObject` ...
* Only when objective is really clear from the class name, method with only "Verb" are allowed.

## Protected property and getter

* If you need to reveal object internal properties but don't want to be changeable, you every time need to make it as protected and provide getter.

## Constant names

* Constant name should be upper cases with underscores.
  * Example:  `TYPE_STAFF`, `STATUS_APPROVED` ...

## PHP docs

* Need to write PHP docs describe input/output params and types on the

## Type Hints

* We are using PHP 7.1, so we should use type hints to fail fast.
