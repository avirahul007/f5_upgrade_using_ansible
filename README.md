# Ease Way to Upgrade your BIGIP Devices

Ready Cookbook available for you to upgrade the firmware of your BIGIP devices. Hmmmm... you think it's simple and any F5 admin can do it!!! But what if I say "Let's do it using one touch option". Don't worry, it's very easy just follow below 

## Pre-requistes 

* Install Ansible (Version = or > 2.7 )
* Install python (Version = 2.7.18)
* Install sshpass (apt-get install sshpass) ==> Module used to intiate ssh connection with BIGIP devices
* Install Ansible Module from link: https://galaxy.ansible.com/f5networks/f5_modules 
* git clone https://github.com/avirahul007/f5_upgrade_using_ansible.git 


* Inventory list of all the f5s i needed to upgrade (active and standby) for the environment.

```
This is stored under /inventory/host file.
Create your own host file.
```

## upgrade.yaml taks that it is going to perform

The playbook perfoms the following actions:

* Checks the failover state of a BIG-IP system
* Prepares the BIG-IP system for an upgrade
* Uses a custom script to identify an available volume set number to use
* Runs a software upgrade
* Install the software on a new volume space.

Note: 
* I have set state parameter to "installed" but if you change it "activated" in the bigip_sotware_install task, the system will reboot the device. Hence, I recommend that you should perform this procedure during a maintenance window.

## How to use the playbook.

To run the playbook, perform the following procedure:

* Log in to your control machine.
* Change the working directory to the playbooks directory.
* To run the upgrade_bigip_software.yml playbook, enter the following command:
* ansible-playbook -i inventory upgrade.yaml

## Impacts of procedure: 

* The BIG-IP system briefly interrupts traffic on active systems when it reloads the configuration during license activation.
* There may be a performance impact when the BIG-IP system serves a high volume of traffic, and you upgrade a standalone system or the  active system in a device group.
* If the state parameter is set to activated in the bigip_sotware_install task, the system reboots the device. This interrupts traffic processing on an active system.
* F5 recommends that you perform this procedure during a maintenance window.


!!!!Please share your feedback to help me to improve further!!!!

