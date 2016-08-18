# ansible-examples
Ansible with vagrant
=======================================

Notes:
------
* Please make sure that you added a public key(id_rsa.pub) into vagrant

* File hosts: (node.vm.network :private_network, ip: "22.22.22.22" in VagrantFile)
[webserver]
22.22.22.22 ansible_ssh_port=22 ansible_ssh_user=vagrant ansible_ssh_private_key_file=~/.ssh/id_rsa

* Check server:
	+ $ansible -i hosts webserver -m ping
		Result
		22.22.22.22 | SUCCESS => {
		    "changed": false,
		    "ping": "pong"
		}
	+ $ansible -i hosts webserver -a "/bin/echo hello"
		Result
		22.22.22.22 | SUCCESS | rc=0 >>
		hello

* Run playbook:
	+vagrant$ ansible-playbook -i ../ansible-nginx/hosts ../ansible-nginx/site.yml


Errors and Resolving:
---------------------
* Fatal: [22.22.22.22]: FAILED! => {"failed": true, "msg": "Timeout (12s) waiting for privilege escalation prompt: "}
	Fixed: set “sudo: yes” into site.yml
