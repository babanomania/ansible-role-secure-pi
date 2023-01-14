ansible-role-secure-pi
=========

This is an ansible-playbook to setup an secure raspberry-pi. Below are the features.


- Change the password of the pi user
- Ensure Root cannot login via ssh
- Disable password based login
- Install & enable ufw and fail2ban
- Set default and ssh firewall rules

Requirements
------------


1. **Prepare a Complex Password**

      This complex password will be updated as the password for the default user, but you need to encrypt the password, [click here](
  https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module) to see how to create encrypted passwords for the user module

2. **List ports to open**

    Identify which ports you want to open from your raspberry pi. Usually port 22 is required so that you can ssh into it and check. If you're planng to setup a web server, generally port 80 or 443 is needed
'

Role Variables
--------------


| Variable Name | Description | Default Value |
|--|--|-- |
| pi_custom_password | encoded password for ssh user| |
| ports_allow | list of ports to open |22, 80 | 
|ensure_autoupdate| flag to enable disable os autoupdate| true | 


Example Playbook
----------------

```yaml
---
- hosts: raspberrypi

  vars:
    # password used here is 'raspberry'
    - pi_custom_password: $6$c04cOXDbcDZ$fobZpDfUp1gOfICS9B5MNmzr9BnNL8gzjPBZnfoYLG/VCYSXFChljrMgczA9WI.TdNXIHtSCVKEJ36suDK1s4/
    - ports_allow:
      - 22
      - 80

  roles:
    - role: 'babanomania.secure_pi'
```

Tests
-----

Below are the steps to test this role

1. Copy the file __test/example.inventory.ini__ to __tests/inventory.ini__
2. Change the ip and username in the __tests/inventory.ini__ file to your raspberry pi's ip and default ssh user.
3. Ensure passwordless ssh is setup between your host and the raspberry pi
4. Run the below command

```bash
ansible-playbook -i tests/inventory tests/test.yml
```

License
-------

MIT
