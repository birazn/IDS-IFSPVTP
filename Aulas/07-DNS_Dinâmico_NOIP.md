# Servidor DNS Dinâmico Gratuito - NOIP <img align="right" src="img/vtp_ifsp-pb.png" width="40%">

![](/home/birazn/Dropbox/IFSP-Votuporanga/Aulas/Superior/IDS-IFSPVTP/img/noip.png)

#### O primeiro passo é criar uma conta no site do serviço gratuito no-ip. [Acessar o site NOIP](https://www.noip.com/)

#### Criar uma conta e fazer a ativação

#### Após ter criado a conta, inicialize sua instância na AWS e pegue o IP para configurar o domínio no NOIP

![](/home/birazn/Dropbox/IFSP-Votuporanga/Aulas/Superior/IDS-IFSPVTP/img/noip-host.png)

Feitas as configurações no site do serviço, agora é a hora de configurar o nosso servidor de modo a que ele envie seu novo IP para o no-ip a intervalos regulares, o que faz com que precisemos decorar somente o domínio que registramos, e não mais o IP.
Isso facilita a configuração do Termius, por exemplo, não sendo mais necessário mudar o IP nele a cada vez que a instância é parada e iniciada novamente.

# Client NOIP

Primeiramente vamos fazer o download do arquivo do cliente e descompactá-lo no nosso servidor.

```bash
cd /usr/local/src/
sudo wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz
sudo tar xzf noip-duc-linux.tar.gz
cd noip-2.1.9-1
sudo apt install make gcc
sudo make
sudo make install
```

Para executar o comando **make**, que faz a compilação dos arquivos e gera o binário, são necessários dois pacotes que não estão instalados por padrão no Ubuntu (normalmente): o próprio **make** e o **gcc**, que ja foram instalados conforme script anterior.

#### Depois de feita a instalação, é necessário configurar o cliente no-ip, e isso é feito com o comando 

```bash
sudo /usr/local/bin/noip2 -C #note que -C é maiusculo 
```

**Algumas perguntas serão feitas: e-mail cadastrado no site no-ip, senha, qual o tempo de atualização do IP (em minutos), se deseja salvar as alterações e qual o arquivo de configuração.**

Feita a instalação e configuração, é hora de colocar o serviço para rodar com o comando

```bash
sudo /usr/local/bin/noip2
```

Esse comando, executado no terminal, faz com o que o serviço passe a rodar, <u>mas caso o servidor seja reinicializado, ele precisa ser rodado novamente.</u> **A seguir veja como automatizar essa inicialização.**

## Colocando NOIP para iniciar automático

Os vários scripts de inicialização do Ubuntu ficam no diretório **<u>/etc/init.d</u>**. Além disso, existem links dentro de outros diretórios de inicialização e encerramento do servidor.
Uma forma prática de automatizar a execução de um comando qualquer, é criando um arquivo chamado **<u>rc.local</u>** dentro do diretório **<u>etc</u>** e dar permissão de execução para ele.

**Podem ser usados vários métodos, vou deixar aqui um deles**

Criar um arquivo

```bash
sudo vim /etc/rc.local
```

Dentro deste arquivo faça uma chamada de *script* com **shebang** e a linha de execução do noip2

```bash
#!/bin/bash
/usr/local/bin/noip2
```

Salvar arquivo e colocar como executável

```bash
sudo chmod 755 /etc/rc.local
```

Reinicie o servidor para verificar se o serviço está ativo.

---

<p align="right">
  <a href="08-Iniciando_com_Docker.md">
     <img title="Iniciando com Docker" src="../img/seta-para-frente.png" width="35" />
  <br>
  Iniciando com Docker
  </a>

</p> 
<p align="left">
<a href="https://github.com/birazn/IDS-IFSPVTP#sumário">
    <img src="../img/casa.png" width="35" />
  <br>
  Sumário
</a>
</p>

---

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)

<img src="../img/birazn-social.png" width="250"/>