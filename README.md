```
👩  This project is part of the passbolt "lab"!
⚗️   It is used to illustrate an article or as a conversation starter.
🧪  Use at your own risks!
```

## Pre-requisites
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [Git](https://git-scm.com/downloads)
- A vanilla server
  - An access to the target server with necessary permission 

## Getting Started

### Clone the repository
```bash
git clone git@github.com:passbolt/lab-passbolt-ansible-install-playbook.git
```

### Update the environment variables

| Environment variable name      | Description                                          | Example                                                                                     |
|--------------------------------|------------------------------------------------------|---------------------------------------------------------------------------------------------|
| db_host                        | The database host                                    | 127.0.0.1                                                                                   |
| db_name                        | The passbolt database name                           | passboltdb                                                                                  |
| db_username                    | The passbolt user username                           | passboltadmin                                                                               |
| db_password                    | The passbolt user password                           | P4ssb0lt!                                                                                   |
| db_root_user                   | The database root username                           | root                                                                                        |
| db_root_password               | The database root password                           | \\(t0-0r)/                                                                                  |
| passbolt_url                   | The passbolt domain name                             | passbolt.local                                                                              |
| php_version                    | The default PHP version                              | 8.2                                                                                         |
| passbolt_edition               | The passbolt edition (ce / pro)                      | ce                                                                                          |
| ssl_subj                       | The self-signed certificate subject information      | /C=LU/ST=Luxembourg/L=Esch-Sur-Alzette/O=Passbolt SA/OU=Passbolt IT Team/CN=passbolt.local/ |
| ssl_subjectAltName             | The self-signed certificate subjectAltName (DNS)     | DNS:passbolt.local                                                                          |
| [PRO] subscription_key_content | The content of the subscription key (base64 encoded) | SUBSCRIPTION KEY (PRO)                                                                      |
| server_gpg_name_real           | The name associated to the server key                | server@passbolt.com                                                                         |
| server_gpg_name_email          | The email associated to the server key               | Passbolt Server                                                                             |
| passbolt_admin_email           | The passbolt first administrator email (username)    | anakin@passbolt.com                                                                         |
| passblt_admin_first_name       | The passbolt first administrator first name          | Anakin                                                                                      |
| passbolt_admin_last_name       | The passbolt first administrator last name           | Skywalker                                                                                   |


### Create an inventory file

You will need to create an inventory file with the details of the targeted server, at the root of the repository, run `touch inventory`

#### Authentication with SSH Key

If you are using your SSH key to logging in to the server, ensure to correctly specify the path of your key
```bash
[passbolt_server]
YOUR_SERVER_IP ansible_user=YOUR_USER ansible_ssh_private_key_file=PATH_TO_YOUR_KEY
```

#### Authentication with password

If you are using a dedicated password to logging in to the server, you can use the example below
```bash
[passbolt_server]
YOUR_SERVER_IP ansible_user=YOUR_USER ansible_ssh_pass=YOUR_PASSWORD
```

#### Authentication to a vagrant machine

If you are on a vagrant machine, you should use the insecure private key in order to logging in
```bash
[passbolt_server]
your_vagrant_machine_ip ansible_user=vagrant ansible_private_key_file=~PATH_TO_INSECURE_PRIVATE_KEY
```

**Pro tips:** The insecure private key for vagrant is most of the time located in `/.vagrant.d/insecure_private_key`

### Run the ansible-playbook
```bash
ansible-playbook -i inventory playbook.yaml 
```

### Configure the passbolt server through the web interface
You should navigate to the `passbolt_url` to finish the installation process e.g. https://passbolt.local


### Run the healthCheck from the server
After the installation, you should monitor that there is no issues with the installation process

`Debian/Ubuntu distribution`
```bash
sudo su -s /bin/bash -c "/usr/share/php/passbolt/bin/cake passbolt healthcheck" www-data
```

`RPM distribution`
```bash
sudo su -s /bin/bash -c "/usr/share/php/passbolt/bin/cake passbolt healthcheck" nginx
```

## Tests

This ansible installation script has been tested on:
- Debian 12 (PRO/CE)
- Debian 11 (PRO/CE)
- Ubuntu 20.04 (CE/PRO)
- Ubuntu 22.04 (CE/PRO)
- Ubuntu 24.04 (CE/PRO)
- AlmaLinux 8 (PRO/CE)
- AlmaLinux 9 (PRO/CE)
- OracleLinux 9 (PRO/CE)
- OracleLinux 9 (PRO/CE)
- RockyLinux 8 (PRO/CE)
- RockyLinux 9 (PRO/CE)

Feel free to help us throughout other distributions and let us know whenever you encounter an issues or if it works fine.

## Copyright & License

(c) 2024 Passbolt SA

Passbolt is registered trademark of Passbolt S.A.

MIT No Attribution - https://opensource.org/licenses/MIT-0