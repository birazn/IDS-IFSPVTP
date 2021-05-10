# Apache TomCat - Instalando e Configurando

Apache Tomcat é um servidor web responsável por rodar códigos java para web, os famosos arquivos JSP.

Com ele é possível portar toda versatilidade e capacidade do java *server pages*, criando paginas web dinâmicas e implementando sistemas de alta performance.

<img src="https://github.com/birazn/IDS2020/blob/master/img/tomcat.png" style="zoom:80%;" />

# Instalando o Java - Teste

Inicialmente é necessário fazer a instalação do java. No Linux existe uma implementação *opensourse* do JDK e JRE.

No comando será instalado a ultima versão do java, neste momento a versão 11

```
sudo apt install default-jdk default-jre
```

Caso queira instalar a versão 8 utilize.

```
sudo apt install openjdk-8-jdk openjdk-8-jre
```

# Pasta base para Tomcat

Crie um diretório para a instalação, nesse procedimento iremos usar um pacote, para ter acesso ao painel de gerenciamento.

```
sudo mkdir /opt/tomcat
```

Baixe o pacote mais atual, **<u>tar.gz</u>** do <a href="https://tomcat.apache.org/download-90.cgi#9.0.38" target="_blank">site Tomcat</a>, e use junto ao comando, a seguir.

# Download Tomcat

Acesse a pasta temporária do sistema.
```
cd /tmp
curl -O https://downloads.apache.org/tomcat/tomcat-9/v9.0.38/bin/apache-tomcat-9.0.38.tar.gz
cd /opt/tomcat
sudo tar xzvf /tmp/apache-tomcat-9.0.38.tar.gz -C /opt/tomcat --strip-components=1
```



# Usuário Tomcat e permissões de pasta

É importante para a segurança, ter um usuário especifico para usar o tomcat.
Crie um grupo e usuário tomcat

```
sudo groupadd tomcat
sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat
sudo chgrp -R tomcat /opt/tomcat
sudo chmod -R g+r conf
sudo chmod g+x conf
sudo chown -R tomcat webapps/ work/ temp/ logs/
```

# Criando arquivo SystemD

É necessário criar um novo arquivo único para executar o Tomcat como um serviço.

```
sudo vim /etc/systemd/system/tomcat.service
```

Inclua o texto abaixo.


```
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/java-1.11.0-openjdk-amd64
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_Home=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
Environment='JAVA_OPTS.awt.headless=true -Djava.security.egd=file:/dev/v/urandom'

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]

WantedBy=multi-user.target
```

Em seguida, notifique o sistema que você criou um novo arquivo executando a seguinte linha de comando:

```
sudo systemctl daemon-reload
```

Os seguintes comandos vão permitir que você execute o serviço Tomcat:

```
sudo chown -R tomcat webapps/ work/ temp/ logs/
sudo su
cd /opt/tomcat/bin
./startup.sh run
```



# Painel Web de Gerenciamento Tomcat

O comando abaixo irá adicionar um login no seu usuário Tomcat, para isso edite o arquivo **tomcat-users.xml**:

```
sudo vim /opt/tomcat/conf/tomcat-users.xml
```

O comando abaixo irá adicionar um login no seu usuário Tomcat, para isso edite o arquivo tomcat-users.xml.

```
sudo vim /opt/tomcat/conf/tomcat-users.xml
```

Adicione as regras, dentro da tag **\<tomcat-users>**

```
<role rolename="manager"/>
<role rolename="admin"/>
<role rolename="admin-script"/>
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-xml"/>
<role rolename="manager-status"/>
<role rolename="admin-gui"/>
<user username="admin" password="SuaSenha" roles="admin,admin-gui,manager,manager-gui,manager-status,manager-script,manager-xml,admin-script"/>
```



# Liberar acesso Tomcat Manager

Para isso, crie ou edite o arquivo  e cole o conteúdo a seguir.

> NOTA: O campo “**allow**” define quais os endereços terão acesso à conexão remota ao Tomcat Manager.
>
> No exemplo abaixo, estão liberados todos os endereços.
>
> Para liberar o acesso somente a um endereço específico ou rede, substitua o conteúdo entre aspas pelo endereço desejado

```
sudo su 
vim /opt/tomcat/conf/Catalina/localhost/manager.xml
```

Cole o código abaixo.

```
<Context privileged="true" antiResourceLocking="false" docBase="$CATALINA_HOME/webapps/manager">
<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
```

Libere o acesso a Role host-manager. Para isso, altere o arquivo. Assim como no passo anterior, será necessário definir o  **allow**:

```
sudo su 
vim /opt/tomcat/webapps/host-manager/META-INF/context.xml
```

Cole ou somente altere código abaixo, conforme necessário.

```
<Context antiResourceLocking="false" privileged="true" >
<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
```

# Colocar script na inicialização

Edite o arquivo, /etc/rc.local e inclua o caminho do startup.sh

```
sudo vim /etc/rc.local
```

Inclua caminho completo

```
/opt/tomcat/bin/startup.sh
```

### Não esqueça de liberar a porta padrão do Tomcar 8080

