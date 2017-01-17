Clojure Uberjar Webapp: App
=========

Run an uberjar web app

Requirements
------------

None

Role Variables
--------------

| Variable                                    | Description                                                                      |
| --------                                    | -----------                                                                      |
| `clojure_uberjar_webapp_app_user`           | user that owns app-related files                                                 |
| `clojure_uberjar_webapp_app_root`           | directory containging app files like jar, config files                           |
| `clojure_uberjar_webapp_app_http_port`      | gets set as `HTTP_SERVER_PORT` env var when starting jar                         |
| `clojure_uberjar_webapp_app_http_env_path`  | path to file that exports `HTTP_SERVER_PORT`                                     |
| `clojure_uberjar_webapp_app_service_name`   | used by upstart, e.g. `sudo service xyz start`                                   |
| `clojure_uberjar_webapp_app_jar_name`       | name to use when copying jar file to server                                      |
| `clojure_uberjar_webapp_app_env_local_path` | where to look on local machine for file that sets other env vars for uberjar app |
| `clojure_uberjar_webapp_app_env_path`       | where to save file that sets app env vars                                        |
| `clojure_uberjar_webapp_app_command`        | used in the upstart script to start the web app                                  |
| `clojure_uberjar_webapp_datomic_env_path`   | location of file to source for datomic env vars                                                                                 |


Dependencies
------------

Requires `flyingmachine.clojure-uberjar-webapp-common`. Setting `clojure_uberjar_webapp_domain` will allow everything else to work.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

MIT

Author Information
------------------

Daniel Higginbotham

* http://twitter.com/nonrecursive
* http://www.braveclojure.com/
