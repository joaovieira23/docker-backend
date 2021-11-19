#DOCKER API

Uma API REST do docker para gerenciar o docker em um servidor remotamente

## INSTALLATION

```
& npm install
$ NODE_PORT=8080 npm start
```

## USAGE

### GET
* `/hello` : ping api
* `/free-port` : obter uma porta livre no servidor
* `/containers` : obter lista de contêineres
* `/images` : obter lista de imagens

### POST
* `/images` : criar uma nova imagem
    * **name** : nome da imagem
* `/containers/run` : executar um contêiner com configuração de arquivo docker
    * **name** : Nome do container (opcional)
    * /!\ body tem que ser um arquivo json

Body exemplo
```
{
    Image: 'node:6',
    Volumes: { "/volume": {} },
    Cmd: ['node', '/volume/server.js'],
    ExposedPorts: { "8080/tcp": {} },
    Env: ['NODE_PORT=8080'],
    HostConfig: {
        Binds: ['/var/projects/my-project:/volume'],
        PortBindings: { "8080/tcp": [{ HostPort: "8080" }] }
    }
}

```
* `/containers/<id>/start` : start container pelo id
* `/containers/<id>/stop` : parar o container pelo id
* `/containers/<id>/kill` : finalizar o container pelo id

### DELETE
* `/images/<name>` : deletar a imagem pelo nome
    * **force** : forcar exclusao (opcional, default: false )
    * **noprune** : (opcional, default: false )
* `/containers/<id>` : deletar um container pelo id
