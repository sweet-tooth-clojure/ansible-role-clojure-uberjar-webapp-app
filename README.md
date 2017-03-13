Clojure Uberjar Webapp: App
=========

This role configures a server to run a standalone java program as a
web server. It:

* Installs packages needed to run a java program (openjdk-8-jre)
* Installs an upstart script to run the program as a service
* Relies on environment variables to configure your program

See https://github.com/sweet-tooth-clojure/ansible-roles for a quick
overview and instructions. See
[_Deploying Your First Clojure App ...From the Shadows_](http://www.braveclojure.com/quests/deploy/)
for an introductory guide to Ansible and in-depth explanation of this
role.

Requirements
------------

None

Role Variables
--------------

I tried to take care to parameterize as much as I could, but to define
defaults such that you're only required to define a couple vars for
everything to work. If you define `clojure_uberjar_webapp_domain`,
then `flyingmachine.clojure-uberjar-webapp-common` will define
`clojure_uberjar_webapp_app_name`, which is used by most of the vars
velow.

For example, if your domain is `foo.bar.com`, the app name will be
`foo-bar-com`. Your java jar will be uploaded to
`/var/www/foo-bar-com/foo-bar-com.jar`. The upstart service will be
named `foo-bar-com`, and you'll find logs under
`/var/log/foo-bar-com/foo-bar-com.log`. I find that this consistency
makes it easier to navigate the filesystem.

There are some references to datomic vars, but those are optional. I
hope to improve the roles such that this role contains no references
to datomic.

| Variable                                      | Description                                                                      |
| --------                                      | -----------                                                                      |
| `clojure_uberjar_webapp_app_user`             | user that owns app-related files                                                 |
| `clojure_uberjar_webapp_app_root`             | directory containging app files like jar, config files                           |
| `clojure_uberjar_webapp_app_http_port`        | gets set as `HTTP_SERVER_PORT` env var when starting jar                         |
| `clojure_uberjar_webapp_app_http_env_path`    | where to put file that exports `HTTP_SERVER_PORT`; gets sourced in upstart       |
| `clojure_uberjar_webapp_app_service_name`     | used by upstart, e.g. `sudo service xyz start`                                   |
| `clojure_uberjar_webapp_app_jar_name`         | name to use when copying jar file to server                                      |
| `clojure_uberjar_webapp_app_env_local_path`   | where to look on local machine for file that sets other env vars for uberjar app |
| `clojure_uberjar_webapp_app_env_path`         | where to save file that sets app env vars; gets sourced in upstart script        |
| `clojure_uberjar_webapp_app_check_local_path` | where to look on local machine for a script template to check the deployment     |
| `clojure_uberjar_webapp_app_command`          | used in the upstart script to start the web app                                  |
| `clojure_uberjar_webapp_datomic_env_path`     | location of file to source for datomic env vars                                  |


Dependencies
------------

* [flyingmachine.clojure-uberjar-webapp-common](https://galaxy.ansible.com/flyingmachine/clojure-uberjar-webapp-common/)
* [flyingmachine.clojure-uberjar-webapp-nginx](https://galaxy.ansible.com/flyingmachine/clojure-uberjar-webapp-nginx/)
*is useful but optional

Example Playbook
----------------

```
---
- hosts: webservers
  become: true
  become_method: sudo
  vars:
    clojure_uberjar_webapp_domain: staging.blahblah.com
  roles:
    - "flyingmachine.clojure-uberjar-webapp-common"
    - "flyingmachine.clojure-uberjar-webapp-app"
    - "flyingmachine.clojure-uberjar-webapp-nginx"
```

GitHub Repo
-------
https://github.com/sweet-tooth-clojure/ansible-role-clojure-uberjar-webapp-app


License
-------

MIT

Author Information
------------------

Daniel Higginbotham

* http://twitter.com/nonrecursive
* http://www.braveclojure.com/
