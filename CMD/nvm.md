---
lastSync: Thu Nov 14 2024 13:51:19 GMT+0000 (Greenwich Mean Time)
---
## Install
### Install script
``` bash
git init
git clone git@github.com:nvm-sh/nvm.git
```
### Install error: Profile not found.
Problem: Tried ~/.bashrc, ~/.bash_profile, ~/.zshrc, and ~/.profile.
Solution: `touch ~/.bash_profile`, then run`./install.sh`
