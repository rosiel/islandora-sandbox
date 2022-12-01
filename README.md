# "Islandora Sandbox"

This is a Composer project used by [Isle-DC](https://github.com/Islandora-Devops/isle-dc) and the [Islandora Playbook](https://github.com/Islandora-Devops/islandora-playbook) in order to install a Drupal site using the [Islandora Install Profile Demo](https://github.com/Islandora-Devops/islandora_install_profile_demo).
Use with caution.

Do not confuse this with [Sandbox](https://github.com/Islandora-Devops/sandbox), the repository that generates the live online [Sandbox](https://sandbox.islandora.ca).

## Testing Instructions

This is how you deploy a different fork (TESTFORK) and branch (TESTBRANCH) of this repo. This is useful for testing alternate forks and branches of the Islandora Install Profile.

### ISLE-DC

Open `Makefile` and edit the line that refers to `islandora-sandbox`. Currently it looks like (beginning omitted for clarity)
```
... 'git clone -b main https://github.com/Islandora-Devops/islandora-sandbox /tmp/codebase; mv /tmp/codebase/* /home/root;'; \
```
Change it to 
```
... 'git clone -b TESTBRANCH https://github.com/TESTFORK/islandora-sandbox /home/root;'; 
``` 
Aside from changing the branch to TESTBRANCH and the fork to TESTFORK, cloning the sandbox _directly_ into /var/www/html/drupal leaves the Islandora Sandbox's git history available, so you it's easier to push updates to the TESTFORK and TESTBRANCH. This is not recommended in production.


### Playbook

Open `vars/demo.yml` and set 
```
drupal_deploy_repo: https://github.com/islandora-devops/islandora-sandbox
drupal_deploy_version: install-profile
``` 
to
```
drupal_deploy_repo: https://github.com/TESTFORK/islandora-sandbox
drupal_deploy_version: TESTBRANCH
```
Make sure `"demo"` is the `"ISLANDORA_INSTALL_PROFILE"` in the Vagrantfile, and `vagrant up`.
