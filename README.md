# Ansible Homelab Automation

An Ansible project for performing operational health checks across a self-hosted Kubernetes homelab.

The project demonstrates configuration management, SSH-based automation, Linux administration, and infrastructure operations.

## Architecture

```text
Ansible Automation VM
        |
        | SSH / Ansible
        |
  +-----+----------+
  |        |       |
Control  Worker  Worker
 Plane     01      02
  +--------+-------+
    Kubernetes Cluster

Features
- Collects operating system facts.
- Reports hostnames and system uptime.
- Checks root filesystem usage.
- Uses SSH for remote administration.
- Keeps read-only health checks from reporting false changes.
- Validates playbooks using GitHub Actions.
Technology Stack
- Ubuntu Server
- Ansible Core
- Linux and SSH
- Kubernetes
- Git and GitHub Actions
Repository Structure
ansible-homelab/
├── .github/workflows/ansible-check.yml
├── inventory/hosts.ini.example
├── playbooks/cluster-health.yml
├── .gitignore
└── README.md


Prerequisites
- Ansible installed on the automation host.
- SSH connectivity to the target nodes.
- An SSH key configured for the remote account.
Setup
Clone the repository:
git clone https://github.com/YOUR_GITHUB_USERNAME/ansible-homelab.git
cd ansible-homelab


Create a local inventory:
cp inventory/hosts.ini.example inventory/hosts.ini


Edit inventory/hosts.ini with your actual node addresses and SSH username. This local file is excluded from Git.
Test connectivity:
ansible kubernetes -i inventory/hosts.ini -m ping


Run the health check:
ansible-playbook -i inventory/hosts.ini playbooks/cluster-health.yml


Continuous Integration
GitHub Actions checks playbook syntax and runs Ansible Lint on pushes and pull requests targeting main. The workflow does not connect to the homelab.
Security
- Never commit passwords, access tokens, SSH private keys, or vault passwords.
- Keep actual infrastructure inventory local.
- Review files and commit history before publishing.
- Use the example inventory for public documentation.
Roadmap
- Introduce reusable Ansible roles.
- Add service and Kubernetes health checks.
- Expand automated testing.
- Add safe configuration-management playbooks.
- Explore Terraform integration for infrastructure provisioning.
Disclaimer
This is a homelab learning and portfolio project. Test automation against your own environment before using it in production.
