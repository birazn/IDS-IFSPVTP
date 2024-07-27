# Dicas Básicas sobre Docker <img align="left" src="../img/docker.png" width="200" />
- **Nível: Intermediário**
- **Tipo de Conteúdo: Prático, Teórico**


<br>

## Criando Instância e configurando


- **Crie normalmente a instância, conforme as aulas anteriores, liberando já durante a configuração as portas 22 e 80;**
- **Após ter conectado na instância, precisamos fazer a instalação da *Engine Docker*, para isso existem várias formas, vou deixar aqui, a que julgo mais simples para distros raiz;**
- **Faça primeiramente a instalação do CURL;**
    - **Se já estiver, irá receber a mensagem ao executar o comando de instalação;**

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl
```

### **Pegar o *script* e executar em Terminal Bash**

```bash
# Pegar o script e executar em Bash
curl -fsSL https://get.docker.com | bash

# Colocando usuario no grupo do Docker - É necessario reiniciar a sessão ou a Instância
sudo usermod -aG docker ubuntu

# Testando a versão do Docker
sudo docker version

# Testando a versão do Docker Compose
sudo docker compose version

# Verificando Containers em Execução
docker container ls
```

## A linha de comando Docker CLI segue uma dinâmica após a última atualização.

**docker {objeto} {ação} {parâmetros}**
**docker {container | image | network | volume | ...} {run | ls | inspect | rm | create | ...}**

```bash
# Baixando a imagem do alpine
docker image pull alpine:3.20

# Listando as imagens baixadas
docker image ls

# Rodando um container com a imagem baixada
docker container run -it alpine:3.20 sh

# É possivel fazer tudo de uma vez só, baixando e executando
docker container run -it hello-world
docker container run -it ubuntu
```

### **Para sair de um container, sem o finalizar “matar”, use a combinação de teclas CTRL+P+Q**

*O ENTRYPOINT* é o principal comando a ser executado quando o container sobe. Ele deve ser, inclusive, um comando que prende o terminal, caso contrário o container apenas sobe e desce não se mantendo útil. Esse comando deve receber um array ou mesmo um parâmetro único.

## Outros exemplos de utilização

> [!TIP]
>
> #### docker container **attach** [CONTAINER ID] 
>
> #### docker container **rm** [CONTAINER ID]
>
> #### docker container [**start/stop/restart**] [CONTAINER ID]
> #### docker container **inspect** [CONTAINER ID]
>
> #### docker container **pause** [CONTAINER ID
>
> #### docker container **unpause** [CONTAINER ID]
>
> #### docker container **stats** [CONTAINER ID]

