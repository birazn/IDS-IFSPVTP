<img src="/home/birazn/Dropbox/IFSP-Votuporanga/Aulas/Superior/IDS-IFSPVTP/img/docker.png" style="zoom:33%;" />

[TOC]

# Iniciando com Docker

## Docker Engine+CLI vs Docker Desktop

A Engine Docker, roda diretamente e por padrão no Linux como CLI (***Command Line Interface***), da mesma forma como começou por volta de 2013. É importante lembrar que, no manuseio e gerenciamento direto nos servidores em nuvem ou local, isso acontece em CLI. O consumo de recursos usando desta forma é bem inferior, ampliando as possibilidades, mesmo com hardwares mais modestos. Em Linux, podemos executar somente a Engine Docker, o CLI ou as demais ferramentas e plugins existentes instalando manualmente.

O Docker Desktop trabalha um pouco diferente, criando uma maquina virtual minúscula, dentro do ambiente do Linux, a exemplo do que é feito nos ambientes gráficos Mac e Windows. O motivo de fazer desta forma, ao invés de simplesmente criar uma GUI (***Graphical User Interface***) para gerenciar a Engine Docker, é compatibilizar a experiencia dos usuários nos três principais ambientes do mercado. Lembrando que esta solução trás a facilidade no controle de *containers* locais em ambientes de desenvolvimento.

Com esta interface do Docker Desktop, fica mais fácil criar, excluir e editar os *containers,* com suas imagens, redes, volumes e demais recursos que podem ser criados.

Se você é um iniciante em tecnologias de *containers* é interessante que comece com o Docker Deskop, até ter mais conhecimento e prática na utilização do CLI.

## Docker Comandos

Docker é uma plataforma de software que permite criar, testar e implantar aplicativos rapidamente, usando contêineres. Com o Docker, os desenvolvedores podem criar um ambiente de desenvolvimento completo, incluindo servidores, bibliotecas e dependências, em um contêiner e implantá-lo facilmente em qualquer lugar.

A seguir, estão alguns dos comandos mais comuns do Docker:

- **docker container run**: Este comando é usado para criar e executar um contêiner a partir de uma imagem do Docker. A sintaxe básica é `docker container run image_name`, onde `image_name` é o nome da imagem que você deseja executar.
- **docker container ls**: Este comando é usado para listar todos os contêineres em execução no sistema. A sintaxe básica é `docker container ls`.
- **docker container ls -a**: Este comando é usado para listar todos os contêineres no sistema. A sintaxe básica é `docker container ls -a`.
- **docker container start/stop/restart/pause/unpause**: Estes comando são usados para iniciar/parar/reiniciar/pausar/despausar um contêiner em execução. A sintaxe básica é `docker container start/stop/restart/pause/unpause container_name`, onde `container_name` é o nome do contêiner que você deseja parar.
- **docker container rm**: Este comando é usado para remover um contêiner. A sintaxe básica é `docker container rm container_name`, onde `container_name` é o nome do contêiner que você deseja remover.
- **docker image rm**: Este comando é usado para remover uma imagem do Docker. A sintaxe básica é `docker image rm image_name`, onde `image_name` é o nome da imagem que você deseja remover, `os containers criados a partir desta imagem precisa estar parados`.
- **docker container inspect:** Este comando é usado para mostrar todas as informações referentes a um determinado container. A sintaxe básica é `docker container inspect image_name`, onde `image_name` é o nome da imagem que você deseja verificar.

Esses são apenas alguns dos comandos mais comuns do Docker. Existem muitos outros comandos disponíveis, e você pode encontrar mais informações na documentação oficial do Docker.

## Documentação de Referência

[O Projeto · HonKit](https://livro.descomplicandodocker.com.br/)

------

# Conceito de Container

## Isolamento de Recursos

- CPU
- Memoria
- Discos
- Networks
- Processo
- Filesystens

## Principal diferença VM x Container

- Complexidade
    - Vulnerabilidades, quando um patch de segurança precisa ser aplicado, em VMs é necessário atualizar todos os sistemas operacionais instalados, enquanto que Docker, basta aplicar no sistema operacional base.
    - Container runtime é nativo linux

## Imagem mostrando a diferença

![https://www.netapp.com/media/Screen-Shot-2018-03-20-at-9.24.09-AM_tcm19-56643.png](https://www.netapp.com/media/Screen-Shot-2018-03-20-at-9.24.09-AM_tcm19-56643.png)

## Docker [Popularizou a 2ªGeração de Container]

- LXC LXD DotCloud

  ### Orquestração

  ![](https://vertigo.com.br/wp-content/uploads/2019/01/grafico-ferramentas-de-orquestracao-768x512-1.png)

## Imagem de Container

- Somente o necessário para APP funcionar

---

# Comandos na Prática

Trabalhando com docker em máquina local.

O Docker está disponível em duas versões:

- Docker Community Edition (Docker CE) **[free]**
- Docker Enterprise Edition (Docker EE) **[pago]**

O processo de instalação é bem simples, usando a referencia do próprio Docker.

## Pegar o script e executar em Bash

```bash
curl -fsSL https://get.docker.com | bash
```

#### A linha executa um *script* que já identifica a sua distro de Linux e faz a instalação de tudo que for necessário.

> **Para as versões de Linux Mint é necessário utilizar outro processo, verifique o arquivo de instalação exclusivo desta distro.**

### Após a instalação faça o teste verificando qual versão foi instalada.

```bash
sudo docker version
```

### Caso queira utilizar em maquina local sem a necessidade de executar usando **sudo** adicione o usuário no grupo do Docker.

```bash
sudo usermod -aG docker $USER
```

> **Nos comandos pratico utilizaremos, já tendo o usuário no grupo Docker.**

#### Verificar se existe container em execução

```bash
docker container ls
```

#### Verificar se existe container em execução ou parado

```bash
docker container ls -a
```

#### Vamos rodar nosso primeiro container

```bash
docker container run hello-world
```

#### Neste processo ele verifica se a imagem do hello-world existe, baixa e executa diretamente, Oferecendo a saída

```bash
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:4e83453afed1b4fa1a3500525091dbfca6ce1e66903fd4c01ff015dbcb1ba33e
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:

  1. The Docker client contacted the Docker daemon.
  2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
     (amd64)
  3. The Docker daemon created a new container from that image which runs the
     executable that produces the output you are currently reading.
  4. The Docker daemon streamed that output to the Docker client, which sent it
     to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

#### Seguindo a própria indicação do "hello-world", vamos agora executar um container e abrir um terminal interativo para podermos manipular.

> **O ENTRYPOINT é o principal comando a ser executado quando o container sobe. Ele deve ser, inclusive, um comando que prende o terminal, caso contrário o container apenas sobe e desce não se mantendo útil. Esse comando deve receber um array ou mesmo um parâmetro único. No nosso exemplo será o 'bash'.**

```bash
docker run -it ubuntu bash
```

Se sairmos do container usando comandos comuns de linux vamos "matar"  processo, pois, o que esta em execução no momento é somente o **bash**. Usar o ***exit*** ou ***ctrl+d*** sairá parando a execução do container.

Para que possamos sair do container, mantendo em execução, usamos o ***<u>ctrl+p+q</u>***.

Caso eu queira voltar para o container em execução, posso usar:

```bash
docker container attach [CONTAINER ID]
```

Então o parâmetro *<u>**run**</u>* é utilizado para executar um container, estando ele na maquina ou não.

Outros parâmetros usam basicamente o mesmo formato, em alguns casos dispensando o ***-it*** do terminal interativo.

```bash
# docker container [start/stop/restart] [CONTAINER ID]
docker container start [CONTAINER ID]
docker container stop [CONTAINER ID]
docker container restart [CONTAINER ID]
```

> Lembrando, para obter informações dos containers em execução usamos: **<u>docker container ls</u>**

Temos também o parâmetros ***inspect*** que gera uma saída com todas as informações sobre o container que for chamado.

```bash
docker container inspect [CONTAINER ID]
```

Podem ser usados também os parâmetros ***pause*** e ***unpause***, que irá pausar ou "despausar" o container.

Ainda é possível verificar as informações de execução de um container com o parâmetro ***stats***

```bash
docker container stats [CONTAINER ID]
```

Quando não queremos mais utilizar aquele container podemos exclui-lo com parametro **rm**.

```bash
docker container rm [CONTAINER ID]
```

## [Livro de referência](https://livro.descomplicandodocker.com.br/chapters/chapter_01.html)

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)
