# Ansible for PHP with STA project

## Proposal

We created this project as a shadow infra for [Ansible](https://docs.ansible.com/ansible/latest/index.html) to automate server infrastructure setup.

Ansible is a configuration management tool that facilitates the task of setting up and maintaining remote servers.
Ansible doesn’t require any special software to be installed on the nodes that will be managed with this tool.
A control machine is set up with the Ansible software, which then communicates with the nodes via standard SSH.

[Here are some tips for making the most of Ansible and Ansible playbooks.](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html#best-practices)


## Initialize machines

> [!WARNING]
> COMMENT OUT ansible.cfg ssh_connection BEFORE RUNNING THIS


To initialize your machines, you need a `yml` file with all admins you want to add.
An admin user has do have a `name`, `GA_file` is the absolute path to it's `.google_authenticator` file and the public keys are defined at `pubkeys`.

The format looks like this, but there is also an example at `etc/admins.yml`:

```yml
admins:
  - name: rocko
    GA_file: /home/rocko/.google_authenticator
    pubkeys:
      - ssh-rsa abcxyz rocko.artischocko@mail.com
      - ssh-ed25519 abcxyz artischocko@rocko.ie
```

You can add several publick keys, but you don't have to.
Once you have set this up, you can run the playbook to intialise _all_ machines.
This means: jumphosts, rsync and the services where the properties live on.

```sh
ansible-playbook initialize.yml --extra-vars "@/path/to/admins.yml"
```

It does the following:
  1. Define all admin users (name, pubkey, Google Authenticator file)
  2. Disable root login
  3. Google Auth set up
  4. Set up firewall rules to only log in via jump host IPs
  

## Using Ansible

> [!WARNING]
> WE NEED A WAY TO DO THIS BETTER:
> COMMENT IN ansible.cfg ssh_connection BEFORE RUNNING THIS
> 
Ansible organises system administration operations into a hierarchy of playbooks containing roles containing tasks.

To run any playbook, we first have to establish an SSH connection to one of the jumphosts:

```shell
bin/auth-jump0
```

This creates an SSH control channel to jumphost0 that will remain valid for 4 hours. Re-run this when connections start failing after 4 hours.

There is a corresponding `bin/auth-jump1`.

Then you can run any playbook like this:

```shell
ansible-playbook playbook.yml
```

If you have more than one inventory (say one to try things out with and a live one), you can overwrite the default inventory of `inventory/php` (set in `ansible.cfg`) like so: `ansible-playbook -i inventory/other ...`

> [!IMPORTANT]
> Before you start, you have to create a vault password. This can be anything.
> See [the ansible user guide](https://docs.ansible.com/ansible/2.8/user_guide/vault.html) for details.


## Set up services

> [!IMPORTANT]
> Before you run this, you should modify the domain names at `inventory/php/group_vars/service.yml`
>

If you wanna read more about the services, please do so at our [Properties readme](Properties.md).
To set them up, run:

- rsync: `ansible-playbook initRsync.yml`
- downloads: `ansible-playbook initServiceDownloads.yml`
- wiki: `ansible-playbook initServiceWiki.yml`
- museum: `ansible-playbook initServiceMuseum.yml`
- main: `ansible-playbook initServiceMain.yml`

Now you are ready to go! :tada:

> [!TIP]
> There is a subset of Utility Tasks at [Tasks.md](Tasks.md).
> 


# Additional tasks

## Using encrypted vars

Edit the all.yml file:

```shell
EDITOR=nano ansible-vault edit inventory/php/group_vars/all.yml
```

You will be prompted for your vault password.

Further details on encryption can be found in [ansible documentation](https://docs.ansible.com/ansible/latest/vault_guide/vault_encrypting_content.html).


## Changing the Jumphost

By default, jumphost0 is used, to change this, you have to copy your `ansible.cfg` to `local.ansible.cfg` (which is .gitignored) and set the shell environment variable `ANSIBLE_CONFIG` to `local.ansible.cfg`. Then you change this line in `local.ansible.cfg`:

```diff
-ssh_common_args = -F etc/ssh_config_jump0
+ssh_common_args = -F etc/ssh_config_jump1
```

And then you initialise the authentication with `bin/auth-jump1` like before.

