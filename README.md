# ansible-django-app

This Ansible role builds and deploys a Django application in a virtualenv, with wsgi and Apache.

### Role variables

* ``app_name``:
* ``repo``:    
* ``branch``: 
* ``domain``:
* ``DJANGO_APP_SETTINGS``: A list of key/value pairs that describe the build-specific application settings, and get exported in the ``build_settings.py`` file. This file will later be symlinked in the application's source code, and needs to be imported by the application's ``settings.py`` file.
   
            DJANGO_APP_SETTINGS:
             - MYSQL_USERNAME: db_user
             - MYSQL_PASSWORD: password

    or

            DJANGO_APP_SETTINGS: {MYSQL_USERNAME: "db_user", MYSQL_PASSWORD: "password"}

### Requirements

* A Debian machine running an SSH server and a user account with sudo permission
* logrotate
* Apache2
* mod_wsgi 
* Django application's settings.py needs to import the ``build_settings.py`` file    

### Example

    playbook.yml
    ---
    - hosts: 
      - all
  
      remote_user: smartpr

      roles:
       - { role: "ansible-build-django-app", 
           app_name: smartpr_api, 
           repo: "git@github.com:smartpr/smartpr-api.git" , 
           branch: "master",
           DJANGO_APP_SETTINGS: [ MYSQL_USERNAME: "db_user", 
                              MYSQL_PASSWORD: "password"]}                         


Invoke playbook

    ansible-playbook playbook.yml                              
