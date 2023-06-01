
# Editor de Texto - Configuração <img align="right" src="../img/vtp_ifsp-pb.png" width="30%" />

<img src="../img/vim.png" width="20%"/>

Vim, é uma opção ao editor em modo texto nano que tem as bases do Vi com algumas atualizações.

Para instalar:

```shell
sudo apt install vim
sudo vim /etc/vim/vimrc # O vimrc é o arquivo que tem as configurações do vim
```

Descomentar as linhas, caso seja necessário:

```shell
# Procurar esta linha
if has("syntax")
  syntax on
endif

# Procurar esta linha e descomente, dependendo do tema do seu terminal
set background=dark

# Procurar esta linha
au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif

# Procurar esta linha
filetype plugin indent on

# Incluir essas linhas logo apos os 'set'
set nu
set cursorline
```

<hr>

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)

<img src="../img/birazn-social.png" width="25%"/>

---

<p align="left">
  <a href="https://github.com/birazn/IDS-IFSPVTP#sumário">
    <img src="../img/casa.png" width="64" />
  </a>
  <br>
  Sumário
</p>
<p align="right">
  <a href="02-ServidorWeb.md">
     <img title="Servidor Web" src="../img/seta-para-frente.png" width="64" />
  </a>
  <br>
  Servidor Web
</p>
