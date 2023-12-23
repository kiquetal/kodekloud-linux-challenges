#### Challenge 2

- Troubleshoot the issues with "yum/dnf" and make sure you are able to install the packages on "centos-host".

        add the nameserver of google to resolv.conf
        
        echo "namseserver 8.8.8.8"  >> /etc/resolv.conf


- Install "nginx" package.
- Install "firewalld" package.

        sudo yum install nginx firewalld

- Configure reverse proxy nginx for a web-app locate in /home/bob/go-app
the web-app is located in /home/bob/go-app


        location / {
        proxy_pass <http://localhost:8080>;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        }

- Restart nginx service

        sudo systemctl restart nginx

- Start and Enable "nginx" service.

        sudo systemctl enable nginx
        sudo systemctl start nginx



