# Ansible Automation Setup
Ansible Setup for MongoDB and GitHub Repository Cloning

This Ansible playbook automates the setup of Docker, cloning a GitHub repository, and configuring MongoDB with a replica set and user authentication.

**Prerequisites**

Ansible installed on the control machine

Target servers accessible via SSH

A valid GitHub personal access token (PAT) stored in an .env file

Root or sudo privileges on the target machines

**Features**

Installs Git and Docker

Clones a specified GitHub repository

Configures MongoDB with a secure keyfile

Initializes a MongoDB replica set

Creates a database user

Starts MongoDB containers using Docker Compose

Waits for MongoDB to be ready and verifies the replica set status

**Setup Instructions**

1. Store GitHub PAT Securely

To avoid exposing your GitHub personal access token in the playbook, store it in an .env file (which should be added to .gitignore to prevent accidental commits):

# .env
GITHUB_PAT="your_personal_access_token"

2. Update .gitignore

Add the .env file to .gitignore to prevent it from being committed to the repository:

# .gitignore
.env

3. Run the Ansible Playbook

Ensure your inventory file (e.g., inventory.ini) is properly set up with your target server(s). Then execute the playbook:

ansible-playbook -i inventory.ini playbook.yml --extra-vars "@.env"

4. Verify MongoDB Setup

To check the status of the MongoDB replica set, run:

docker exec mongodb-1 mongosh --host localhost --port 27018 -u root -p root --authenticationDatabase admin --eval 'rs.status()'

5. Check Running Containers

Use the following command to verify that the MongoDB containers are running:

docker ps

6. Verify MongoDB User Creation

Run the following command to verify that the sentinel user exists:

docker exec mongodb-1 mongosh --host localhost --port 27018 -u root -p root --authenticationDatabase admin --eval 'db.getSiblingDB("sentinel").getUsers()'

Troubleshooting

If the playbook fails due to permission issues, try running it with sudo.

If GitHub authentication fails, ensure that your PAT is correct and has the required repository permissions.

If MongoDB doesn't start, check container logs using:

docker logs mongodb-1

If the replica set initialization fails, manually run:

docker exec mongodb-1 mongosh --host localhost --port 27018 -u root -p root --authenticationDatabase admin --eval 'rs.initiate()'

Contributions

Feel free to contribute by creating a pull request or raising an issue in the repository.
