.. _section-cookbook-roles-cleanup:

Host cleanup
================================================================================


.. _section-cookbook-roles-cleanup-cleanuppkgs:

Removing packages from all target hosts
--------------------------------------------------------------------------------

To remove arbitrary number of APT packages from all managed systems just use
role :ref:`cleanup <section-role-cleanup>`. Use following variable inside of your
``inventory/group_vars/all/vars.yml`` file::

    hm_cleanup__remove_packages:
        debian:
            apt:
              - first-package
              - second-package
              - ...

Then execute the role::

    apbf role_cleanup.yml


.. _section-cookbook-roles-cleanup-cleanupfiles:

Removing files from all target hosts
--------------------------------------------------------------------------------

To remove arbitrary number of files and/or directories from all managed systems
just use role :ref:`cleanup <section-role-cleanup>`. Use following variable inside
of your ``inventory/group_vars/all/vars.yml`` file::

    hm_cleanup__remove_files:
        - "/etc/file/to/be/removed.txt"
        - "/var/to/discard"

Then execute the role::

    apbf role_cleanup.yml
