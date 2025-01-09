# Services and properties

Each property is implemented as an Ansible role located in the [roles/properties](roles/properties) directory.

All properties have a `templates` directory. This is for files such as cron scripts or configuration files needed by the property.

## Rsync

This service keeps repositories up-to-date by performing a git checkout via a cron job.
The update process is automated to ensure the latest version of the code is always available.

On the Rsync.php.net machine are 4 directories located:

`local/services`: The location of the scripts responsible for updating repositories and the rsync daemon config file.

`local/mirrors`: The directory where the repositories are stored and updated.

`/local/repos`: Another directory where the repositories are stored and updated.

#### Content workflow
rsync.php.net is a property. It pulls content from GitHub and puts the file to `/local/mirrors/{property}` on the rsync-machine. The property itself pulls the data from this folder via `rsync`. All this is handled by cronjobs.

```mermaid
graph TD
    A[Git Repository] -->|Cronjob: Pull updates| B[Rsync Service]
    B -->|Cronjob: Pull updates| C[Property Local Repository]
    C -->|Deploy to| D[Document Root]
```

## Services
```mermaid
graph TD
  ServiceMain[Main Service] --> Status[status]
  ServiceMain --> Main[main]
  ServiceMain --> Gcov[gcov]
  ServiceMain --> Lxr[lxr]
  
  ServiceWiki[Wiki Service] --> Wiki[wiki]
  ServiceMuseum[Museum Service] --> Museum[museum]
  
  ServiceDownloads[Downloads Service] --> Downloads[downloads]
  ServiceDownloads --> Shared[shared]
```

### downloads

```sh
ansible-playbook addDownloads.yml
```

<details>
  <summary>
    <h3>What this does</h3>
  </summary>

  It puts the `apache.conf`, a file with some secrets to `/local/this-box`.
  Further, it copies the apache config files for `downloads.php.net` and `shared.php.net`.
  It creates letsencrypt-certs for `downloads.php.net` and self-signed SSL certs for `shared.php.net`.

</details>

### wiki

This playbook installs the following:

- apache2
- libapache2-mod-php8.2
- php8.2
- certbot
- python3-certbot-apache

It copies the apache config file to wiki.conf and creates letsencrypt certificates.
The domain and email is saved as variables.

### museum

### main


## Backups

Backups are run as part of the property role tasks.

Backup process is different for `main` and other properties. For `main` backup is done for mysql database and apache2 config as per: https://github.com/php/systems/blob/master/backup-main and for other properties a tar file of the docroot folder is created and is backed up.
