.. _section-role-cleanup:

Role **cleanup**
================================================================================

Ansible role for convenient bulk filesystem cleanup on all target systems.

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/cleanup>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-cleanup>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-cleanup>`__


Description
--------------------------------------------------------------------------------

Purpose of this role is to enable the administrator to remove arbitrary number
of files.

With the file removal, there is a lurking danger, that the administrator could
accidentally delete essential directories or even the whole system (``rm -rf /``).
There is a built-in safeguard within the task that is handling the file removal,
which will refuse to delete few selected paths (see *forbidden values* below).
This however should be considered only as a really basic protection against
accidental mistakes, but be aware it can be easily bypassed.

.. warning::

    **Always use the file removal tool with caution !!!**


Requirements
--------------------------------------------------------------------------------

This role does not have any special requirements.


Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

No other roles have direct dependency on this role.


Managed files
--------------------------------------------------------------------------------

This role does not directly manage content of any files on target system.


Internal variables
--------------------------------------------------------------------------------

.. envvar:: hm_cleanup__remove_files

    List of files, that MUST NOT be present on target system. Any file/directory
    on this list will be removed from the target host.

    * *Datatype:* ``list of strings``
    * *Default value:* ``empty list``
    * *Forbidden values:* ``["/","/bin","/boot","/lib","/root","/sbin","/usr","/var"]``


Usage and customization
--------------------------------------------------------------------------------

This role is (attempted to be) written according to the `Ansible best practices <https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html>`__. The default implementation should fit most users,
however you may customize it by tweaking default variables and providing custom
templates.


Variable customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most of the usefull variables are defined in ``defaults/main.yml`` file, so they
can be easily overridden almost from `anywhere <https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable>`__.


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


Example Playbook
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers-cleanup]
    localhost

Example content of role playbook file ``playbook.yml``::

    - hosts: servers-cleanup
      remote_user: root
      roles:
        - role: honzamach.cleanup
      tags:
        - role-cleanup

Example usage::

    ansible-playbook -i inventory playbook.yml


License
--------------------------------------------------------------------------------

MIT


Author Information
--------------------------------------------------------------------------------

Honza Mach <honza.mach.ml@gmail.com>
