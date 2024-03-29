# Servidor Web – Habilitando a Navegação <img align="right" src="../img/vtp_ifsp-pb.png" width="250" />

<img src="../img/serverweb.png" width="50%"/>

# O que é?

Servidor web pode ser um programa de computador responsável por aceitar pedidos HTTP de clientes, geralmente os navegadores, e servi-los com respostas HTTP, incluindo opcionalmente dados, que geralmente são páginas web, tais como documentos HTML com objetos multimídias embutidos.

O mais popular, e mais utilizado no mundo, é o servidor **Apache** (software livre).

A Microsoft possui a sua própria solução denominada **IIS** (Internet Information Services).

<img src="../img/apache-logo-3.png" width="30%"/>

## Instalando e Configurando Apache 2

#### O Servidor Apache ou Servidor HTTP Apache.

Antes de qualquer instalação é aconselhável verificar por atualizações nos repositórios.

```shell
sudo apt update
sudo apt upgrade
sudo apt install apache2
```

## Configurando Apache 2

Para fazer configurações mais finas dentro do apache, o arquivo utilizado é:

```shell
sudo vim /etc/apache2/apache2.conf
```

<p align="right">
<a href="03-VirtualHosts.md">
     <img title="Virtual Hosts" src="../img/seta-para-frente.png" width="35" />
  <br>
  Virtual Hosts
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

<img src="../img/social.png" width="250"/>