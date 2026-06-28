## Instalação dos Pacotes

```bash
    sudo apt install openssh-server -y
    sudo apt install xrdp -y
    sudo apt install fail2ban -y
    sudo apt install remmina -y
```

## Teste de Acesso SSH
```bash
    ssh vendedor1@192.168.201.10
    # Senha: vendas123
```

## Configuração do SSH
```bash
    sudo nano /etc/ssh/sshd_config
    sudo systemctl restart ssh
    sudo systemctl status ssh
    sudo ss -tlnp | grep ssh
```

### /etc/ssh/sshs_conf
```bash
    Port 22
    PermitRootLogin no
    PasswordAuthentication yes
    PubkeyAuthentication yes
    MaxAuthTries 3
    ClientAliveInterval 300
    ClientAliveCountMax 2
```

## Configuração do xRDP
```bash
    sudo systemctl start xrdp
    sudo systemctl enable xrdp
    sudo systemctl status xrdp
    sudo ss -tlnp | grep 3389
    sudo systemctl restart xrdp
```

### /etc/xrdp/xrdp.ini
```bash
[globals]
    port=3389
    crypt_level=high
    channel_code=1

[xrdp1]
    name=sesman-X11rdp
    lib=libxup.so
    username=ask
    password=ask
    port=-1
```

## Configuração Fail2ban (segurança)
```bash
    sudo apt install fail2ban -y
    sudo nano /etc/fail2ban/jail.local
    sudo systemctl restart fail2ban
    sudo fail2ban-client status sshd
```

### /etc/fail2ban/jail.local
```bash
[sshd]
    enabled = true
    port = 22
    filter = sshd
    logpath = /var/log/auth.log
    maxretry = 3
    bantime = 3600
```

## Testes realizados na pasta /evidencias/terminal_server/