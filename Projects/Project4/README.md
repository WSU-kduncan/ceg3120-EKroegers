# Load Balancing TODOs
1. Config file

```bash
Host CoolServer
    HostName 10.0.1.10
    User ubuntu
    IdentityFile /home/ubuntu/.ssh/vockey.pem

Host CoolServerJr
    HostName 10.0.1.11
    User ubuntu
    IdentityFile /home/ubuntu/.ssh/vockey.pem
```

2. SSHing between systems
- using the config file previously shown, I can use `ssh CoolServer` or `ssh CoolServerJr` from the proxy

3. HAProxy configuration
- Load Balancer Documentation
	- Modified backend as follows:
```bash
backend blog-backend
   balance roundrobin
   mode http
   server CoolServer :80 check
   server CoolServerJr :80 check
```

4. Webserver 1 and 2 documentation
- had to modify index file hosted locally at /var/www/html/ on both servers, and had to modify permissions to properly save it
- `sudo ufw allow 'Apache'` is necessary to allow all traffic we need
- Restart using `sudo systemctl restart apache2`
- Used https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04 largely

5. Screenshots of webserver content
![Content numero uno](/Projects/Project4/images/img1.png)
![dos content](/Projects/Project4/images/img2.png)
