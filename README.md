# FS SERVICOS

## Intro 

### O que é?

Playbook para criar 

- Object Storage via [Minio](http://minio.io) 
- FTP via [vsftpd](https://security.appspot.com/vsftpd.html)

### Para que sirve?

Precisamos, mesmo estando num ambiente on-premise, usar servicos cloud native. Nesse sentido, não podemos seguir usando Samba para poder escrever e ler arquivos de um windows file-server, precisamos então ter um servidor intermediario q nos permita chegar ate o servidor windows file server 

## Playbook 

### Instalação

```
sudo ansible-playbook site.yml -i inventory-prd  -e deploy_docker=true
```

###  Servicos 

#### FTP

Servidor  `ftp-servicos.docs-planet.site`


#### MINIO

Criando as credenciais para um minio server

```sh
export MINIO_ACCESS_KEY=$(date | md5sum | head -c 16 | awk '{ print toupper($0) }')
export MINIO_SECRET_KEY=$(date | md5sum | head -c 16 | awk '{ print toupper($0) }')
```

Com esses dados, modifique as variaveis do playbook, nos 3 ambientes. PRD: `group_vars/prd/minio.yml`

Rode o playbook 

```
sudo ansible-playbook site.yml -i inventory-prd -t minio-nginx
```
