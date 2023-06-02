# Primeiro Dockerfile <img align="right" src="../img/vtp_ifsp-pb.png" width="250">



<img align="center" src="../img/docker.png" width="200" />

Até agora tudo foi feito na linha de comando, porém, principalmente nos dias de hoje, não dá para viver mais sem automatizar as coisas, então vamos conhecer o Dockerfile.

O *dockerfile* nada mais é do que um arquivo onde você determina todos os detalhes do seu *container*, como, por exemplo, a imagem que você vai utilizar, aplicativos que necessitam ser instalados, comandos a serem executados, os volumes que serão montados e assim por diante.

Nosso primeiro Dockerfile.

```bash
mkdir primeiroDockerfile
cd primeiroDockerfile
vim Dockerfile
```

Com o arquivo aberto para edição, escrevam as linhas que seguem.

```Dockerfile
FROM debian
RUN /bin/echo "OLA DOCKER"
```

Salve e sai do editor de texto vim.

Após a criação do arquivo é necessária criação dessa imagem.

```bash
docker build -t nome-imagem:1.0 .
```

O ponto "**.**" do final do comando, indica que o Dockerfile a ser executado é o que está na própria pasta que estamos.

Após a execução, verifique se a imagem foi criada

```bash
docker image ls
```

## Criando algo útil

Vamos agora criar uma imagem que traga um Apache funcionando dentro de um Ubuntu, expondo a porta **80** do *container* e colocando o apache em execução.

```dockerfile
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

Feita a imagem é possivel executar normalmente como vinhamos fazendo com as imagens externas.

```bash
docker container run --name MeuServidor -d serverweb:1.0
```



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
