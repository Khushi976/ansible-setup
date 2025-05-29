# 🛠️ Ansible Automation Project

This project provides a modular set of Ansible playbooks to automate the setup and configuration of various components such as Docker, MongoDB, CUDA, Git repositories, and more.

---

## 📁 Directory Structure

.
├── roles/
│ ├── Linux_health.yml
│ ├── common.yml
│ ├── cuda_setup.yml
│ ├── cuda_setup_static.yml
│ ├── docker_compose.yml
│ ├── docker_setup.yml
│ ├── git_clone.yml
│ ├── mini_conda.yml
│ ├── mongodb_replica.yml
│ └── mongodb_setup.yml
├── hosts.ini
├── main.yml
├── playbook.yml
├── .gitignore
└── README.md


## 🧾 Inventory Setup

Define your target hosts inside `hosts.ini`. Here's an example structure:

```ini
[all]
192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
192.168.1.11 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[db]
192.168.1.11

[web]
192.168.1.10
📜 Playbook Execution
To run the main playbook:
ansible-playbook -i hosts.ini playbook.yml
If you want to execute specific tasks:

ansible-playbook -i hosts.ini roles/docker_setup.yml
🧩 Role Overview
Each file under the roles/ folder is a standalone playbook that encapsulates a specific setup task. You can include them in the main playbook or run them independently.

✅ Included Roles
Role	Description
common.yml	Base system updates, utilities
Linux_health.yml	System health checks and diagnostics
cuda_setup.yml	CUDA toolkit installation (default method)
cuda_setup_static.yml	CUDA static setup (non-dynamic envs)
docker_setup.yml	Docker engine installation
docker_compose.yml	Docker Compose setup
git_clone.yml	Clones repositories
mini_conda.yml	Installs Miniconda
mongodb_setup.yml	MongoDB single-node setup
mongodb_replica.yml	MongoDB replica set configuration

How main.yml & playbook.yml Work
main.yml: Might be used to include/import all individual role YAMLs.

playbook.yml: Primary playbook that gets executed and includes roles/tasks conditionally or sequentially.

Example structure for playbook.yml:
- name: Master setup playbook
  hosts: all
  become: true
  tasks:
    - name: Include base setup
      import_playbook: roles/common.yml

    - name: Install Docker
      import_playbook: roles/docker_setup.yml

    - name: Setup MongoDB
      import_playbook: roles/mongodb_setup.yml

🔐 Ansible Vault (Optional)
To encrypt sensitive files like secrets or credentials:

ansible-vault encrypt secrets.yml
To run playbooks with vault:
ansible-playbook -i hosts.ini playbook.yml --ask-vault-pass


✅ Best Practices
Use ansible-lint to catch issues.

Keep roles atomic and reusable.

Secure credentials with ansible-vault.

Document each role with comments inside the YAML.

📄 License
MIT License. See the LICENSE file for details.


Happy Automating! 🚀

---

Let me know if you'd like to autogenerate this `README.md` based on the actual task names from each `.yml` file, or if you want a breakdown of what each script does line by line.






