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
- had to modify index file at /var/www/html/ on both servers, and had to modify permissions to properly save it
- `sudo ufw allow 'Apache'` is necessary to allow all traffic we need

