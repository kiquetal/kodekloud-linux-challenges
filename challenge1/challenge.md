#### Challenge 1

- Create a group called "dba_users" and add the user called 'bob' to this group

      sudo groupadd dba_users
      sudo usermod -aG dba_users bob

- Install the correct packages that will allow the use of "lvm" on the centos machine.

      sudo yum install lvm2

- Create a Physical Volume for "/dev/vdb"

      sudo pvcreate /dev/vdb

- Create a Physical Volume for "/dev/vdc"

      sudo pvcreate /dev/vdc

- Create a volume group called "dba_storage" using the physical volumes "/dev/vdb" and "/dev/vdc"

      sudo vgcreate dba_storage /dev/vdb /dev/vdc


- Create an "lvm" called "volume_1" from the volume group called "dba_storage". Make use of the entire space available in the volume group

      sudo lvcreate -l 100%FREE -n volume_1 dba_storage

Ensure that the mountpoint "/mnt/dba_storage" has the group ownership set to the "dba_users" group
Ensure that the mount point "/mnt/dba_storage" has "read/write" and execute permissions for the owner and group and no permissions for anyone else.

      sudo mkdir /mnt/dba_storage
      sudo chown :dba_users /mnt/dba_storage
      sudo chmod 770 /mnt/dba_storage

Format the lvm volume "volume_1" as an "XFS" filesystem
Mount the filesystem at the path "/mnt/dba_storage".
Make sure that this mount point is persistent across reboots with the correct default options.

      sudo mkfs.xfs /dev/dba_storage/volume_1
      sudo mount /dev/dba_storage/volume_1 /mnt/dba_storage
      sudo echo "/dev/dba_storage/volume_1 /mnt/dba_storage xfs defaults 0 0" >> /etc/fstab

using fdisk -l

It didnt work, we should use /dev/mapper/dba_storage-volume_1
