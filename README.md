# Ansible-vagrant

Shell provisioning script to bootstrap Ansible from within a Vagrant VM running on any OS.  
This is inspired and based on Jeff Geerlings [JJG-Ansible-Windows](https://github.com/geerlingguy/JJG-Ansible-Windows).  
This script can run Ansible playbooks from within the Linux VM through Vagrant.

Read more about other techniques for using Ansible within a Windows environment, on Server Check.in: [Running Ansible within Windows](https://servercheck.in/blog/running-ansible-within-windows).  
Find out how to run ansible directly from Host OS: [Vagrant Provisioning with ansible](https://docs.vagrantup.com/v2/provisioning/ansible.html).  
## Usage

An example Vagrantfile is added, you could either edit it or replace it with your own Vagrantfile.  
If you choose to replace the Vagrantfile, be sure to include the shell provisioner installing ansible on the guest and run the playbook, like in code below:

```ruby  
# Provisioning configuration for shell script.  
config.vm.provision "shell" do |sh|  
  sh.path = "ansible.sh"  
  sh.args = "provisioning/playbook.yml provisioning/inventory"  
end  
```  

The provisiong Files are located inside the `provisioning` Folder.

The example playbook runs once and creates a file `ansible_facts.txt` inside /root/ folder containing the VM facts.  
The file is created by running `ansible` from inside an ansible playbook.


## Licensing and More Info

Created by [Andreas Schmidt](http://www.andywhv.de/) in 2014. Licensed under the MIT license; see the LICENSE file for more info.
