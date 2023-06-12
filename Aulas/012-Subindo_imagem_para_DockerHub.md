# Subindo imagem para Docker Hub <img align="right" src="../img/vtp_ifsp-pb.png" width="250">

Para enviarmos uma imagem pronta para o docker hub é necessário, alem de todos os procedimentos para geração, "*build*", da imagem, ter uma conta criada.

<img align="center" src="../img/docker.png" width="200" />

## Criar conta no Docker Hub

### O que é o Docker Hub

Dockerhub é um Serviço de Web Hosting compartilhado para imagens Docker, é nele que os **Dockerfiles** disponibilizadas para a comunidade, bem como **imagens oficiais** também são disponibilizadas por grandes grupos para facilitar o trabalho na hora de criar uma infraestrutura Docker.

Para criar sua conta acesse o site https://hub.docker.com/ e faça seu cadastro.

![](/home/birazn/Dropbox/IFSP-Votuporanga/Aulas/Superior/BSI/IDSS5/IDS-IFSPVTP/img/dockerhub-tela.png)

Após seu cadastro faça login, na interface terá uma tela sem repositório onde poderá cria-los diretamente pelo sistema ou serão gerados automaticamente durante os "*Puchs*", enviando suas imagens. **Pode ser necessário acessar o e-mail de cadastro para confirmação.**

<img src="/home/birazn/Dropbox/IFSP-Votuporanga/Aulas/Superior/BSI/IDSS5/IDS-IFSPVTP/img/dockerhub-repositorio.png"  />

A conta gratuita possui direito a um repositório privado. Existem planos pagos, caso queira mais repositórios privados, isso geralmente é voltado para empresas que usam Docker em sua infraestrutura.

Com a sua conta criada é a hora de fazer o primeiro envio de imagem para o repositório, caso ainda não tenha entendido a ideia, é totalmente semelhando ao que faz subindo seus projetos e códigos para o Github.

Para listar as nossas imagens, use o comando docker images ou docker image ls

```bash
docker images
```

Obtendo um resultado semelhante a mostrado na imagem.

![](/home/birazn/Dropbox/IFSP-Votuporanga/Aulas/Superior/BSI/IDSS5/IDS-IFSPVTP/img/DockerImages.jpg)

Caso ainda não tenha nenhuma imagem criada, vamos criar a primeira, usando procedimento da [aula anterior](https://github.com/birazn/IDS-IFSPVTP/blob/master/Aulas/011-Primeiro_Dockerfile.md) com o Dockerfile.

```bash
FROM ubuntu
LABEL maintainer="@birazn"
RUN apt update
RUN apt install apache2 -y
RUN apt autoclean

EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

Após a criação do arquivo é necessária criação dessa imagem.

```bash
docker build -t serverweb:1.0 .
```

> #### Lembrando que cada Dockerfile deve estar dentro de seu diretório

Feita a imagem é possivel executar normalmente como vinhamos fazendo com as imagens externas, para testar se está tudo correto.

```bash
docker container run --name MeuServidor -d serverweb:1.0
```

Antes de enviarmos nossa imagem para a nuvem precisamos "taggea-la" com o comando *docker tag*, isso é importante para identificarmos o ID atual da imagem e também para indicarmos o usuário da conta no Docker Hub.

```bash
docker tag b6182e430414 SEU_DOCKER_ID/serverweb:1.0
```

Faça o login com comando `docker login`, coloque suas credenciais e receberá mensagem "**Login Succeeded*"

Execute o *push* para "*empurrar*" sua imagem para o repositório.

```
docker push birazn/serverweb:1.0
```

Será gerada uma mensagem de envio com um hash sha256

Verifique diretamente no site, se o repositório foi enviado, após isso todos podem usar esta imagem gerada para criar seus *container* baseado na sua infraestrutura.

---
<p align="right">
  <a href="#">
     <img title="#" src="../img/seta-para-frente.png" width="35" />
  <br>
  Proximo
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