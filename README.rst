ansible-role-weirdo-common
--------------------------
This role centralizes common tasks used across
different roles for the WeIRDO_ project.

.. _WeIRDO: https://github.com/redhat-openstack/weirdo

Role variables
~~~~~~~~~~~~~~

For default values, see `defaults/main.yml`_

* ``base_packages``: A list of packages to install by default
* ``debug_packages``: A list of packages meant for debug purposes to install by default
* ``job_name``: Name of the job (defaults to Jenkins-provided environment variable)
* ``build_numer``: Build number of the job (defaults to Jenkins-provided environment variable)
* ``log_root``: Root directory where the debug logs will be sent to
* ``log_destination``: Subdirectory where the debug logs will be sent to
* ``log_paths``: Log paths to recover by default
* ``debug_commands``: Hash of debug commands that will be run and output to log files

.. _defaults/main.yml: https://github.com/redhat-openstack/ansible-role-weirdo-common/blob/master/defaults/main.yml

Included tasks
~~~~~~~~~~~~~~

* ``logs``: Recovers basic logs by default
* ``packages``: Ensures required dependencies are installed
* ``setup``: Sets up log directory, configures sysstat
* ``rescue``: Task that gets included in rescue blocks to notify different handlers

Dependencies
~~~~~~~~~~~~

`ansible-role-ci-centos`_ to be installed as ``ci-centos`` when the role ci-centos is used to provision nodes.

.. _ansible-role-ci-centos: https://github.com/redhat-openstack/ansible-role-ci-centos

Example playbook
~~~~~~~~~~~~~~~~

.. code-block:: yaml

    - name: Run packstack scenario001 tests
      hosts: openstack_nodes
      force_handlers: True
      roles:
        - role: "common"
        - { role: "packstack", test: "scenario001" }
        - { role: "common", action: "logs" }
