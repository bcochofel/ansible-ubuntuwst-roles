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

# Requirements

This repository should be used from a Python Virtual Environment.

## Install Podman

Molecule can use [podman](https://podman.io/) for testing. If you want to use `podman` you need to install it:

```bash
# Ubuntu (19.10, 19.04 and 18.04)
. /etc/os-release
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/x${NAME}_${VERSION_ID}/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"
wget -nv https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/x${NAME}_${VERSION_ID}/Release.key -O Release.key

sudo apt-key add - < Release.key
sudo apt-get update -qq
sudo apt-get -y install podman
```

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

You now have python virtual environment with all the dependencies installed and can start deploying the ansible roles.

## Install Ansible and Molecule

If you don't want to use the `requirements.txt` file you can install both `ansible` and `molecule` using the following commands:

```bash
python3 -m pip install wheel pytest testinfra flake8 pytest-testinfra pytest-flake8
python3 -m pip install "molecule[ansible,lint,docker,podman]"
```

generate `requirements.txt` file using the following command:

```bash
pip freeze > requirements.txt
```

# Create new Ansible Role

## Ansible Role using custom Cookiecutter template

## Ansible Role using default template

# References

* [Molecule Documentation](https://molecule.readthedocs.io/en/latest/index.html)
* [Molecule Getting Started Guide](https://molecule.readthedocs.io/en/latest/getting-started.html)
* [Use custom Ansible role templates with Molecule](https://megamorf.gitlab.io/2018/12/18/use-custom-role-templates-with-molecule/)
* [Ansible is now default test verifier in Molecule](https://loncar.net/posts/ansible-is-now-default-test-verifier-in-molecule/)
