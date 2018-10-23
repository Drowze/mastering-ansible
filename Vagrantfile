Vagrant.configure(2) do |config|

  # ssh settings
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo service ssh restart
  EOC

  config.vm.define("app01"){ |a| a.vm.box = "ubuntu/trusty64";}# a.vm.network('forwarded_port', guest: 22, host: 2222) }
  config.vm.define("app02"){ |a| a.vm.box = "ubuntu/trusty64";}# a.vm.network('forwarded_port', guest: 22, host: 2200) }
  config.vm.define("lb01") { |a| a.vm.box = "ubuntu/trusty64";}# a.vm.network('forwarded_port', guest: 22, host: 2201) }
  config.vm.define("db01") { |a| a.vm.box = "ubuntu/trusty64";}# a.vm.network('forwarded_port', guest: 22, host: 2202) }
end

