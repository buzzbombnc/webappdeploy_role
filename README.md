webappdeploy_role
=================

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

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

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
