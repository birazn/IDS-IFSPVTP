# Servidor Web – Habilitando a Navegação

<img src="https://github.com/birazn/IDS-IFSPVTP/blob/master/img/apache-logo-3.png" width="10%"/>

## Opção de Editor de texto

Vim, é uma opção ao editor em modo texto nano que tem as bases do Vi com algumas atualizações.

Para instalar:

```shell
$ sudo apt install vim
$ sudo vim /etc/vim/vimrc # O vimrc é o arquivo que tem as configurações do vim
```
Descomentar as linhas:

```shell
# Procurar esta linha
if has("syntax")
  syntax on
endif
# Procurar esta linha
set background=dark

# Procurar esta linha
if has("autocmd")
  au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal$
endif

# Procurar esta linha
if has("autocmd")
  filetype plugin indent on
endif

# Incluir essas linhas logo apos os 'set'
set nu
set cursorline
```



# Servidor Web

Servidor web pode ser um programa de computador responsável por aceitar pedidos HTTP de clientes, geralmente os navegadores, e servi-los com respostas HTTP, incluindo opcionalmente dados, que geralmente são páginas web, tais como documentos HTML com objetos multimídias embutidos.

O mais popular, e mais utilizado no mundo, é o servidor **Apache** (software livre).

A Microsoft possui a sua própria solução denominada **IIS** (Internet Information Services).



## Instalando e Configurando Apache 2

#### O Servidor Apache ou Servidor HTTP Apache.

Antes de qualquer instalação é aconselhável verificar por atualizações nos repositórios.

```shell
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install apache2
```

## Configurando Apache 2

Para fazer configurações mais finas dentro do apache, o arquivo utilizado é:

```shell
$ sudo vim /etc/apache2/apache2.conf
```



## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)

