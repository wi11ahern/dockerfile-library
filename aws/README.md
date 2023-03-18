# AWS
## Overview
Used for managing AWS infrastructure with Terragrunt and Terraform. Also sets ZSH as the default shell
for an improved terminal experience. 

## Installs
- Terraform v1.3.0
- Terragrunt v0.40.0
- Python 3.X
- AWS CLI
- mandoc
- unzip
- wget
- vim
- curl
- git
- oh-my-zsh

## Bash Aliases
- `tg` -- Executes Terragrunt binary.
- `tf` -- Executes Terraform binary.
- `gs` -- Executes `git status`.

## Building the Image
**No SSH Key Args**
```
docker build -t aws:latest .
```

**With SSH Key Args**
```
docker build -t aws:latest --build-arg SSH_PUBLIC_KEY="$(cat ~/.ssh/id_rsa.pub)" --build-arg SSH_PRIVATE_KEY="$(cat ~/.ssh/id_rsa)" .
```