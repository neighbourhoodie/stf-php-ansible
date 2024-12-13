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
ssh -fNF etc/ssh_config jumphost0.ams3.do.php.backend.lol
```

This creates an SSH control channel to jumphost0 that will remain valid for 4 hours. Re-run this when connections start failing after 4 hours.

Then you can run any playbook like this:

```shell
ansible-playbook -i inventory/php playbook.yml
```

## Initialize machines

To initialize your machines, run this playbook:

```sh
ansible-playbook -i inventory/php initialize.yml --extra-vars "@/path/to/admins.yml"
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

Initialise all machines
  1. Define all admin users (name, pubkey, Google Authenticator file)
  2. Disable root login
  3. Google Auth set up
  4. Set up firewall rules to only log in via jump host IPs

# Set up services

> [!IMPORTANT]
> Before you run this, you should modify the domain names at `inventory/php/group_vars/service.yml`
>

## downloads.php.net

```sh
ansible-playbook -i inventory/php addDownloads.yml --ask-vault-pass
```

<details>
  <summary>
    <h3>What this does</h3>
  </summary>

  This playbook installs the following sowtware on a machine:
  - apache 2
  - libapache2-mod-php8.2
  - php8.2
  - certbot
  - python3-certbot-apache
  - openssl
  - apache2-utils

  It puts the `apache.conf`, a file with some secrets to `/local/this-box`.
  Further, it copies the apache config files for `downloads.php.net` and `shared.php.net`.
  It creates letsencrypt-certs for `downloads.php.net` and self-signed SSL certs for `shared.php.net`.

</details>

## wiki.php.net

## museum.php.net

## main.php.net


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
ansible-playbook -i inventory/php addAdminUser.yml --extra-vars "username=rocko path_to_google_auth=absolute/path/to/.google_authenticator"
```

This playbook creates a new user on jumphosts and all services.
User group is `sudo`. It puts the `.google_authenticator` file to the jumphost and the ssh-key to everywhere.

### Add a release-manager user

```shell
ansible-playbook -i inventory/php addReleaseManagerUser.yml --extra-vars "username=tacocat path_to_google_auth=absolute/path/to/.google_authenticator"
```

This playbook creates a new user on jumphosts and the download-service.
User group is `release-manager`. It puts the `.google_authenticator` file to the jumphost and the ssh-key to the downloads service.

### Delete a user

To delete a user you can run the `deleteUser` playbook. You have to add the `username` of the user you want to delete, this is mandatory. You can also add the name of the host from where you want to delete the user e.g. nyc1, service0, service1. If no host is provided it will be deleted from `all` by default.

```shell
ansible-playbook -i inventory/php deleteUser.yml --extra-vars "username=USERNAME host=HOSTNAME"
```

---

## Using different jumphosts

You can specify different hosts that you want to run your playbook on. Currently we have two jumphosts set up: one in Europe (ams3) and one in North America (nyc1). By default the host is set to the jumphost in Europe (ams3).

To change jumphost to a different one use the `--extra-vars` argument as follows:

```shell
ansible-playbook -i inventory/php [Add playbook yml file] --extra-vars "host=[ADD HOST e.g. nyc1]"
```

## Using encrypted vars

1. create file `EDITOR=nano ansible-vault create inventory/php/group_vars/all.yml`
2. edit file `EDITOR=nano ansible-vault edit inventory/php/group_vars/all.yml`

(Password was added by the create command: - 123)

Further details on encryption can be found in [ansible documentation](https://docs.ansible.com/ansible/latest/vault_guide/vault_encrypting_content.html).
