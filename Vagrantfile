# Setup a virtualbox vm with ansible provisioning
#
domain = 'example.dev'

nodes = [
  { :hostname => 'mybox', :ip => '192.168.0.42', :box => 'ubuntu/trusty64', :ram => 512, :box_url => 'http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box' },
]
Vagrant::configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.box = node[:box]
      node_config.vm.box_url = node[:box_url]
      node_config.vm.hostname = node[:hostname] + '.' + domain
      node_config.vm.network "private_network", ip: node[:ip]

      memory = node[:ram] ? node[:ram] : 512;
      node_config.vm.provider "virtualbox" do |vb|
        vb.name = node[:hostname];
        vb.memory = memory.to_s;
		    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
	    end
      # Provisioning configuration for shell script.
      node_config.vm.provision "shell" do |sh|
        sh.path = "ansible.sh"
        sh.args = "provisioning/playbook.yml provisioning/inventory"
      end
    end
  end
end
