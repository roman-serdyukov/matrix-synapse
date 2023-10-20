
Развертывание matrix-synapse server + synapse-admin + element-web
=========

Ansible role состоит из следующих групп tasks:
- Установка дополнительных пакетов - install_other.yml
- Установка и настройка postgresql - install_postgresql.yml
- Установка и настройка matrix-synapse - install_matrix_synapse.yml
- Установка и настройка nginx - install_nginx.yml
- Установка и настройка coturn - install_coturn.yml
- Установка и настройка element web - install_element_web.yml
- Установка и настройка synapse-admin - install_synapse_admin.yml

Включить/отключить нужный блок можно раскоментировав/закоментировав его в tasks/main.yml.

В templates/ лежат файлы конфигураций:
- homeserver.yaml.j2 - конфигурация matrix-synapse
- matrix.conf.j2, matrix-admin.conf.j2, element.conf.j2 - конфигурация сайтов для nginx
- config.json.j2 - конфигурация element-web
- turnserver.conf.j2 - конфигурация coturn
- docker-compose.yml.j2 - конфигурация Docker Compose для synapse-admin

Requirements
------------

- Разработана с помощью ansible 2.13.3
- Работоспособность протестирована на Ubuntu 20.04 и Ubuntu 22.04

Role Variables
--------------

- other_pack - список дополнительных пакетов для установки
- nginx_pack - список пакетов для установки и настройки web сервера
- repo_url - адрес дистрибутива matrix-synapse
- key_folder - путь к папке для добавления ключа репозиторию
- domain_zones - список зон для web сервера
- matrix - зона для matrix-synapse
- synapse-admin - зона для synapse-admin
- element - зона для element
- conf_files - список файлов конфигурации для nginx
- git_repo: git репозиторий synapse-admin

Отдельно в group_vars вынес следующие переменные:
- email_address - для запроса сертификата certbot
- db_name - имя базы данных postgresql
- db_user - имя пользователя базы данных postgresql
- db_pass - пароль к базе данных postgresql
- matrix_admin_user - имя пользователя админимтратора matrix-synapse
- matrix_admin_pass - пароль администратора matrix-synapse
- my_domain - доменное имя
  
Example Playbook
----------------

```
- name: Install apps server
  hosts: {{ your_servers }}
  roles:
    - matrix-synapse-role.yml
```

License
-------
Роль создана по [инструкции на Habr-е от Chiudik](https://habr.com/ru/articles/739606/)

MIT

Author Information
------------------

Сердюков Роман
reserdukov@gmail.com