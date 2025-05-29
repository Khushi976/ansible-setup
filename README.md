**🛠️ Ansible Automation Project**

This project is a modular automation setup using Ansible to manage and configure servers for various development and production tasks. It includes independent playbooks for setting up Docker, MongoDB, CUDA, system health checks, Git cloning, and more.

---

**📁 Project Structure**

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

---

**🧾 Inventory Setup**

Your `hosts.ini` defines the remote servers Ansible connects to.

Example `hosts.ini`:

```ini
[all]
192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
192.168.1.11 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[db]
192.168.1.11

[web]
192.168.1.10

**
▶️ Running the Playbooks**
Run the full setup:
ansible-playbook -i hosts.ini playbook.yml
Run individual role playbooks:
ansible-playbook -i hosts.ini roles/docker_setup.yml
ansible-playbook -i hosts.ini roles/mongodb_setup.yml


**🧩 Role Descriptions**

File	Description
common.yml	Base utilities, system updates
Linux_health.yml	System health checks (CPU, memory, disk, etc.)
cuda_setup.yml	CUDA toolkit installation using default sources
cuda_setup_static.yml	Static CUDA installation method
docker_setup.yml	Installs Docker engine
docker_compose.yml	Installs Docker Compose
git_clone.yml	Clones repositories from a Git source
mini_conda.yml	Installs Miniconda for Python environments
mongodb_setup.yml	Sets up a single-node MongoDB instance
mongodb_replica.yml	Configures MongoDB replica set

**📜 Example playbook.yml**

- name: Execute Ansible Automation Setup
  hosts: all
  become: true
  tasks:
    - name: Include Common Setup
      import_playbook: roles/common.yml

    - name: Setup Docker
      import_playbook: roles/docker_setup.yml

    - name: Install Docker Compose
      import_playbook: roles/docker_compose.yml

    - name: Setup CUDA
      import_playbook: roles/cuda_setup.yml

    - name: Install Miniconda
      import_playbook: roles/mini_conda.yml

    - name: Setup MongoDB
      import_playbook: roles/mongodb_setup.yml

    - name: Configure MongoDB Replica
      import_playbook: roles/mongodb_replica.yml

    - name: Git Repository Cloning
      import_playbook: roles/git_clone.yml

    - name: Run System Health Checks
      import_playbook: roles/Linux_health.yml


**🔐 Using Ansible Vault**
To encrypt sensitive variable or credential files:

ansible-vault encrypt secrets.yml

Run a playbook with the vault password:
ansible-playbook -i hosts.ini playbook.yml --ask-vault-pass


**🧪 Tips & Best Practices**

✅ Use ansible-lint for YAML and playbook validation.
🛡️ Protect credentials using ansible-vault.
🔁 Ensure playbooks are idempotent (safe to run multiple times).
🔍 Test on non-production systems before wide-scale deployment.
✍️ Document variables and parameters within each YAML file.
🛡️ .gitignore Suggestion



Here’s an example .gitignore to keep your repository clean:
*.retry
*.log
secrets.yml
__pycache__/
*.pyc
.idea/
.vscode/
.env



📄 License
This project is licensed under the MIT License. See the LICENSE file for details.


Happy Automating with Ansible!

Let me know if you want this generated as a downloadable file or adapted to Markdown with HTML formatting for a website.











:






