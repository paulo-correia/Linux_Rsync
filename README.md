# Rsync

rsync é um utilitário amplamente usado para manter cópias de um arquivo em dois sistemas de computadores ao mesmo tempo.

É normalmente encontrado em sistemas do tipo Unix e em funções como um programa de sincronização de arquivos e transferência de arquivos.

## Instalação

Toda a instalação é feita como **root**

### Debian

Instale o pacote rsync com o comando:

 `apt-get install rsync`

### CentOS  

instale o pacote rsync com o comando:

 `yum -y install rsync `

Instale o pacote xinted com o comando:

 `yum -y install xinetd`

## Configuração

### Debian

Edite o arquivo /etc/default/rsync

Altere de:

 `RSYNC_ENABLE=false`

Para:

 `RSYNC_ENABLE=true`

### CentOS  

Edite o arquivo /etc/xinetd.d/rsync

Altere de:

 `disable = yes`

Para:

 `disable = no`

### Comum a ambos

Crie o arquivo /etc/rsyncd.conf

Coloque o seguinte conteúdo:

 ```
max connections = 1
log file = /var/log/rsync.log
timeout = 300
[cache]
comment = Cache of Mongrels
path = /usr/local/cache
read only = no
list = yes
uid = nobody
gid = nogroup
list = yes
hosts allow = 127.0.0.0/8 192.168.0.0/24 
```

Salve e saia

Reinicie o serviço xinetd com o comando:

 `service xinetd restart`

## Testes

 `rsync rsync://ip do server`

Copiar de uma máquina (estando na máquina) para o server:

 `sudo rsync -v -e ssh arquivo usuario@ip do server:/caminho`

Copiar do server para uma máquina (estando na máquina):

 `sudo rsync -v -e ssh usuario@ip so server:/caminho/arquivo . `