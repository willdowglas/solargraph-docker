# solargraph-docker

Solargraph for VSCode

## Setup

```
docker-compose build solargraph
docker-compose up -d solargraph --name solargraph
```

## VS Code settings

```json
"solargraph.transport": "external",
"solargraph.externalServer": {
    "host": "localhost",
    "port": 8091
}
```
