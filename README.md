# Ansible PHP5 Role

[![Build Status](https://travis-ci.org/weareinteractive/ansible-php5.png?branch=master)](https://travis-ci.org/weareinteractive/ansible-php5)
[![Stories in Ready](https://badge.waffle.io/weareinteractive/ansible-php5.svg?label=ready&title=Ready)](http://waffle.io/weareinteractive/ansible-php5)

> `php5` is an [ansible](http://www.ansible.com) role which:
>
> * installs php5
> * configures php5
> * installs xtra packages
> * installs pear packages
> * installs pecl packages

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.php5
```

Using `requirements.yml`:

```
- src: franklinkim.php5
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-php5.git
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# php5_packages:
#   - php5-gd
#   - php5-dev
# php5_cli_config:
#   - { section: PHP, option: default_charset, value: UTF-8 }
# php5_apache2_config:
#   - { section: PHP, option: default_charset, value: UTF-8 }
# php5_modules:
#  - { name: gd, config: [] }
#  - { name: curl, config: [] }
#  - { name: tidy, config: [] }
#  - { name: mysql, config: [] }
#  - { name: mcrypt, config: [] }
#  - { name: xmlrpc, config: [] }
#  - { name: xdebug, config: [] }
#  - { name: imagick, config: [] }
#  - { name: mail, type: 'php', config: [] }
#  - { name: mail-mime, type: 'php', config: [] }
# php5_pear_packages:
#  - Mail_IMAPv2
# php5_pecl_packages:
#  - { name: yaml, config: [] }
#  - { name: mailparse, config: [] }

# apt packages
php5_packages:
  - php5
  - php5-dev
  - php5-cli
  - php-pear
# cli config settings
php5_cli_config: []
# cli config settings
php5_apache2_config: []
# list of pear packages to install
php5_pear_packages: []
# list of pecl packages to install
php5_pecl_packages: []
# list of php modules to install & configure
php5_modules: []
```

## Example playbook

```
- hosts: all
  roles:
    - franklinkim.apt
    - franklinkim.php5
  vars:
    apt_repositories:
      - 'ppa:ondrej/php5'
    php5_cli_config:
      - { section: PHP, option: default_charset, value: UTF-8 }
      - { section: Date, option: date.timezone, value: Europe/Berlin }
      - { section: PHP, option: error_log, value: /var/log/php5/error-cli.log }
```

## Notes

You can use `franklinkim.apt` to add a repository to get the latest `php5`:

```
apt_repositories:
  - 'ppa:ondrej/php5'
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-php5.git
$ cd ansible-php5
$ vagrant up
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) We Are Interactive under the MIT license.
