### Rodando container em background
```bash
docker run -d app:v2
```
### Nomeando um container
```bash
docker run -d  --name <NOME_DO_CONTAINER> app:v2
```
### Logs
```bash
docker logs 5f723fab204a
```
```bash
docker logs -f 5f723fab204a
```
```bash
docker logs -n 5f723fab204a
```
```bash
docker logs -t 5f723fab204a
```

### Docker ports
```bash
docker run -d -p 80:3000 --name app2 app:v2
```
### Executando comandos em containers
```bash
docker exec app ls
```
### Iniciando e parando containers
```bash
docker start <CONTAINER_NAME>
```
```bash
docker stop <CONTAINER_NAME>
```
### Removendo containers
```bash
docker rm <NOME_DO_CONTAINER>
```

### Volumes persistentes
```bash
docker volume create app-dados
```

### Inspecionando o volume
```bash
docker volume inspect app-dados
```
### Associando o volume a um container
```bash
docker run -d -p 3000:3000 --name app -v app-dados:/app/dados app:v2
```

### Verificando se o volume foi assossiado ao container
```bash
docker exec -it app sh
ls dados
```
### Criando um arquivo de teste dentro do volume dados
```bash
docker exec -it app sh
cd dados
echo "Hi Docker" > test.txt
```
### Removendo container e verificando se o volume persiste ainda com o arquivo de teste criado
```bash
docker rm -f app
```
### Criando outro container utilizando o volume anterior para ver se os dados se mantem
```bash
docker run -d -p 3000:3000 --name app2 -v app-dados:/app/dados app:v2
docker exec -it app2 sh
ls dados
```

### Copiando arquivos do container para o host
```bash
docker cp app2:/app/dados/test.txt .
docker cp app2:/app/dados/test.txt ~/
docker cp app2:/app/dados/test.txt /home/$USER
```