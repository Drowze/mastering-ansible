Vagrant.configure(2) do |config|

  # ssh settings
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo service ssh restart
  EOC

  {
    'app01' => '192.168.1.254',
    'app02' => '192.168.1.253',
    'lb01' => '192.168.1.252',
    'db01' => '192.168.1.251'
  }.each do |name, ip_address|
    config.vm.define name do |a|
      a.vm.box = 'ubuntu/trusty64'
      a.vm.hostname = name
      a.vm.network 'private_network', ip: ip_address
    end
  end
end

