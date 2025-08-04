# Automated WordPress Deployment with Ansible Roles

A modular, production-ready Ansible project for installing and configuring WordPress on Ubuntu 22.04. This repository provides reusable roles for Apache, PHP, MariaDB, and WordPress—ideal for teams and third-party integration.

## Architecture

- **Ansible Controller:** Any Linux host with Ansible installed.
- **Managed Nodes:** Ubuntu 22.04 servers (e.g., AWS EC2 instances).
- **Connectivity:** SSH with privilege escalation (sudo).

## Repository Layout

├── inventory.ini               # Inventory file for target hosts  
├── site.yml                    # Main playbook  
├── group_vars/                 # Shared variables  
│   ├── all.yml                 # Non-sensitive defaults  
│   └── vault.yml               # Encrypted secrets (Ansible Vault)  
└── roles/  
    ├── apache/                 # Apache install & config  
    ├── php/                    # PHP and extensions  
    ├── mariadb/                # MariaDB install & hardening  
    └── wordpress/              # Download, configure, and secure WP  

## Prerequisites

- Ansible ≥ 2.9  
- SSH access to all target hosts  
- (Optional) Ansible Vault for secrets management  

## Getting Started

1. Clone this repository:  
   ```bash
   git clone https://github.com/yourorg/wordpress-ansible.git
   cd wordpress-ansible
   ```

2. Define your inventory in `inventory.ini`:  
   ```ini
   [web]
   192.0.2.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
   ```

3. Configure non-sensitive defaults in `group_vars/all.yml`.

4. Create and encrypt `group_vars/vault.yml` for database credentials:  
   ```bash
   ansible-vault create group_vars/vault.yml
   ```

5. Run the playbook:  
   ```bash
   ansible-playbook -i inventory.ini site.yml --ask-vault-pass
   ```

6. Once completed, visit `http://<your_server_ip>` to finalize WordPress setup.

## Customization

- **Variables:** Adjust paths, package lists, and credentials in `group_vars/all.yml`.  
- **Templates:** Tweak Apache vhost in `roles/wordpress/templates/wordpress.conf.j2`.  
- **Extensions:** Enable or disable PHP modules in `roles/php/vars/main.yml`.  

## Security and Best Practices

- Store sensitive data (passwords, API keys) in Ansible Vault (`vault.yml`).  
- Use least-privilege users and secure file permissions (`www-data:www-data`, `0644/0755`).  
- Harden MariaDB by removing anonymous accounts, disabling remote root, and deleting test databases.  
- Generate WordPress salt keys via the official API for session security.  
- Enable Apache security headers (X-Frame-Options, X-Content-Type-Options, etc.).  

## Contributing

1. Fork the repository  
2. Create a feature branch (`git checkout -b feature/xyz`)  
3. Commit your changes (`git commit -m "Add xyz"`)  
4. Push and open a Pull Request  


