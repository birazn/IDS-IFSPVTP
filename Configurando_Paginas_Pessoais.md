# Configurando Páginas Pessoais

É possível oferecer a cada utilizador a possibilidade de criar páginas Internet pessoais.

Uma vez concluída a instalação do **Apache2**, a configuração do suporte para páginas pessoais consiste na ativação do módulo ***userdir*** do servidor apache2.

```bash
$ sudo a2enmod userdir
```

### Ativar suporte ao PHP

A execução de scripts php está desativada nas páginas pessoais. Para ativar, é necessário comentar a linha:

**php_admin_flag engine Off**

no arquivo <mark>/etc/apache2/mods-available/php7.X.conf</mark> (Verificar a versão do PHP instalado)

## A utilização

As páginas pessoais são acessíveis através de um endereço: 

**http://ip_do_servidor/~nome_usuario**

Quando o servidor recebe um pedido deste, tenta encontrar e servir o conteúdo de um diretório específico chamada **public_html** na home do usuário.

Portanto, para que cada usuário possa criar as suas páginas deve, antes de mais nada, criar um diretório chamada “**public_html**” na sua home, onde colocará os conteúdos.

### Criando o diretório, no usuário existente

```bash
$ mkdir ~/public_html
```

Uma vez criado o diretório, o usuário pode começar a criar conteúdos.

Na pasta public_html crie um arquivo **index.html**

```bash
$ vim ~/public_html/index.html
```

Coloque o código para efetuar o teste.

```html
<!DOCTYPE html>
   <html lang="pt-br">
   <head>
      <title>Bem Vindo ao IDS - Página Pessoal!</title>
      <meta charset="UTF-8">
   </head>
   <body>
    <h1>Página pessoal – Olá Mundo</h1>
    <p>Bem Vindo!</p>
   </body>
</html>
```

## Automatizando processo para futuros usuários

Para que o diretório **public_html** seja criado automaticamente quando for criado um novo usuário, é adicionada a entrada em **/etc/skel**, com direitos de acesso exclusivos para próprio utilizador:

```bash
$ sudo mkdir /etc/skel/public_html 
$ sudo chmod 0700 /etc/skel/public_html
```
