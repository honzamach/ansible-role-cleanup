.. _section-role-cleanup:

Role **cleanup**
================================================================================

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/cleanup>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-cleanup>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-cleanup>`__

Purpose of this role is to enable the administrator to remove arbitrary number
of files and cleanup target systems.

With the file removal, there is a lurking danger, that the administrator could
accidentally delete essential directories or even the whole system (``rm -rf /``).
There is a built-in safeguard within the role that is handling the file removal,
which will refuse to delete few selected paths (see *forbidden values* below).
This however should be considered only as a really basic protection against
accidental mistakes, but be aware it can be easily bypassed.

.. warning::

    **Always use the file removal tool with caution !!!**

**Table of Contents:**

* :ref:`section-role-cleanup-installation`
* :ref:`section-role-cleanup-dependencies`
* :ref:`section-role-cleanup-usage`
* :ref:`section-role-cleanup-variables`
* :ref:`section-role-cleanup-files`
* :ref:`section-role-cleanup-author`

This role is part of the `MSMS <https://github.com/honzamach/msms>`__ package.
Some common features are documented in its :ref:`manual <section-manual>`.


.. _section-role-cleanup-installation:

Installation
--------------------------------------------------------------------------------

To install the role `honzamach.cleanup <https://galaxy.ansible.com/honzamach/cleanup>`__
from `Ansible Galaxy <https://galaxy.ansible.com/>`__ please use variation of
following command::

    ansible-galaxy install honzamach.cleanup

To install the role directly from `GitHub <https://github.com>`__ by cloning the
`ansible-role-cleanup <https://github.com/honzamach/ansible-role-cleanup>`__
repository please use variation of following command::

    git clone https://github.com/honzamach/ansible-role-cleanup.git honzamach.cleanup

Currently the advantage of using direct Git cloning is the ability to easily update
the role when new version comes out.


.. _section-role-cleanup-dependencies:

Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

No other roles have dependency on this role.


.. _section-role-cleanup-usage:

Usage
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers_cleanup]
    your-server

Example content of role playbook file ``role_playbook.yml``::

    - hosts: servers_cleanup
      remote_user: root
      roles:
        - role: honzamach.cleanup
      tags:
        - role-cleanup

Example usage::

    # Run everything:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml

    # Do not remove packages from the APT cache:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml --extra-vars '{"hm_cleanup__autoclean":false}'

    # Do not uninstall now unnecessary packages:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml --extra-vars '{"hm_cleanup__autoremove":false}'


.. _section-role-cleanup-variables:

Configuration variables
--------------------------------------------------------------------------------


Internal role variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. envvar:: hm_cleanup__autoclean

    Remove useless packages from the local APT cache.

    * *Datatype:* ``bool``
    * *Default:* ``true``

.. envvar:: hm_cleanup__autoremove

    Removing dependencies that are no longer required (automatically installed packages).

    * *Datatype:* ``bool``
    * *Default:* ``true``

.. envvar:: hm_cleanup__remove_files

    List of files, that MUST NOT be present on target system. Any file/directory
    on this list will be removed from the target host.

    * *Datatype:* ``list of strings``
    * *Default:* ``empty list``
    * *Forbidden values:* ``["/","/bin","/boot","/lib","/root","/sbin","/usr","/var"]``


.. _section-role-cleanup-files:

Managed files
--------------------------------------------------------------------------------

This role does not manage content of any files on target system.


.. _section-role-cleanup-author:

Author and license
--------------------------------------------------------------------------------

| *Copyright:* (C) since 2019 Honza Mach <honza.mach.ml@gmail.com>
| *Author:* Honza Mach <honza.mach.ml@gmail.com>
| Use of this role is governed by the MIT license, see LICENSE file.
|
