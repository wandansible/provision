Ansible role: Provision
=======================

Base role for handling machine provisioning.
Handles all the common tasks associated with provisioning
hosts. This includes prompting for a username and password
when required, setting a root password, and upgrading packages
to their latest versions.

Role Variables
--------------

```
ENTRY POINT: main - Base role for handling machine provisioning

        Handles all the common tasks associated with provisioning
        hosts. This includes prompting for a username and password
        when required, setting a root password, and upgrading packages
        to their latest versions.

OPTIONS (= is mandatory):

- provision_full_upgrade
        If true, run apt full-upgrade on provision
        [Default: True]
        type: bool

- provision_ssh_password_authentication
        If true, use password-based SSH authentication
        [Default: False]
        type: bool

- provision_user_keep
        If true, keep the provision user after the host is
        successfully provisioned
        [Default: False]
        type: bool

- provision_user_password
        Password for the provision user, leave this as an empty string
        to be prompted for the password
        [Default: (null)]
        type: str

- provision_user_private_key_file
        Path to the provision user's private SSH key on the host
        running ansible
        [Default: ssh/ansible_ed25519]
        type: str

- provision_user_public_key
        Contents of the provision user's public SSH key
        [Default: (null)]
        type: str

- provision_user_ssh_password
        Password for password-based SSH authentication or when
        provision_ssh_password_authentication = true leave this as an
        empty string to set the password to provision_user_password.
        [Default: (null)]
        type: str

- provision_user_username
        Username for the provision user, set this to an empty string
        to be prompted for the username
        [Default: ansible]
        type: str

- root_password
        Password for the root user
        [Default: (null)]
        type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/provision,main,wandansible.provision
     
Or, by adding the following to `requirements.yml`:

    - name: wandansible.provision
      src: https://github.com/wandansible/provision

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: all
      roles:
         - role: wandansible.provision
           become: true
           vars:
             root_password: "hunter2"
