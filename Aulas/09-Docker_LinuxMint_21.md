# Instalando Docker Linux Mint 21 <img align="right" src="../img/vtp_ifsp-pb.png" width="30%" />

<br>

<img align="center" src="../img/docker.png" width="30%" />

<br>

## Instalando Docker Engine - Terminal

```bash
sudo apt update && sudo apt upgrade -y
sudo apt -y install apt-transport-https ca-certificates curl software-properties-common
```

### Confirmar que não há nada
```bash
sudo apt -y remove docker docker.io containerd runc
```

### Buscar chave autenticação
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Adicionar Repositório [Verificar os-release]
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu jammy stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Testar se deu certo
```bash
cat /etc/apt/sources.list.d/docker.list
```

**Resposta correta**

```bash
deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu jammy stable
```

### Verificar se está tudo correto
```bash
sudo apt update
```

### Instalar recursos para Docker Engine [Não é Docker Desktop]
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Adicionar seu usuário no grupo docker
```bash
sudo usermod -aG docker $USER
```

### Efetivar alteração [Ou restart session]
```bash
newgrp docker
```

### Verificar versão
```bash
docker version
```

### Testar primeiro *container*
```bash
docker run hello-world 
```

### Testar algo mais funcional
```bash
docker container run -it ubuntu /bin/bash
```


## Fonte
[Computing For Geeks](https://computingforgeeks.com/install-docker-docker-compose-on-linux-mint/)

---

## Dúvidas?

[@birazn](https://www.instagram.com/birazn)

[Canal YouTube](https://www.youtube.com/birazn)

<img src="../img/birazn-social.png" width="250" />