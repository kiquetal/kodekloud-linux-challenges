### Challenge 3

- Create a user called "david" , change his login shell to "/bin/zsh" and set "D3vUd3raaw" password for this user.
   Make user "david" a member of "admins" group.

        sudo useradd -s /bin/zsh david
        sudo passwd david
        sudo usermod -aG admins david

- Create a user called "natasha" , change her login shell to "/bin/zsh" and set "DwfawUd113" password for this user.
  Make user "natasha" a member of "admins" group.
    
        sudo useradd -s /bin/zsh natasha
        sudo passwd natasha
        sudo usermod -aG admins natasha

- Make sure all users under "admins" group can run all commands with "sudo" and without entering any password.

        sudo visudo
        %admins ALL=(ALL) NOPASSWD: ALL

- Give some additional permissions to "admins" group on "/data" directory so that any user who is the member the "admins" group has "full permissions" on this directory.

        sudo chgrp -R admins /data
        sudo chmod -R 770 /data

        sudo setfacl -m g:admins:rwx /data

-Make sure all users under "admins" group can run all commands with "sudo" and without entering any password.

        sudo visudo
        %admins ALL=(ALL) NOPASSWD: ALL

- Edit the disk quota for the group called "devs". Limit the amount of storage space it can use (not inodes). Set a "soft" limit of "100MB" and a "hard" limit of "500MB" on "/data" partition.

        sudo edquota -g devs

        100M 500M
- Make sure all users under "devs" group can only run the "dnf" command with "sudo" and without entering any password.

        sudo visudo
        %devs ALL=(ALL) NOPASSWD: /usr/bin/dnf

- Configure a "resource limit" for the "devs" group so that this group (members of the group) can not run more than "30 processes" in their session. This should be both a "hard limit" and a "soft limit", written in a single line.

   sudo bash -c 'echo "session required pam_limits.so" >> /etc/pam.d/common-session'
   sudo bash -c 'echo "@devs hard nproc 30" >> /etc/security/limits.conf'
   sudo bash -c 'echo "@devs soft nproc 30" >> /etc/security/limits.conf'
