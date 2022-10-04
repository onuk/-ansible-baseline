ansible-baseline
=========

This base role configures some parameters and installs base tools in the system.

Requirements
------------

Ansible 2.10.8

Role Variables
--------------

|Variable|Description|
|--------|-----------|
| locales | Configures the system locales for example: en_US.UTF-8 or uk_UA.UTF-8 |
| timezone_name | Configures the system timezone for example: Europe/Berlin or Europe/Kyiv |
| sysctl_config | The variable which helps to manage sysctl configuration in a system |
| sysctl_config_location | The variable set path to /etc/sysctl.conf |
| ulimit_config | The variable which helps to manage ulimit configuration in a system |
| ulimit_config_location | The variable set path to /etc/security/limits.conf |
| packages | Overrides the list of the base packages to install in system |


Dependencies
------------
N/A

Example of how to use the role
----------------

    - hosts: localhost
      become: true
      gather_facts: yes
      
      vars:
        locales:
            - en_US.UTF-8
            - uk_UA.UTF-8
        timezone_name: Europe/Berlin
        sysctl_config:
          kernel.sysrq: 0
          kernel.core_uses_pid: 1
          fs.file-max: 65535
        sysctl_config_location: /etc/sysctl.conf
        ulimit_config: 
            - domain: '*'
              type: 'soft'
              item: 'nproc'
              value: '65535'
            - domain: '*'
              type: 'hard'
              item: 'nproc'
              value: '65535'
        ulimit_config_location: /etc/security/limits.conf
        packages:
            - vim
            - git
            - tmux
            - htop
            - curl
            - wget
            - sudo
            - strace
            - iftop
            - jnettop
            - iotop
            - nload
            - ioping
            - tree
            - ncdu
    roles:
      - role: ansible-baseline

License
-------

MIT

Author Information
------------------
[Yurii Onuk](https://onuk.org.ua)
