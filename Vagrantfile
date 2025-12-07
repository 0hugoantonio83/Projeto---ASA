# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Configurações Globais
  config.vm.box = "debian/bookworm64"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.linked_clone = true
    v.check_guest_additions = false
  end
  config.trigger.before :"Vagrant::Action::Builtin::WaitForCommunicator", type: :action do |t|
    t.warn = "Iterrompe o servidor dhcp do virtualbox"
    t.run = {inline: "vboxmanage dhcpserver stop --interface vboxnet0"}
  end

  # Servidor de Arquivos
  config.vm.define "arq" do |arq|
    arq.vm.hostname = "arq.evandi.hugo.devops"
    arq.vm.network :private_network, ip: "192.168.56.138"
    (1..3).each do |x|
      arq.vm.disk :disk, size: "10GB", name: "disk-#{x}"
    end

    arq.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbooks/arq/arq_import.yml"
    end
  end

  # Servidor de Banco de Dados
  config.vm.define "db" do |db|
    db.vm.hostname = "db.evandi.hugo.devops"
    db.vm.network :private_network, mac: "0800273A0002", type: "dhcp"

    db.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook/db/db_import.yml"
    end
  end
  
  # Servidor de Aplicação
  config.vm.define "app" do |app|
    app.vm.hostname = "app.evandi.hugo.devops"
    app.vm.network :private_network, mac: "0800273A0003", type: "dhcp"
    app.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook/app/app_import.yml"
    end
  end

  # Host Cliente
  config.vm.define "cli" do |cli|
    cli.vm.hostname = "cli.evandi.hugo.devops"
    cli.vm.network :private_network, type: "dhcp"
    cli.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
    cli.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook/cli/cli_import.yml"
    end
  end
end
