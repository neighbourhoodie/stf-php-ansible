# Ansible for PHP with STA project

## Proposal

We created this project as a shadow infra for [Ansible](https://docs.ansible.com/ansible/latest/index.html) to automate server infrastructure setup.

Ansible is a configuration management tool that facilitates the task of setting up and maintaining remote servers.
Ansible doesn’t require any special software to be installed on the nodes that will be managed with this tool. A control machine is set up with the Ansible software, which then communicates with the nodes via standard SSH.

[Here are some tips for making the most of Ansible and Ansible playbooks.](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html#best-practices)


## Set up the jumphost

There is a role that installs common software on the jumphosts (Google Authenticator).

Run it:
```sh
ansible-playbook -i inventory/php jumphosts.yml --tags "install"
```
It installs Google Authenticator and enables it by changing the congig files `/etc/ssh/sshd_config` and `/etc/pam.d/sshd`.

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
User group is `release-manager`. It puts the `.google_authenticator` file to the jumphost and the ssh-key to everywhere.

## Using different jumphosts

You can specify different hosts that you want to run your playbook on. Currently we have two jumphosts set up: one in Europe (ams3) and one in North America (nyc1). By default the host is set to the jumphost in Europe (ams3).

To change jumphost to a different one use the `--extra-vars` argument as follows:

```shell
ansible-playbook -i inventory/php [Add playbook yml file] --extra-vars "host=[ADD HOST e.g. nyc1]"
```

# Delete a user

To delete a user you can run the `deleteUser` playbook. You have to add the `username` of the user you want to delete, this is mandatory. You can also add the name of the host from where you want to delete the user e.g. nyc1, service0, service1. If no host is provided it will be deleted from `ams3` by default.

```shell
ansible-playbook -i inventory/php deleteUser.yml --extra-vars "username=USERNAME host=HOSTNAME"
```

## Running Ansible

Clone the repository and request access to the test droplets.

Ensure you can successfully `ssh` into the test droplets via jumphost from your local machine.

**Run the jumphost playbook as follows:**

```bash
ansible-playbook -i inventory/php jumphosts.yml --ask-vault-pass
```

**Run the playbook for all services as follows:**

```bash
ansible-playbook -i inventory/php services.yml
```

## Using encrypted vars

1. create file `EDITOR=nano ansible-vault create inventory/php/group_vars/all.yml`
2. edit file `EDITOR=nano ansible-vault edit inventory/php/group_vars/all.yml`

(Password was added by the create command: - 123)

Further details on encryption can be found in [ansible documentation](https://docs.ansible.com/ansible/latest/vault_guide/vault_encrypting_content.html).
