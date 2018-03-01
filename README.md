webappdeploy_role
=================

Role to build out a web application on a server:
1. Creates user/group for application.
2. Downloads source code for app.
3. Makes any tweaks as described by the `app_tasks` variable.

See the `tests/test.yml` for usage details.

Requirements
------------

* [application_role](https://github.com/buzzbombnc/application_role)

Role Variables
--------------

The following variables may be provided:

| Variable         | Required | Description                                                    |
|:-----------------|:--------:|:---------------------------------------------------------------|
| server_name      | true     | The primary domain name of the server.                         |
| server_admin     | true     | The primary admin's email address for the server.              |
| alt_server_names | false    | A list of alternate server names.                              |
| ssl_server       | false    | A boolean to determine if the server is SSL or not.            |
| app_git_repo     | true     | Git repository to deploy from.                                 |
| app_git_ref      | false    | Git reference to use.  Defaults to 'HEAD'.                     |
| app_tasks        | false    | a list of application tasks to include from the `apptasks` dir.|

Note that if your `app_git_repo` utilizes SSH, you must have a key available for connection.

If you're using an SSH agent for connecting to your remote host and the git+SSH repository, you may need to add additional configuration to the Ansible inventory file:

    ansible_ssh_extra_args="-o ForwardAgent=yes"

Variables required by `application_role`:
* app_user

The follow variables are defined in defaults/main.yml:

| Variable         | Required | Description                                                    |
|:-----------------|:--------:|:---------------------------------------------------------------|
| server_base_dir  | false    | The base directory for websites.  Default: /srv/httpd          |

See documentation for other optional arguements.

Apptasks
--------

* virtualenv

| Variable                 | Required | Description                                        |
|:-------------------------|:--------:|:---------------------------------------------------|
| virtualenv_site_packages | false    | Include site pkgs in virtualenv?  Default is true. |

* environment

Builds an `environment` file in the current deployment directory.  Will get populated with the full path to the 
shared directory and the version of the git repo.

In addition:

| Variable     | Required | Description                                        |
|:-------------|:--------:|:---------------------------------------------------|
| app_env_vars | false    | A dictionary of environment key-values.            |

* django

  + Performs checks, tests, and database migrations.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

MIT License

Copyright (c) 2018 Ken Treadway

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
