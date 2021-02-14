# Ansible Roles for Ubuntu Workstation

[![pre-commit badge][pre-commit-badge]][pre-commit] [![Conventional commits badge][conventional-commits-badge]][conventional-commits] [![Keep a Changelog v1.1.0 badge][keep-a-changelog-badge]][keep-a-changelog] [![MIT License Badge][license-badge]][license]
[![GitHub release (latest by date)][gh-release-badge]][changelog]

This repository has several `ansible roles and playbooks` that can be used to configure Ubuntu as a Workstation.

## pre-commit hooks

Read the [pre-commit hooks](docs/pre-commit-hooks.md) document for more info.

## git-chglog

Read the [git-chglog](docs/git-chlog.md) document for more info.

## TL;DR

If you just want to run the playbooks on this repo you just need to install `ansible` and configure it to use
on the remote hosts you want to.

Check [this](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) link for more info on how
to install `ansible`.

List of playbooks available:

| playbook            | description                                |
| ------------------- | ------------------------------------------ |
| base_utils.yml      | Install base utilities and pip packages    |
| cloud_tools.yml     | Install Azure, AWS and GCP(*) CLI tools    |
| collab_tools.yml    | Collaboration tools                        |
| dev_tools.yml       | Development tools                          |
| i3wm.yml            | Install i3 Window Manager                  |
| kube_tools.yml      | Kubernetes administration tools            |
| terraform_tools.yml | Terraform tools for linting and compliance |

(*) not yet implemented

**NOTE: Before running the playbooks ensure that your `inventory` is configured.**

run the playbooks:

```bash
ansible-playbook <playbook.yml>
```

to run the `i3wm.yml` playbook on `localhost` execute:

```bash
ansible-playbook -i localhost, i3wm.yml
```

## Requirements

This repository should be used from a Python Virtual Environment.

### Setup Python 3

Make sure versions are up-to-date and install git and ssh server:

```bash
sudo apt update
sudo apt -y upgrade
```

Check Python version:

```bash
python3 -V
```

Install essential tools for the development environment:

```bash
sudo apt install -y python3-pip build-essential libssl-dev libffi-dev python3-dev python3-venv git ssh
```

### Setup Virtual Environment

Create the Virtual Environment:

```bash
python3 -m venv venv
```

Activate the environment:

```bash
source venv/bin/activate
```

Install `requirements.txt`:

```bash
pip install --upgrade setuptools wheel pip
pip install -r requirements.txt
```

Install `community.general` collection for Ansible:

```bash
ansible-galaxy collection install community.general
```

You now have python virtual environment with all the dependencies installed and can start deploying the ansible roles.

### Configure Ansible

You should have `ssh` installed and running.

Create SSH key:

```bash
ssh-keygen -t rsa
```

Ensure sudo passwordless for the ansible user by creating a file
`/etc/sudoers.d/bcochofel` with the following contents:

```bash
bcochofel ALL=(ALL) NOPASSWD: ALL
```

### Install Ansible and Molecule manually

If you don't want to use the `requirements.txt` file you can install both `ansible` and `molecule` using the following commands:

```bash
python3 -m pip install wheel pytest testinfra flake8 pytest-testinfra pytest-flake8 cookiecutter
python3 -m pip install "molecule[ansible,lint,docker]"
# for snap module
ansible-galaxy collection install community.general
```

generate `requirements.txt` file using the following command:

```bash
pip freeze > requirements.txt
```

## Create new Ansible Role

### Ansible Role using custom Cookiecutter template

You can use custom [`cookiecutter`](https://github.com/cookiecutter/cookiecutter) templates with some pre-defined tasks or variables.
You can use [this](https://github.com/bcochofel/molecule-cookiecutter) repo for reference.

Go to the `roles` folder and execute the following commands:

```bash
cd roles/
cookiecutter gh:bcochofel/molecule-cookiecutter
```

answer the on-screen questions.

### Ansible Role using default template

To use the default template execute the following commands:

```bash
cd roles/
molecule init role -d docker <role-name>
```

* -d: docker driver

## How to test the Role

Change to the `role` folder.

### Create instance

```bash
molecule create
```

### List instances

```bash
molecule list
```

### Test Role against instance

```bash
molecule converge
```

### Manual inspection

```bash
molecule login
```

### Run Verification steps

```bash
molecule verify
```

### Run Lint steps

```bash
molecule lint
```

### Destroy instance

```bash
molecule destroy
```

### Run all tests

```bash
molecule test
```

## References

* [Molecule Documentation](https://molecule.readthedocs.io/en/latest/index.html)
* [Molecule Getting Started Guide](https://molecule.readthedocs.io/en/latest/getting-started.html)
* [Use custom Ansible role templates with Molecule](https://megamorf.gitlab.io/2018/12/18/use-custom-role-templates-with-molecule/)
* [Ansible is now default test verifier in Molecule](https://loncar.net/posts/ansible-is-now-default-test-verifier-in-molecule/)
* [Testing your Ansible roles with Molecule](https://www.jeffgeerling.com/blog/2018/testing-your-ansible-roles-molecule)

[pre-commit]: https://github.com/pre-commit/pre-commit
[pre-commit-badge]: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white
[conventional-commits-badge]: https://img.shields.io/badge/Conventional%20Commits-1.0.0-green.svg
[conventional-commits]: https://conventionalcommits.org
[keep-a-changelog-badge]: https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735
[keep-a-changelog]: https://keepachangelog.com/en/1.0.0/
[license]: ./LICENSE
[license-badge]: https://img.shields.io/badge/license-MIT-green.svg
[gh-release-badge]: https://img.shields.io/github/v/release/bcochofel/ansible-ubuntuwst-roles?color=green
[changelog]: ./CHANGELOG.md
