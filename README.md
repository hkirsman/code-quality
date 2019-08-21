# Code Quality

This composer package will provide some basic code quality checks before commiting code by using
https://github.com/phpro/grumphp.

It checks only modified files or new files.

## Checks performed

This repository currently has following checks:

* PHP Drupal Coding Standards
* PHP 7.3 Compatibility
* PHP syntax

## Pre-requisites

* Composer

## Installation

This needs to be done only once either while creating a project or enabling code checks in existing project.

`composer require hkirsman/code-quality:dev-master --dev`

Add grumphp.yml to same location as composer.json:
````yml
parameters:
  tasks:
    php_compatibility: ~
    php_check_syntax:
      ignore_patterns: []
      triggered_by:
        - php
        - module
        - inc
    phpcs:
      standard:
        - vendor/hkirsman/code-quality/phpcs.xml
      ignore_patterns:
        - cfg/
        - libraries/
      triggered_by:
        - php
        - module
        - inc
  extensions:
    - hkirsman\PhpCompatibilityTask\ExtensionLoader
    - hkirsman\PhpCheckSyntaxTask\ExtensionLoader
````

## Custom PHP CodeSniffer rules

If you need to customize the rules for PHP CodeSniffer then drop in phpcs.xml in the same
folder as composer.json and configure grumphp.yml:
````yml
parameters:
  tasks:
    phpcs:
      standard:
        - phpcs.xml
````

## Usage

The pre-commit hook will be automatically run upon executing `git commit`.

The code scanning can be avoided by `git commit --no-verify`.
