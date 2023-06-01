# Instalando e Configurando o PostgreSQL <img align="right" src="img/vtp_ifsp-pb.png" width="40%">

<img title="" src="img/postgresql.png" alt="">

Fazer a instalação usando o comando abaixo, **verifiquem a versão** do repositório.

```shell
sudo apt install postgresql-14 -y
```

## Habilitando usuário no PostgreSQL

```shell
sudo -u postgres psql
alter user postgres with encrypted password 'senha_da_nasa';
```

## Habilitando acesso remoto ao servidor PostgreSQL

#### Abra o arquivo

```shell
sudo vim /etc/postgresql/14/main/postgresql.conf
```

**Altere a linha**

```shell
# listen_addresses = 'localhost'                 # what IP address(es) to listen on
```

**Para**

```shell
listen_addresses = '*'                           # what IP address(es) to listen on
```

Retire o comentário e troque o <u>'localhost'</u> por <u>'*'</u>

Salve e feche o arquivo

------

#### Abra o arquivo

```shell
sudo vim /etc/postgresql/14/main/pg_hba.conf
```

**Que por padrão vem**

```shell
# "local" is for Unix domain socket connections only
local    all        all        peer
```

```shell
# IPv4 local connections:
host     all     all     127.0.0.1/32     scram-sha-256
```

```shell
# IPv6 local connections:
host     all     all     ::1/128         scram-sha-256
```

## Altere conforme necessário

**Assim ficará a regra de liberação:**

```shell
# IPv4 local connections:
host     all     all     0.0.0.0/0         scram-sha-256
```

<mark>**É possível também liberar o acesso apenas a uma rede específica:**</mark>

```shell
# IPv4 local connections:
host     all     all     192.168.1.0/24     scram-sha-256  
```

------

#### Abra o pgadmin4 ou software de preferência e faça a conexão usando as credenciais do servidor configurado.

#### Não esqueçam de liberar a porta no grupo de segurança ou na configuração de rede da sua Instância, de acordo com a nuvem utilizada ou VM Local.

<hr>

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)
