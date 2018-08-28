Vagrant.configure("2") do |config|
   config.vm.box = "centos/7"
   config.vm.provision "shell", path: "install.sh"  
   
   config.vm.define "cdbox" do |cd|
    cd.vm.hostname = "web"
    cd.vm.hostname = "testing-machine"
    cd.vm.network "public_network", ip: "172.16.202.96"
   end

   config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", 2500]
      v.customize ["modifyvm", :id, "--cpus", "2"]
   end
 
   if File.exists?(File.join(Dir.home, ".ssh" , "id_rsa.pub"))
      ssh_key= File.read(File.join(Dir.home, ".ssh","id_rsa.pub"))
     
           config.vm.provision :shell, :inline =>"
           echo 'Copying Local Ssh Keys to the VM For Provisioning'
           mkdir -p /home/vagrant/.ssh
           chmod -R 750 /home/vagrant/.ssh
           echo '#{ssh_key}' >> /home/vagrant/.ssh/authorized_keys && chmod -R 644 /home/vagrant/.ssh/authorized_keys          
           ", privileged: false
  else
      raise Vagrant::Errors::VagrantError, "\n SSH keys Not Found"
  end

end
