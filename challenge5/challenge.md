- The "root" account is currently locked on "centos-host", please unlock it.
    
        sudo passwd -u root
- Make user "root" a member of "wheel" group

        sudo usermod -aG wheel root

- Edit the PAM configuration file for the "su" utility so that this utility only accepts the requests from the users that are part of the "wheel" group and the requests from the users should be accepted immediately, without asking for any password.
    
    vim /etc/pam.d/su
  
    Locate the line auth       sufficient   pam_rootok.so

    change for

    auth       sufficient   pam_wheel.so trust use_uid


- Install "mariadb" database server on this server and "start/enable" its service.

        sudo yum install mariadb-server
        sudo systemctl enable mariadb
        sudo systemctl start mariadb

  - Add a local DNS entry for the database hostname "mydb.kodekloud.com" so that it can resolve to "10.0.0.50" IP address.

        sudo vim /etc/hosts
        10.0.0.50    mydb.kodekloud.com

- Add an extra IP to eth1 interface on this system: 10.0.0.50/24

  sudo ip addr add 10.0.0.50/24 dev eth1


- Create and run a new Docker container based on the "nginx" image. The container should be named as "myapp" and the port "80" on the host should be mapped to the port "80" on the container.

        docker run -d --name myapp -p 80:80 nginx
      
- Create a bash script called "container-start.sh" under "/home/bob/" which should be able to "start" the "myapp" container. It should also display a message "myapp container started!"

        vim container-start.sh
        #!/bin/bash
        docker start myapp
        echo "myapp container started!"
        chmod +x container-start.sh
    
            
- 
Create a bash script called "container-stop.sh" under "/home/bob/" which should be able to stop the "myapp" container. It should also display a message "myapp container stopped!"

        vim container-stop.sh
        #!/bin/bash
        docker stop myapp
        echo "myapp container stopped!"
        chmod +x container-stop.sh


- Add a cron job for the "root" user which should run "container-stop.sh" script at "12am" everyday.

        sudo crontab -e
        0 0 * * * /home/bob/container-stop.sh

- Add a cron job for the "root" user which should run "container-start.sh" script at "8am" everyday.

        sudo crontab -e
        0 8 * * * /home/bob/container-start.sh

  - Change root mysql password
    
    First log into without password
        sudo mysql -u root
  
    then 

     ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';


    


