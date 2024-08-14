# Ansible Molecule Demo

This is a sample collection to demonstrate how molecule works.

The molecule code itself was taken from the [molecule documentation](https://ansible.readthedocs.io/projects/molecule/examples/podman/).

This repo is the fully functioning collection with molecule. You should comment out the contents of verify.yml and tasks/main.yml in the role before starting the demo.

I've included an mp4 video of the demo if you would rather play that.

Typically I follow this "script" to demo molecule:

```console
# show ansible.cfg and setup an ansible-collections path to develop a collection

# show the following files in the extensions/molecule/default directory
molecule.yml
requirements.yml
create.yml
destroy.yml
converge.yml
verify.yml

# create the ephemeral containers
$ molecule create

# demonstrate that they exist
$ podman ps

# show that molecule does not do much without test
$ molecule verify

# edit verify.yml to test for the presence of the httpd package
# and then run verify again to see it fail
$ molecule verify

# edit tasks/main.yml in the role to install the httpd package
# and then run converge
$ molecule converge

# login to the container and see the package installed
$ molecule login -h ubi9
$ rpm -qa | grep httpd
$ <CTRL-D> to exit container

# run verify again to see if it passes
$ molecule verify

# test for idempotence
$ molecule idempotence

# clean up the ephemeral containers
$ molecule destroy

# show that the ephemeral containers do not exist
$ podman ps

# run the full suite of tests
# this is what you would run inside a pipeline
$ molecule test
```
