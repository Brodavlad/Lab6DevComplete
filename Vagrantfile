ENV["VAGRANT_EXPERIMENTAL"] = "disks"
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"

    config.vm.disk :disk, size: "300MB", name: "extra_storage1"
    config.vm.disk :disk, size: "300MB", name: "extra_storage2"
    config.vm.disk :disk, size: "300MB", name: "extra_storage3"
    config.vm.disk :disk, size: "300MB", name: "extra_storage4"  


  config.vm.provision "shell", inline: <<-SHELL
    pvcreate /dev/sdc /dev/sdd /dev/sde /dev/sdf
    vgcreate vg01 /dev/sdc /dev/sdd /dev/sde /dev/sdf
    lvcreate -l 100%FREE vg01 /dev/sdc /dev/sdd -n lv0
    lvcreate -l 100%FREE vg01 /dev/sde /dev/sdf -n lv1
    mkfs.ext4 /dev/vg01/lv0 
    mkfs.ext4 /dev/vg01/lv1 
    mkdir -p /mnt/vol0 /mnt/vol1
    echo '/dev/vg01/lv0 /mnt/vol0 ext4 defaults 0 0' >>/etc/fstab
    echo '/dev/vg01/lv1 /mnt/vol1 ext4 defaults 0 0' >>/etc/fstab
    mount -a
  SHELL

end
