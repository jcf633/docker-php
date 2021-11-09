# Docker PHP

Ambiente de desenvolvimento PHP para Docker
```bash
PHP
Apache2
MySQL
```

## Instalação

1 - Estrutura de pasta
```bash
mkdir workspace
cd workspace
mkdir html
mkdir bash-env
```

2 - Clonar repositório
```bash
git clone https://github.com/jcf633/docker-php.git docker-php
```

3 - Customização Bash
```bash
cd bash-env
touch aliases.sh
```
`Obs. No arquivo aliases.sh pode ser adicionado variáveis de ambiente das aplicações, para se rodar migrations por exemplo. 
Esse arquivo será lido automaticamente ao acessar a máquina php-apache.`

4 - Criar variáveis de ambiente do docker
```bash
cd ../docker-php
cp env-example .env
```
`Obs. No arquivo .env pode ser alterado versão do PHP, portas onde apache irá rodar na sua máquina, versão e credenciais do MySQL, 
além de poder alterar pasta de logs e pasta onde serão criados os volumes do docker.`

5 - Construir imagens dos serviços
```bash
docker-compose build
```

6 - Subir os serviços
```bash
docker-compose up -d
```

### Scripts SQL

Os scripts sql devem sem colocados na pasta scripts-sql. 
```
workspace       
│
└─── docker-php
    │
    └─── mysql
        │
        └─── scripts-sql
```
`Obs. Deve ser criado scripts .sql dentro da pasta scripts-sql, esses script podem conter criação de database, inserts, etc.
É possivel ver um exemplo no arquivo (script.sql.example) dentro da pasta scripts-sql.`

### Apache Virtual Host

Os arquivos de configuração dos virtuais host devem sem colocados na pasta sites. 
```
workspace       
│
└─── docker-php
    │
    └─── php-apache
        │
        └─── apache-config
             │
             └─── sites
```
`Obs. Deve ser criado um arquivo .conf dentro da pasta sites, sempre que adicionado um novo virtual host.
É possivel ver um exemplo no arquivo (virtual-host.conf.example) dentro da pasta sites.
Sempre que houver alteração nestes arquivos, é necessario dar restart no service com o comando 
(docker-compose restart php-apache), comando deve ser rodado dentro da pasta docker-php.`

### Acessar máquina

Para rodar comandos pelo bash em suas aplicações, como por exemplo composer ou migrations, você pode acessar a máquina através do comando:
```bash
docker-compose run php-apache bash
ls
cd <nome-seu-projeto>
```
`Obs. Comando deve ser rodado dentro da pasta docker-php.`

### Clonar projetos

Suas aplicações PHP devem ser clonadas dentro da pasta **html**, criada dentro de **workspace**.

### Estrutara de pastas do workspace

```
workspace       
│
└─── docker-php
│
└─── bash-env
│
└─── logs
│
└─── data
│
└─── html
     │
     └─── <seus-projetos>
```
`Obs. As pastas logs e data serão criadas automaticamente quando os serviços subirem.`