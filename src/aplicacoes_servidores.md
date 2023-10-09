[Principal](../README.md)

# Docker

Instalação Básica:
```
sudo apt install docker.io docker-compose
```
Habilitar ao iniciar o sistema:
```
sudo systemctl enable --now docker docker.socket containerd
```
Help:
```
docker --help
```
Docker Hub:<https://hub.docker.com/>


# Instalação a partir do docker hub:

Imagem do Wordpress latest:
```
docker pull wordpress
```

Imagem do Ubuntu latest:
```
docker pull ubuntu
```


# Comandos Básicos

### Verificar Imagens:
```
docker images
```

### Iniciar um container: (exemplo wordpress)
```
docker run --name meuwordpress -p 8080:80 -d wordpress
```

 <details markdown='1'><summary>
Especificações
 </summary>
 
 --name: nome do container
 -p: porta do container
 -d: Imagem a ser usada
 </details>



### Listar Containers:
```
docker ps
```
<details markdown='1'><summary>
Especificações
</summary>
 - Responde com lista de containers ativos
 - ID é um dado útil para manipulação de containers
</details>
```
docker ps -a
```
<details markdown='1'><summary>
Especificações
</summary>

Indica Conteiners que estão funcionando e que já foram parados

</details>

### Parar um container:
```
docker stop ID
```
### Iniciar um container:
```
docker start ID
```
### Reiniciar um container:
```
docker restart ID
```
### Remover um container:
```
docker rm ID
```

<details markdown='1'><summary>
Especificações
</summary>

- Para remover um container ele deve estar parado
- Evite usar o comando rm -f ID (remoção de forma forçada)

</details>


### Remover uma imagem:
```
docker rmi ID
```
<details markdown='1'><summary>
Especificações
</summary>

- Para remover uma imagem ela não pode estar em uso
- Evite usar o comando rmi -f ID (remoção de forma forçada)

</details>

Documentação Básica:
<https://docs.docker.com/>

Documentação sobre Docker
<https://docs.docker.com/get-started/overview/>

## Casa OS Docker

Instalação:
```
curl -fsSL https://get.casaos.io | sudo bash
```





## Uptime KUMA

Monitoramento de Servidores

[Uptime Kuma](https://uptime.kuma.pet/)

Exemplo de Instalação básica:

```
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

 - Como usar
   - <https://www.youtube.com/watch?v=JmvYkzA1bQg>

Passo a passo:
 - Adicionar novo monitor
   - Tipo de monitor
   - Nome Amigável
   - URL
   - Intervalo de Heartbeat
   - Novas Tentativas
   - Avançado
     - Certificate Expiry
   - Status Code
     - 200-299
   - Tags
   - Metodos de Autenticação
 - Configurar Notificações
   - Verifique como
 - Paginas de Status
   - Nome
   - Slug
     - nome de status

# Portainer

[Portainer](https://portainer.io)

Community edition

Monitoramento de Conteiner

---
---

