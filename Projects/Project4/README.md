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
