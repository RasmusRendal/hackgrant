# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/debian11"

  config.vm.provider :libvirt do |libvirt|
    libvirt.graphics_type = "spice"
    libvirt.channel :type => 'spicevmc', :target_name => 'com.redhat.spice.0', :target_type => 'virtio'
    libvirt.video_type = "qxl"
    libvirt.video_vram = 65536
    libvirt.memory = 4096
    libvirt.cpus = 4
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
