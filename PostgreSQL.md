# Instalando e Configurando o PostgreSQL

<img src="https://github.com/birazn/IDS2020/blob/master/img/postgresql.png"  />

Fazer a instalação usando o comando abaixo, verifiquem a versão do repositório.

```shell
sudo apt install postgresql-10 -y
```

## Habilitando usuário no PostgreSQL

```shell
sudo -u postgres psql
alter user postgres with encrypted password 'senhaescolhida';
```

## Habilitando acesso remoto ao servidor PostgreSQL

Abra o arquivo

```shell
sudo nano /etc/postgresql/10/main/postgresql.conf
```
**Altere a linha**

```shell
# listen_addresses = 'localhost' 				# what IP address(es) to listen on
```

**Para**

```shell
listen_addresses = '*'					    	# what IP address(es) to listen on
```

Descomentando e trocando <u>'localhost'</u> por <u>'*'</u>

Salve e feche o arquivo

------

Abra o arquivo

```shell
sudo nano /etc/postgresql/10/main/pg_hba.conf
```

**Que por padrão vem**

```shell
# "local" is for Unix domain socket connections only
local	all		all		trust # ou peer
```

```shell
# IPv4 local connections:
host 	all 	all 	127.0.0.1/32 	trust
```

```shell
# IPv6 local connections:
host 	all 	all 	::1/128 		trust
```

## Altere conforme necessário

**Assim ficará a regra de liberação:**

```shell
# IPv4 local connections:
host 	all 	all 	0.0.0.0/0 		md5
```

**É possível também liberar o acesso apenas a uma rede específica:**

```shell
# IPv4 local connections:
host 	all 	all 	192.168.1.0/24 	md5
```

------

#### Abra o pgadmin ou software de preferência e faça a conexão usando as credenciais do servidor configurado. 

#### Não esqueçam de liberar a porta no grupo de segurança ou na configuração de rede da sua Instância ou VM.