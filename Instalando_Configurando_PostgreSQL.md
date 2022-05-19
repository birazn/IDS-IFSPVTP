# Instalando e Configurando o PostgreSQL

<img title="" src="img/postgresql.png" alt="">

Fazer a instalação usando o comando abaixo, **verifiquem a versão** do repositório.

```shell
sudo apt install postgresql-12 -y
```

## Habilitando usuário no PostgreSQL

```shell
sudo -u postgres psql
alter user postgres with encrypted password 'senha_da_nasa';
```

## Habilitando acesso remoto ao servidor PostgreSQL

#### Abra o arquivo

```shell
sudo nano /etc/postgresql/12/main/postgresql.conf
```

**Altere a linha**

```shell
# listen_addresses = 'localhost'                 # what IP address(es) to listen on
```

**Para**

```shell
listen_addresses = '*'                            # what IP address(es) to listen on
```

Retire o comentário e troque o <u>'localhost'</u> por <u>'*'</u>

Salve e feche o arquivo

------

#### Abra o arquivo

```shell
sudo nano /etc/postgresql/12/main/pg_hba.conf
```

**Que por padrão vem**

```shell
# "local" is for Unix domain socket connections only
local    all        all        trust # ou peer
```

```shell
# IPv4 local connections:
host     all     all     127.0.0.1/32     trust
```

```shell
# IPv6 local connections:
host     all     all     ::1/128         trust
```

## Altere conforme necessário

**Assim ficará a regra de liberação:**

```shell
# IPv4 local connections:
host     all     all     0.0.0.0/0         md5
```

<mark>**É possível também liberar o acesso apenas a uma rede específica:**</mark>

```shell
# IPv4 local connections:
host     all     all     192.168.1.0/24     md5
```

------

#### Abra o pgadmin ou software de preferência e faça a conexão usando as credenciais do servidor configurado.

#### Não esqueçam de liberar a porta no grupo de segurança ou na configuração de rede da sua Instância, de acordo com a nuvem utilizada ou VM Local.

<hr>

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)
