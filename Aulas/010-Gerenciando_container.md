# Gerenciando *container* <img align="right" src="../img/vtp_ifsp-pb.png" width="250">

<br>

<img align="center" src="../img/docker.png" width="200" />

<br>

## Recursos básicos de hardware

Como vimos o parâmetro `stats` mostra informações dos *container* em execução, se em alguma necessidade seja importante limitar os recursos é possível fazer conforme o exemplo.

```bash
docker container run --name teste --cpus=4 -m 512m -d nginx
```

Desta forma limitamos o uso de CPU em 4 e uso de memora em 512MB. Caso queira alterar estes valores, é possível fazer usando comando `update`

```bash
docker container update --cpus=2 -m 256m teste
```

## Recursos de mapeamento de portas

Em alguns casos é necessário direcionar as requisições da máquina real para dentro do *container*, conforme exemplo.

```bash
docker container run --name apache2-container -p 8080:80 -d ubuntu/apache2
```

Desta forma, toda requisição feita na por **8080** do navegador local, será redirecionado para porta **80** do *container*, neste caso respondendo com pagina padrão do Apache.

## Recursos de mapeamento de diretórios

Há também a possibilidade de espelharmos uma pasta local, diretamente para dentro do *container*, sendo possível executar nossos arquivos de códigos em interpretadores que estão dentro do *container*. Este mapeamento pode ocorrer usando o caminho absoluto do diretório ou utilizando variável de ambiente do **Docker**.

```bash
docker container run --name apache2-volume -v $PWD:/var/www/html -d ubuntu/apache2
```

Assim, todo conteúdo da pasta local em que foi executado o `run` será mapeada para a pasta `/var/www/html`

Unindo os dois comandos, de portas e diretórios temos.

```bash
docker container run --name apache2-server -p 8080:80 -v $PWD:/var/www/html -d ubuntu/apache2
```

Aqui temos a pasta local sendo mapeada para dentro do *container* em execução e respondendo na máquina local pela porta **8080**.

### Agora é só soltar a imaginação, criando infraestruturas com as possibilidades citadas.
---
<p align="right">
  <a href="011-Primeiro_Dockerfile.md">
     <img title="Primeiro Dockerfile" src="../img/seta-para-frente.png" width="35" />
  <br>
  Primeiro Dockerfile
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