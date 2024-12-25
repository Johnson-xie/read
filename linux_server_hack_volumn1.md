





## 2024-12-25

ssh-agent

```shell
eval `ssh-agent`

ssh-add -l

ssh-add {private-key}

ssh -A root@{first_node}

ssh root@{second}

# local config: ~/.ssh/config
Host *
    ForwardAgent yes

#
ssh k8-{node-behind-bastion}
ssh root@{internal-node}


ssh {xq-cd}
ssh root@{xq-sg-ip}
```



```shell
cat config_template
Host *
    ForwardAgent yes

# login into bastion
Host singapore
    User root
    HostName {IP}
    Port 36000
    IdentityFile ~/.ssh/{private_key}.pem

# lgame
Host sg-xx-*
    User root
    ProxyCommand ssh singapore -W $(sed 's/sg-xx-//g' <<<  %h):%p
    Port 36000
    IdentityFile ~/.ssh/{private_key}.pem


# k8s
Host k8-*
    User root
    ProxyCommand ssh singapore -W $(sed 's/k8-//g' <<<  %h):%p
    Port 22
    IdentityFile ~/.ssh/{private_key}.pem

Host xq-sg
    User root
    HostName 43.156.228.157
    Port 22
    IdentityFile ~/.ssh/xq.pem
Host xq-cd
    User root
    HostName 43.136.167.53
    Port 22
    IdentityFile ~/.ssh/xq.pem
```

