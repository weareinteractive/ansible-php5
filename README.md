# Ansible weareinteractive.php5 role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-php5.svg)](https://travis-ci.org/weareinteractive/ansible-php5)
[![Galaxy](https://img.shields.io/badge/galaxy-weareinteractive.php5-blue.svg)](https://galaxy.ansible.com/weareinteractive/php5)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-php5.svg)](https://github.com/weareinteractive/ansible-php5)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-php5.svg)](https://github.com/weareinteractive/ansible-php5)

> `weareinteractive.php5` is an [Ansible](http://www.ansible.com) role which:
>
> * installs php5
> * configures php5
> * installs xtra packages
> * installs pear packages
> * installs pecl packages
> * configures logrotate

## Installation

Using `ansible-galaxy`:

```shell
$ ansible-galaxy install weareinteractive.php5
```

Using `requirements.yml`:

```yaml
- src: weareinteractive.php5
```

Using `git`:

```shell
$ git clone https://github.com/weareinteractive/ansible-php5.git weareinteractive.php5
```

## Dependencies

* Ansible >= 2.4
**Note:**

> Since Ansible Galaxy supports [organization](https://www.ansible.com/blog/ansible-galaxy-2-release) now, this role has moved from `franklinkim.php5` to `weareinteractive.php5`!

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---
# For more information about default variables see:
# http://www.ansibleworks.com/docs/playbooks_variables.html#id26
#
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

# User
php5_user: www-data
# apt packages (versions)
php5_packages:
  - php5
  - php5-dev
  - php5-cli
  - php-pear
# error log path
php5_log_path: /var/log/php5
# cli config settings
php5_cli_config: []
# fpm config settings
php5_fpm_config: []
# apache config settings
php5_apache2_config: []
# list of pear packages to install
php5_pear_packages: []
# list of pecl packages to install
php5_pecl_packages: []
# list of php modules to install & configure
php5_modules: []

```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

```yaml
---

- name: restart apache2
  service: name=apache2 state=restarted

- name: restart php5-fpm
  service: name=php5-fpm state=restarted

```


## Usage

This is an example playbook:

```yaml
---

- hosts: all
  become: yes
  roles:
    - weareinteractive.apt
    - weareinteractive.php5
  vars:
    php5_cli_config:
      - { section: PHP, option: default_charset, value: UTF-8 }
      - { section: Date, option: date.timezone, value: Europe/Berlin }
      - { section: PHP, option: error_log, value: /var/log/php5/error-cli.log }
    php5_pear_packages:
      - { name: Mail, config: [] }
    php5_pecl_packages:
      - { name: hrtime, config: [] }

```


## Testing

```shell
$ git clone https://github.com/weareinteractive/ansible-php5.git
$ cd ansible-php5
$ make test
```

## Contributing
In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

*Note: To update the `README.md` file please install and run `ansible-role`:*

```shell
$ gem install ansible-role
$ ansible-role docgen
```

## License
Copyright (c) We Are Interactive under the MIT license.
