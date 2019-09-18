Vagrant.configure("2") do |config|
   config.vm.box_check_update = false
   config.ssh.insert_key = false
   config.hostmanager.enabled = true
   config.hostmanager.manage_host = false
   config.hostmanager.manage_guest = true

   (1..1).each do |i|
        config.vm.define "sandbox.cloudera.com" do |node|
            # 设置虚拟机的Box
            node.vm.box = "centos7.5"
            # 设置虚拟机的主机名
            node.vm.hostname="sandbox.cloudera.com"
            # 设置虚拟机的IP
            node.vm.network "private_network", ip: "192.168.56.#{100+i}"
            # 设置主机与虚拟机的共享目录
            # node.vm.synced_folder "~/Documents/vagrant/share", "/home/vagrant/share"

            node.vm.provider "virtualbox" do |v|
                # 设置虚拟机的名称
                v.name = "sandbox.cloudera.com"
                # 设置虚拟机的内存大小
                v.memory = 8192
                # 设置虚拟机的CPU个数
                v.cpus = 4
            end
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "site.yml"
                ansible.verbose="vvv"
                ansible.groups = {
                  "worker_servers" => ["sandbox.cloudera.com"],
                  "master_servers" => ["sandbox.cloudera.com"],
                  "edge_servers" => ["sandbox.cloudera.com"],
                  "gateway_servers" => ["sandbox.cloudera.com"],
                  "utility_servers" => ["sandbox.cloudera.com"],
                  "cdh_servers" => ["sandbox.cloudera.com"],
                  "db_server" => ["sandbox.cloudera.com"],
                  "scm_server" => ["sandbox.cloudera.com"],
                  "krb5_server" => ["sandbox.cloudera.com"]

                }
            end
        end
   end
end