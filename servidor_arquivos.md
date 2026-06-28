## Arquivo de Configuração Principal:
### sudo nano /etc/samba/smb.conf
```bash
[global]
   workgroup = WORKGROUP
   server string = Servidor TechNet
   netbios name = SERVIDOR
   interfaces = 127.0.0.1 192.168.201.10
   bind interfaces only = yes
   security = user
   map to guest = bad user
   guest account = nobody
   log file = /var/log/samba/log.%m
   max log size = 1000

[publico]
   path = /srv/samba/publico
   browseable = yes
   read only = no
   guest ok = yes
   create mask = 0666
   directory mask = 0777
   force group = nogroup

[vendas]
   path = /srv/samba/vendas
   browseable = yes
   read only = no
   guest ok = no
   valid users = vendedor1, vendedor2
   create mask = 0660
   directory mask = 0770
   force user = root
   force group = root

[rh]
   path = /srv/samba/rh
   browseable = yes
   read only = no
   guest ok = no
   valid users = recursos
   create mask = 0660
   directory mask = 0770

[ti]
   path = /srv/samba/ti
   browseable = yes
   read only = no
   guest ok = no
   valid users = tecnico
   create mask = 0660
   directory mask = 0770
```

### Criação dos diretórios
```bash
sudo mkdir -p /srv/samba/{publico,vendas,rh,ti}
sudo chmod 1777 /srv/samba/publico
sudo chown nobody:nogroup /srv/samba/publico
sudo chmod 770 /srv/samba/vendas
sudo chown root:root /srv/samba/vendas
sudo chmod 770 /srv/samba/rh
sudo chown root:root /srv/samba/rh
sudo chmod 770 /srv/samba/ti
sudo chown root:root /srv/samba/ti
```

### Criação dos Usuários e senhas
```bash
sudo useradd -m -s /bin/bash vendedor1
sudo useradd -m -s /bin/bash vendedor2
sudo useradd -m -s /bin/bash recursos
sudo useradd -m -s /bin/bash tecnico
sudo useradd -m -s /bin/bash admin

echo "vendedor1:vendas123" | sudo chpasswd
echo "vendedor2:vendas123" | sudo chpasswd
echo "recursos:rh123" | sudo chpasswd
echo "tecnico:ti123" | sudo chpasswd
echo "admin:admin123" | sudo chpasswd
```

# Testes realizados na pasta /evidencias/servidor_arquivos/
