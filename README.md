# Ansible for PHP with STA project

## Proposal

We created this project as a shadow infra for [Ansible](https://docs.ansible.com/ansible/latest/index.html) to automate server infrastructure setup.

Ansible is a configuration management tool that facilitates the task of setting up and maintaining remote servers.
Ansible doesn’t require any special software to be installed on the nodes that will be managed with this tool. A control machine is set up with the Ansible software, which then communicates with the nodes via standard SSH.

[Here are some tips for making the most of Ansible and Ansible playbooks.](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html#best-practices)

## Using Ansible

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

## Initialize machines

To initialize your machines, run this playbook:

```sh
ansible-playbook initialize.yml --extra-vars "@/path/to/admins.yml"
```

You have to pass a file with all admins you want to add. The format looks like this, but there is also an example at `etc/admins.yml`:

```yml
admins:
  - name: rocko
    GA_file: /home/rocko/.google_authenticator
    pubkeys:
      - ssh-rsa abcxyz rocko.artischocko@mail.com
      - ssh-ed25519 abcxyz artischocko@rocko.ie
```

You can add several publick keys, but you don't have to.

### What this does

Initialise _all_ machines. This means: jumphosts, services where the properties live on and the rsync machine.

  1. Define all admin users (name, pubkey, Google Authenticator file)
  2. Disable root login
  3. Google Auth set up
  4. Set up firewall rules to only log in via jump host IPs

# Set up services TBD

> [!IMPORTANT]
> Before you run this, you should modify the domain names at `inventory/php/group_vars/service.yml`
>

If you wanna read more about the services, please do so at our [Properties readme](Properties.md).

downloads.php.net
: `ansible-playbook addDownloads.yml`
wiki.php.net
: `ansible-playbook addWiki.yml`
museum.php.net
: `ansible-playbook initMuseum.yml`
main.php.net
: `ansible-playbook initMain.yml`

## Changing the Jumphost

By default, jumphost0 is used, to change this, you have to copy your `ansible.cfg` to `local.ansible.cfg` (which is .gitignored) and set the shell environment variable `ANSIBLE_CONFIG` to `local.ansible.cfg`. Then you change this line in `local.ansible.cfg`:

```diff
-ssh_common_args = -F etc/ssh_config_jump0
+ssh_common_args = -F etc/ssh_config_jump1
```

And then you initialise the authentication with `bin/auth-jump1` like before.


# Utility tasks

## Add a new user

To add a new user, an admin or a release-manager, you use the related playbooks.

### prerequisites

- You need the `.google_authenticator` file somewhere on your local machine
- You have to put the ssh key to `roles/add_ssh_key/templates/ssh_keys/username`.

The playbooks take the required parameters `username` and `path_to_google_auth`:

> [!NOTE]
> The name of the ssh_key file has to be the same as the username.

It creates a linux user and copies the `.google_authenticator` file and the `authorized_keys` to the user's homedir.

### Add an admin user

```shell
ansible-playbook addAdminUser.yml --extra-vars "username=rocko path_to_google_auth=absolute/path/to/.google_authenticator"
```

This playbook creates a new user on jumphosts and all services.
User group is `sudo`. It puts the `.google_authenticator` file to the jumphost and the ssh-key to everywhere.

### Add a release-manager user

A release manager has only access to the downloads machine.

```shell
ansible-playbook addReleaseManagerUser.yml --extra-vars "username=tacocat path_to_google_auth=absolute/path/to/.google_authenticator"
```

This playbook creates a new user on jumphosts and the download-service.
User group is `release-manager`. It puts the `.google_authenticator` file to the jumphost and the ssh-key to the downloads service.

### Delete a user

To delete a user you can run the `deleteUser` playbook. You have to add the `username` of the user you want to delete, this is mandatory. You can also add the name of the host from where you want to delete the user e.g. nyc1, service0, service1. If no host is provided it will be deleted from `all` by default.

```shell
ansible-playbook deleteUser.yml --extra-vars "username=USERNAME host=HOSTNAME"
```

---

## Using encrypted vars

1. create file `EDITOR=nano ansible-vault create inventory/php/group_vars/all.yml`
2. edit file `EDITOR=nano ansible-vault edit inventory/php/group_vars/all.yml`

(Password was added by the create command: - 123)

Further details on encryption can be found in [ansible documentation](https://docs.ansible.com/ansible/latest/vault_guide/vault_encrypting_content.html).


## Using different jumphosts

You can specify different hosts that you want to run your playbook on. Currently we have two jumphosts set up: one in Europe (ams3) and one in North America (nyc1). By default the host is set to the jumphost in Europe (ams3).

To change jumphost to a different one use the `--extra-vars` argument as follows:

```shell
ansible-playbook [Add playbook yml file] --extra-vars "host=[ADD HOST e.g. nyc1]"
```

## Access ip address from ansible facts cache

We use `hostvars` to access server information. Facts need to be gathered and cached in `.ansible-facts-cache` to access it. Run the following to gather cache. Replace HOSTNAME with relevant hostname e.g. `service0` or `jumphost0`.

```shell
ansible HOSTNAME -m setup
```
