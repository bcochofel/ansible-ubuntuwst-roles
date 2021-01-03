# Ansible Roles for Ubuntu Workstation

[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![GitHub license](https://img.shields.io/github/license/bcochofel/ansible-ubuntuwst-roles.svg)](https://github.com/bcochofel/ansible-ubuntuwst-roles/blob/master/LICENSE)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/bcochofel/ansible-ubuntuwst-roles)](https://github.com/bcochofel/ansible-ubuntuwst-roles/tags)
[![GitHub issues](https://img.shields.io/github/issues/bcochofel/ansible-ubuntuwst-roles.svg)](https://github.com/bcochofel/ansible-ubuntuwst-roles/issues/)
[![GitHub forks](https://img.shields.io/github/forks/bcochofel/ansible-ubuntuwst-roles.svg?style=social&label=Fork&maxAge=2592000)](https://github.com/bcochofel/ansible-ubuntuwst-roles/network/)
[![GitHub stars](https://img.shields.io/github/stars/bcochofel/ansible-ubuntuwst-roles.svg?style=social&label=Star&maxAge=2592000)](https://github.com/bcochofel/ansible-ubuntuwst-roles/stargazers/)

This repository has several `ansible roles and playbooks` that can be used to configure Ubuntu as a Workstation.

# GIT Hooks

* [`pre-commit`](https://pre-commit.com/#install)

You can also use [pre-commit](https://pre-commit.com/#install). After installing
`pre-commit` just execute:

```ShellSession
pre-commit install
```

You can run specific hooks on all files:

```ShellSession
pre-commit run terraform-fmt --all-files
```

You can force all the hooks to run with the following command:

```ShellSession
pre-commit run --all-files
```

# TL;DR

If you just want to run the playbooks on this repo you just need to install `ansible` and configure it to use
on the remote hosts you want to.

Check [this](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) link for more info on how
to install `ansible`.

List of playbooks available:

| playbook | description |
| -------- | ----------- |
| base_utils.yml | Install base utilities and pip packages |
| i3wm.yml | Install i3 Window Manager |

**NOTE: Before running the playbooks ensure that your `inventory` is configured.**

run the playbooks:

```bash
ansible-playbook <playbook.yml>
```

to run the `i3wm.yml` playbook on `localhost` execute:

```bash
ansible-playbook -i localhost, i3wm.yml
```

# Requirements

This repository should be used from a Python Virtual Environment.

## Setup Python 3

Make sure versions are up-to-date:

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
sudo apt install -y python3-pip build-essential libssl-dev libffi-dev python3-dev python3-venv
```

## Setup Virtual Environment

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
pip install -r requirements.txt
```

Install `community.general` collection for Ansible:

```bash
ansible-galaxy collection install community.general
```

You now have python virtual environment with all the dependencies installed and can start deploying the ansible roles.

## Install Ansible and Molecule

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

# Create new Ansible Role

## Ansible Role using custom Cookiecutter template

You can use custom [`cookiecutter`](https://github.com/cookiecutter/cookiecutter) templates with some pre-defined tasks or variables.
You can use [this](https://github.com/bcochofel/molecule-cookiecutter) repo for reference.

Go to the `roles` folder and execute the following commands:

```bash
cd roles/
cookiecutter gh:bcochofel/molecule-cookiecutter
```

answer the on-screen questions.

## Ansible Role using default template

To use the default template execute the following commands:

```bash
cd roles/
molecule init role -d docker <role-name>
```

* -d: docker driver

# How to test the Role

Change to the `role` folder.

## Create instance

```bash
molecule create
```

## List instances

```bash
molecule list
```

## Test Role against instance

```bash
molecule converge
```

## Manual inspection

```bash
molecule login
```

## Run Verification steps

```bash
molecule verify
```

## Run Lint steps

```bash
molecule lint
```

## Destroy instance

```bash
molecule destroy
```

## Run all tests

```bash
molecule test
```

# References

* [Molecule Documentation](https://molecule.readthedocs.io/en/latest/index.html)
* [Molecule Getting Started Guide](https://molecule.readthedocs.io/en/latest/getting-started.html)
* [Use custom Ansible role templates with Molecule](https://megamorf.gitlab.io/2018/12/18/use-custom-role-templates-with-molecule/)
* [Ansible is now default test verifier in Molecule](https://loncar.net/posts/ansible-is-now-default-test-verifier-in-molecule/)
* [Testing your Ansible roles with Molecule](https://www.jeffgeerling.com/blog/2018/testing-your-ansible-roles-molecule)
