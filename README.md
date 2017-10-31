# Ansible Role for Lufi (Let's Upload That File)

[![Build Status](https://travis-ci.org/noplanman/ansible-lufi.svg?branch=master)](https://travis-ci.org/noplanman/ansible-lufi)

Installs and configures Lufi on Debian/Ubuntu servers.
Find out more about Lufi [here](https://framagit.org/luc/lufi), created by [Luc Didry](https://framagit.org/u/luc).

This role will automatically install a service that will start when the server boots up.
It will figure out which service manager is being used automatically too.

## Requirements

Using this role doesn't install Nginx or Apache as a reverse proxy, you need to do that yourself!
An example configuration for Nginx can be found [here](https://framagit.org/luc/lufi/wikis/installation#putting-lufi-behind-nginx).

## Role Variables

Set the user/group that will be used to run Lufi. It makes sense to use the webserver user/group.

```
lufi_user: www-data
lufi_group: www-data
```

Set if Lufi should be kept up to date. (default: no)

```
lufi_keep_updated: no
```

There are a few mandatory and many optional values. Check all possible variables in `defaults/main.yml`.

```
# Required!
lufi_working_dir: "/var/www/example.com"
lufi_listen: "http://127.0.0.1:8080"    # Or an array, if multiple addresses.
lufi_contact: "admin@example.com"
lufi_secrets: ["array", "of", "random", "secrets"]

# Optional
lufi_theme: "default"
lufi_proxy: no
lufi_workers: 30
lufi_clients: 1
lufi_url_length: 8
lufi_provis_step: 5
lufi_provisioning: 100
lufi_token_length: 32
lufi_max_file_size: 104857600
lufi_piwik_img: ""
lufi_broadcast_message: ""
lufi_default_delay: 0
lufi_max_delay: 0
lufi_prefix: "/"
lufi_allowed_domains: []
lufi_fixed_domain: ""
lufi_mail_sender: "no-reply@lufi.io"
lufi_db_path: "lufi.db"
lufi_upload_dir: "files"
lufi_session_duration: 3600
lufi_keep_ip_during: 365
lufi_max_total_size: 10*1024*1024*1024
lufi_policy_when_full: "warn"
lufi_delete_no_longer_viewed_files: 90
```

## Role Tags

Each part of the setup has a tag.

```
lufi:install
lufi:site
lufi:service
```

## Dependencies

None.

## Example Playbook

```
# playbook.yml
---
- hosts: servers
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - { role: noplanman.lufi }
```
```
# vars/main.yml
---
lufi_working_dir: "/var/www/lufi.example.com"
lufi_listen: "http://127.0.0.1:8080"
lufi_contact: "admin@lufi.example.com"
lufi_secrets: ["xud7ooJu","aiNg7duG","ih7kom8Z","Ocaish3I","Ooja7chi","Eet4weil","Ethee4Go","xahJ0ohy"]
lufi_broadcast_message: "Welcome to Lufi. Upload those files!"
```

## License

MIT
