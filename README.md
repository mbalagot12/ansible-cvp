# CVP_Ansible_Modules
Pre Release Work in progress Anisble modules for CVP

## Modules overview

**cv_configlet**

 - `add`, `delete`, and `show` configlets.

  Configlets can be created, deleted then added to containers or devices. - also in cv_devices as required to move devices between containers
  Any Tasks that are generated as a result will be returned.
  Need to add the option to check (CVP verify) the configuration contained in the Configlet

**cv_container**
 - `add`, `delete`, and `show` containers

Containers can be created or deleted.

- Example playbook for container creation: [playbook.container.add.yaml](tests/playbook.container.add.yaml) 
- Example playbook for container deletion: [playbook.container.delete.yaml](tests/playbook.container.delete.yaml) 


**cv_device**
 - `add`, `delete`, and `show` devices

  Devices can be deployed from the undefined container to a provisioned container or moved from one container to another using the add functionality and specifying the target container. Configlets can be added to devices using add and specifying the current parent container.
  Devices can be Removed from CVP using the delete option and specifying "CVP" as the container, equivalent to the REMOVE GUI option.
  Devices can be reset and moved to the undefined container using the delete option and specifying "RESET" as the container.
  Configlets can be removed from a device using the delete option and specifying the configs to be removed and the current parent container as the container.
  show option provide device data and current config.

**cv_image [testing]**
 - `add`, `delete`, and `show` image bundles

  Image bundles must exist in CVP already, this module will allow the manipulation of them in CVP.
  Add and Delete will allow bundles to be applied or removed from Containers and devices
  Show will provide information on the contents of the image bundle.

**cv_tasks [Future]**
 - `add`, `delete`, and `show` tasks

  Tasks must exist in CVP already, this module will allow the manipulation of them in CVP.
  Add and Delete will allow Tasks to be executed or Canceled
  Show will provide information on the current Status or a Task.

## Installation

**CvpRac**

  To use these modules you will need cvprac.
  The official version can be found here: [Arista Networks cvprac](https://github.com/aristanetworks/cvprac)
  CVPRACV2 in this repository is a tweaked version with additional functionality that has been requested in the official version.

  Installation notes are available on [installation page](INSTALLATION.md)

> Note: Repository is a pre-release work. Installation is requires to run non standard process for python and ansible.

## Example playbook

This example outlines how to use Ansible to create a device container on Arista CloudVision.

```yaml
---
- name: Test cv_container
  hosts: cvp
  connection: local
  gather_facts: no
  tasks:
    - name: Create a container on CVP.
      cv_container:
        host: '{{ansible_host}}'
        username: '{{cvp_username}}'
        password: '{{cvp_password}}'
        protocol: https
        container: ansible_container
        parent: Tenant
        action: add
```


## Resources

  Other CVP Ansible modules can be found here: [Arista EOS+ Ansible Modules](https://github.com/arista-eosplus/ansible-cloudvision)

## License

Project is published under [BSD License](LICENSE).

## Ask question or report issue

Please open an issue on Github this is the fastest way to get an answer.

## Contribute

Contributing pull requests are gladly welcomed for this repository. If you are planning a big change, please start a discussion first to make sure we’ll be able to merge it.