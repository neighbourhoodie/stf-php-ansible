# Scripts list

There are many script files used in the [PHP Systems](https://github.com/php/systems) repository to maintain the different properties. Some of these scripts have been converted to Ansible scripts and moved to the roles of this respository.

Following are the list of all the scripts used in the Systems repository and they are marked as whether they are moved to Ansible scripts or left in the existing Systems repo.

| Script | PHP Systems | Ansible project |
|--------|-------------| --------------- |
| analytics/analytics.php.net.conf    | [analytics.php.net.conf](https://github.com/php/systems/blob/master/analytics/analytics.php.net.conf)       | - |
| analytics/installed-packages.txt    | [installed-packages.txt](https://github.com/php/systems/blob/master/analytics/installed-packages.txt)       | - |
| analytics/users                     | [users](https://github.com/php/systems/blob/master/analytics/users)                                         | - |
| bk2/apache2/monitoring.php.net.conf | [monitoring.php.net.conf](https://github.com/php/systems/blob/master/bk2/apache2/monitoring.php.net.conf)   | - |
| bk2/README.md                       | [README.md](https://github.com/php/systems/blob/master/bk2/README.md)                                       | - |
| bk2/install-config.sh               | [install-config.sh](https://github.com/php/systems/blob/master/bk2/install-config.sh)                       | - |
| bk2/installed-packages.txt          | [installed-packages.txt](https://github.com/php/systems/blob/master/bk2/installed-packages.txt)             | - |
| boxen/analytics                     |[analytics](https://github.com/php/systems/blob/master/boxen/analytics)                                      | - |
| boxen/bk2                           | [bk2](https://github.com/php/systems/blob/master/boxen/bk2)                                                 | - |
| boxen/bugs                          | [bugs](https://github.com/php/systems/blob/master/boxen/bugs)                                               | - |
| boxen/downloads.php.net             | [downloads.php.net](https://github.com/php/systems/blob/master/boxen/downloads.php.net) | [roles/properties/downloads/tasks/deploy.yml#L15](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/downloads/tasks/deploy.yml#L15) |
| boxen/euk2.php.net                  | [euk2.php.net](https://github.com/php/systems/blob/master/boxen/euk2.php.net) | - |
| boxen/main.php.net                  | [main.php.net](https://github.com/php/systems/blob/master/boxen/main.php.net) | [properties/main/tasks/deploy.yml#L36](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/main/tasks/deploy.yml#L36) |
| boxen/qa.php.net                    | [qa.php.net](https://github.com/php/systems/blob/master/boxen/qa.php.net)                             | - |
| boxen/svn2.php.net                  | [svn2.php.net](https://github.com/php/systems/blob/master/boxen/svn2.php.net)                         | - |
| bugs.php.net/additional.mysql.cnf   | [additional.mysql.cnf](https://github.com/php/systems/blob/master/bugs.php.net/additional.mysql.cnf)  | - |
| downloads.php.net/apache2/downloads.php.net.conf | [downloads.php.net.conf](https://github.com/php/systems/blob/master/downloads.php.net/apache2/downloads.php.net.conf) | [roles/properties/downloads/templates/downloads.php.net.conf](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/downloads/templates/downloads.php.net.conf) |
| downloads.php.net/apache2/shared.php.net.conf | [shared.php.net.conf](https://github.com/php/systems/blob/master/downloads.php.net/apache2/shared.php.net.conf) | [roles/properties/shared/templates/shared.php.net.conf](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/shared/templates/shared.php.net.conf) |
| main.php.net/apache2/sites-available/gcov.php.net.conf | [gcov.php.net.conf](https://github.com/php/systems/blob/master/main.php.net/apache2/sites-available/gcov.php.net.conf) | [roles/properties/gcov/templates/gcov.php.net.conf](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/gcov/templates/gcov.php.net.conf) |
| main.php.net/apache2/sites-available/lxr.php.net.conf | [lxr.php.net.conf](https://github.com/php/systems/blob/master/main.php.net/apache2/sites-available/lxr.php.net.conf) | [roles/properties/lxr/templates/lxr.php.net.conf](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/lxr/templates/lxr.php.net.conf) |
| main.php.net/apache2/sites-available/status.php.net.conf | [status.php.net.conf](https://github.com/php/systems/blob/master/main.php.net/apache2/sites-available/status.php.net.conf) | [roles/properties/status/templates/status.php.net.conf](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/status/templates/status.php.net.conf) |
| php-web4/nginx/sites-available/www.php.net | [www.php.net](https://github.com/php/systems/blob/master/php-web4/nginx/sites-available/www.php.net) | - |
| php-web4/nginx/mime.types           | [mime.types](https://github.com/php/systems/blob/master/php-web4/nginx/mime.types)            | - |
| php-web4/nginx/nginx.conf           | [nginx.conf](https://github.com/php/systems/blob/master/php-web4/nginx/nginx.conf)            | - |
| qa/apache2/news.php.net.conf        | [news.php.net.conf](https://github.com/php/systems/blob/master/qa/apache2/news.php.net.conf)  | - |
| qa/apache2/qa.php.net.conf          | [qa.php.net.conf](https://github.com/php/systems/blob/master/qa/apache2/qa.php.net.conf)      | - |
| qa/colobus/config                   | [config](https://github.com/php/systems/blob/master/qa/colobus/config)                        | - |
| qa/postfix/aliases                  | [aliases](https://github.com/php/systems/blob/master/qa/postfix/aliases)                      | - |
| qa/postfix/main.cf                  | [main.cf](https://github.com/php/systems/blob/master/qa/postfix/main.cf)                      | - |
| qa/supervisor/colobus.conf          | [colobus.conf](https://github.com/php/systems/blob/master/qa/supervisor/colobus.conf)         | - |
| qa/supervisor/colobus.conf          | [colobus.conf](https://github.com/php/systems/blob/master/qa/supervisor/colobus.conf)         | - |
| qa/README.md                        | [README.md](https://github.com/php/systems/blob/master/qa/README.md)                          | - |
| qa/install-config.sh                | [install-config.sh](https://github.com/php/systems/blob/master/qa/install-config.sh)          | - |
| qa/sync-mlmmj-and-colobus.php       | [sync-mlmmj-and-colobus.php](https://github.com/php/systems/blob/master/qa/sync-mlmmj-and-colobus.php) | - |
| qa/users | [users](https://github.com/php/systems/blob/master/qa/users)                                                             | - |
| rsync.php.net/README.md             | [README.md](https://github.com/php/systems/blob/master/rsync.php.net/README.md)         | - |
| rsync.php.net/cronjobs.root         | [cronjobs.root](https://github.com/php/systems/blob/master/rsync.php.net/cronjobs.root) | [roles/properties/rsync/tasks/main.yml#L46-74](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/rsync/tasks/main.yml#L46-74) |
| rsync.php.net/rsynd.conf            | [rsynd.conf](https://github.com/php/systems/blob/master/rsync.php.net/rsynd.conf)       | [roles/properties/rsync/templates/rsynd.conf](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/rsync/templates/rsynd.conf) |
| shared-config/20-sudo-nopassword    | [20-sudo-nopassword](https://github.com/php/systems/blob/master/shared-config/20-sudo-nopassword) | [initialize.yml#L128](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/initialize.yml#L128) |
| shared-config/iptables.conf         | [iptables.conf](https://github.com/php/systems/blob/master/shared-config/iptables.conf) | - |
| svn2/apache2/conf-available/remote-ip-log.conf    | [remote-ip-log.conf](https://github.com/php/systems/blob/master/svn2/apache2/conf-available/remote-ip-log.conf)   | - |
| svn2/apache2/sites-available/conf.php.net.conf    | [conf.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/conf.php.net.conf)    | - |
| svn2/apache2/sites-available/conf2.php.net.conf   | [conf2.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/conf2.php.net.conf)  | - |
| svn2/apache2/sites-available/doc.php.net.conf     | [doc.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/doc.php.net.conf)      | - |
| svn2/apache2/sites-available/gtk.php.net.conf     | [gtk.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/gtk.php.net.conf)      | - |
| svn2/apache2/sites-available/people.php.net.conf  | [people.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/people.php.net.conf) | - |
| svn2/apache2/sites-available/pres.php.net.conf    | [pres.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/pres.php.net.conf)    | - |
| svn2/apache2/sites-available/pres2.php.net.conf   | [pres2.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/pres2.php.net.conf)  | - |
| svn2/apache2/sites-available/talks.php.net.conf   | [talks.php.net.conf](https://github.com/php/systems/blob/master/svn2/apache2/sites-available/talks.php.net.conf)  | - |
| svn2/installed-packages.txt         | [installed-packages.txt](https://github.com/php/systems/blob/master/svn2/installed-packages.txt) | - |
| svn2/users                          | [users](https://github.com/php/systems/blob/master/svn2/users)                        | - |
| archive-matomo-data                 | [archive-matomo-data](https://github.com/php/systems/blob/master/archive-matomo-data) | - |
| backup-bugsweb                      | [backup-bugsweb](https://github.com/php/systems/blob/master/backup-bugsweb)           | - |
| backup-main                         | [backup-main](https://github.com/php/systems/blob/master/backup-main) | [properties/main/tasks/backup.yml](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/main/tasks/backup.yml) |
| backup-pear                         | [backup-pear](https://github.com/php/systems/blob/master/backup-pear)                 | - |
| backup-pecl                         | [backup-pecl](https://github.com/php/systems/blob/master/backup-pecl)                 | - |
| backup-thisbox                      | [backup-thisbox](https://github.com/php/systems/blob/master/backup-thisbox)           | - |
| backup-wiki-php-net                 | [backup-wiki-php-net](https://github.com/php/systems/blob/master/backup-wiki-php-net) | [roles/properties/wiki/tasks/backup.yml](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/wiki/tasks/backup.yml) |
| build-docs-lang-rsync               | [build-docs-lang-rsync](https://github.com/php/systems/blob/master/build-docs-lang-rsync) | - |
| build-docs-rsync                    | [build-docs-rsync](https://github.com/php/systems/blob/master/build-docs-rsync) | [roles/properties/rsync/templates/build-docs-rsync](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/rsync/templates/build-docs-rsync) |
| build-manual                        | [build-manual](https://github.com/php/systems/blob/master/build-manual)                     | - |
| build-pear-manual                   | [build-pear-manual](https://github.com/php/systems/blob/master/build-pear-manual)           | - |
| check-fails                         | [check-fails](https://github.com/php/systems/blob/master/check-fails)                       | - |
| check-ssh-connectivity              | [check-ssh-connectivity](https://github.com/php/systems/blob/master/check-ssh-connectivity) | - |
| create-system-users.sh              | [create-system-users.sh](https://github.com/php/systems/blob/master/create-system-users.sh) | [addAdminUser.yml](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/addAdminUser.yml) |
| create_aliases.sh                   | [create_aliases.sh](https://github.com/php/systems/blob/master/create_aliases.sh)           | - |
| cron-box                            | [cron-box](https://github.com/php/systems/blob/master/cron-box)                             | - |
| crontab                             | [crontab](https://github.com/php/systems/blob/master/cron-box-crontab)                      | - |
| email-assigned-bugsweb              | [email-assigned-bugsweb](https://github.com/php/systems/blob/master/email-assigned-bugsweb) | - |
| export_phpmasterdb_aliases.sh       | [export_phpmasterdb_aliases.sh](https://github.com/php/systems/blob/master/export_phpmasterdb_aliases.sh) | - |
| gen-ide-json.php                    | [gen-ide-json.php](https://github.com/php/systems/blob/master/gen-ide-json.php)             | - |
| gen-phpweb-sqlite-db.php            | [gen-phpweb-sqlite-db.php](https://github.com/php/systems/blob/master/gen-phpweb-sqlite-db.php) | - |
| install-colobus                     | [install-colobus](https://github.com/php/systems/blob/master/install-colobus)               | - |
| install-docweb-jpgraph              | [install-docweb-jpgraph](https://github.com/php/systems/blob/master/install-docweb-jpgraph) | - |
| install-iptables-config             | [install-iptables-config](https://github.com/php/systems/blob/master/install-iptables-config) | - |
| maintain-main                       | [maintain-main](https://github.com/php/systems/blob/master/maintain-main) | [roles/properties/main/templates/maintain-main](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/main/templates/maintain-main) |
| maintain-master-dns.php             | [maintain-master-dns.php](https://github.com/php/systems/blob/master/maintain-master-dns.php) | [roles/properties/main/templates/maintain-master-dns.php](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/main/templates/maintain-master-dns.php) |
| maintain-pear                       | [maintain-pear](https://github.com/php/systems/blob/master/maintain-pear)                   | - |
| no-feedback-bugsweb                 | [no-feedback-bugsweb](https://github.com/php/systems/blob/master/no-feedback-bugsweb)       | - |
| populate-rsync.sh                   | [populate-rsync.sh](https://github.com/php/systems/blob/master/populate-rsync.sh) | [roles/properties/rsync/templates/git-clone](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/rsync/templates/git-clone) |
| php.net.zone                        | [php.net.zone](https://github.com/php/systems/blob/master/php.net.zone) | [roles/properties/main/templates/php.net.zone](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/main/templates/php.net.zone) |
| process-main-zone-file              | [process-main-zone-file](https://github.com/php/systems/blob/master/process-main-zone-file) | [roles/properties/main/templates/process-main-zone-file](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/main/templates/process-main-zone-file) |
| prune-backups                       | [prune-backups](https://github.com/php/systems/blob/master/prune-backups) | [roles/backup_property/tasks/main.yml#L52](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/backup_property/tasks/main.yml#L52) |
| runone                              | [runone](https://github.com/php/systems/blob/master/runone)                                   | - |
| update-analytics-web                | [update-analytics-web](https://github.com/php/systems/blob/master/update-analytics-web)       | - |
| update-bugsweb                      | [update-bugsweb](https://github.com/php/systems/blob/master/update-bugsweb)                   | - |
| update-colobus-archive              | [update-colobus-archive](https://github.com/php/systems/blob/master/update-colobus-archive)   | - |
| update-cvs-mail-aliases             | [update-cvs-mail-aliases](https://github.com/php/systems/blob/master/update-cvs-mail-aliases) | - |
| update-distributions                | [update-distributions](https://github.com/php/systems/blob/master/update-distributions)       | - |
| update-docs-sources                 | [update-docs-sources](https://github.com/php/systems/blob/master/update-docs-sources)         | - |
| update-docs-translation-status      | [update-docs-translation-status](https://github.com/php/systems/blob/master/update-docs-translation-status) | - |
| update-docweb                       | [update-docweb](https://github.com/php/systems/blob/master/update-docweb)                     | - |
| update-download-area                | [update-download-area](https://github.com/php/systems/blob/master/update-download-area)       | - |
| update-downloads                    | [update-downloads](https://github.com/php/systems/blob/master/update-downloads) | [roles/properties/downloads/templates/update-downloads](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/downloads/templates/update-downloads) |
| update-everything                   | [update-everything](https://github.com/php/systems/blob/master/update-everything) | [roles/properties/rsync/templates/update-everything](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/rsync/templates/update-everything) |
| update-gtkweb                       | [update-gtkweb](https://github.com/php/systems/blob/master/update-gtkweb)                     | - |
| update-letsencrypt                  | [update-letsencrypt](https://github.com/php/systems/blob/master/update-letsencrypt) | [roles/add_certbot/tasks/main.yml#L53](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/add_certbot/tasks/main.yml#L53) |
| update-manuals                      | [update-manuals](https://github.com/php/systems/blob/master/update-manuals)                 | - |
| update-mirrors                      | [update-mirrors](https://github.com/php/systems/blob/master/update-mirrors) | [roles/properties/rsync/templates/update-mirrors](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/rsync/templates/update-mirrors) |
| update-newsweb                      | [update-newsweb](https://github.com/php/systems/blob/master/update-newsweb)                 | - |
| update-pearweb-manuals              | [update-pearweb-manuals](https://github.com/php/systems/blob/master/update-pearweb-manuals) | - |
| update-peclweb                      | [update-peclweb](https://github.com/php/systems/blob/master/update-peclweb)                 | - |
| update-peopleweb                    | [update-peopleweb](https://github.com/php/systems/blob/master/update-peopleweb)             | - |
| update-phd-docs                     | [update-phd-docs](https://github.com/php/systems/blob/master/update-phd-docs)               | - |
| update-phpweb-backend               | [update-phpweb-backend](https://github.com/php/systems/blob/master/update-phpweb-backend)   | - |
| update-phpweb-manuals               | [update-phpweb-manuals](https://github.com/php/systems/blob/master/update-phpweb-manuals)   | - |
| update-qaweb                        | [update-qaweb](https://github.com/php/systems/blob/master/update-qaweb)                     | - |
| update-shared                       | [update-shared](https://github.com/php/systems/blob/master/update-shared) | [roles/properties/shared/templates/update-shared](https://github.com/neighbourhoodie/stf-php-ansible/blob/main/roles/properties/shared/templates/update-shared) |
| update-systems                      | [update-systems](https://github.com/php/systems/blob/master/update-systems)                 | - |
| update-talksweb                     | [update-talksweb](https://github.com/php/systems/blob/master/update-talksweb)               | - |
| update-time                         | [update-time](https://github.com/php/systems/blob/master/update-time)                       | - |
| update-win-pkg-cache                | [update-win-pkg-cache](https://github.com/php/systems/blob/master/update-win-pkg-cache)     | - |
