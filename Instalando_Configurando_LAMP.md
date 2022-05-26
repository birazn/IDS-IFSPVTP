# Instalando e Configurando LAMP

## Atualizando repositórios

```bash
$ sudo apt update
$ sudo apt upgrade
```

> É importante que o Servidor Web já esteja instalado e configurado. Neste caso, estamos usando o Apache 2.

---

## MySQL

O MySQL é um sistema de gerenciamento de banco de dados relacional (SGBDR) e é um componente popular de muitas aplicações.

```bash
$ sudo apt install mysql-server
```

#### Verificando serviço

```bash
$ sudo service mysql status # forma convencional
# ou
$ sudo systemctl status mysql # forma mais atual
```

#### Após a instalação

> para remover o banco de dados de teste e quaisquer permissões de usuário estranhos adicionados durante o processo inicial de instalação, para configurar e melhorar a segurança do seu servidor MySQL

```bash
$ sudo mysql_secure_installation
```

Esta configuração, exibirá a opção **<mark>VALIDATE PASSWORD PLUGIN</mark>** usada como validação de senhas fortes para usuários do MySQL. Existem três níveis:

- low

- medium

- strong

Caso **não queira** usar a validação, basta pressionar **ENTER**

#### Continuando sem usar a validação

No próximo passo, você poderá alterar a senha do usuário root.

- Digite a senha (não esquecer) **dica '13579'**

Nas próximas questões você pode responder: (ou mude como preferir)

- remover usuário anônimo **sim (Y)**;

- remover acesso remoto **sim (Y)**; <mark>(tira acesso remoto com root)</mark>

- remover banco de dados de teste **sim (Y)**;

- recarregar privilégios agora **sim (Y)**.

#### Logando como root

```bash
$ sudo mysql
```

**Deve cair em um prompt**

```bash
mysql>
```

Se você quiser fazer login como root através de programas externos, como o **phpMyAdmin**, você tem duas opções:

**A primeira opção é alterando o método de autenticação do usuário root:**

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'senha_da_nasa';
FLUSH PRIVILEGES;
```

**E a segunda e recomendada é criar um usuário administrativo com acesso a todos os bancos de dados, sem alterar o método de autenticação do root:** <mark>(indicada)</mark> **dica '13579'**

```sql
CREATE USER 'ids'@'localhost' IDENTIFIED BY 'senha_da_nasa';
GRANT ALL PRIVILEGES ON *.* TO 'ids'@'localhost' WITH GRANT OPTION;
```

Ainda dentro do terminal MySQL, vamos criar um banco de dados e conceder acesso de usuários para utilizar as bases, o procedimento abaixo deve ser usado com a **versão 8 do MySQL**.

```sql
CREATE DATABASE ids2022;
CREATE USER 'azureuser'@'localhost' IDENTIFIED BY 'senha_da_nasa';
GRANT ALL ON ids2022.* TO 'azureuser'@'localhost' WITH GRANT OPTION;
exit
```

> **Caso queira liberar acesso remoto para outros programas**

```bash
$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

Comente a linha do **bind-address**

---

# PHP

É o interpretador que torna possível a execução de paginas dinâmicas e interativa usando seus próprios scripts e frameworks.

```bash
$ sudo apt install php5 php-pear php5-mysql libapache2-mod-php5 php5-pgsql
```

**(para base Debian 8 – verificando a versão PHP)**

```bash
$ sudo apt install libapache2-mod-php7.X php7.X php7.X-mysql php7.X-pgsql
```

**(para versões superiores do Debian)**

> Notem que o X apresentado na versão '7.X' é para indicar que as versões pode ser diferentes, dependendo da distro e do tempo de lançamento dela.

Criar o diretório de log para PHP e dar permissão do usuário Apache:

```bash
$ sudo mkdir /var/log/php
$ sudo chown www-data /var/log/php
```

**(<u>www-data</u> é usuário do apache)**

Crie um arquivo funcionalidades.

```bash
$ sudo vim /var/www/html/phpinfo.php
```

```php
<?php
phpinfo();
?>
```

**Se funcionar siga para o próximo passo**

## PHP MyAdmin

```bash
$ sudo apt install phpmyadmin
```

Marcar a opção do servidor web que está utilizando com **Apache**.

Configurar o banco integrando com phpmyadmin.

Para acessar o phpmyadmin acesse o endereço local ou <u>http://IP-do-servidor/phpmyadmin</u> que terá que abrir.

---

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)
