![Static Badge](https://img.shields.io/badge/STATUS-Em_Desenvolvimento-FFC000)
># Sprint 2 - Docker 
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/d250db2d-77e2-4d3d-ace7-8675a7efd155" width="400px" /> </div>



># Desafio 1 ![Static Badge](https://img.shields.io/badge/STATUS-Resolvido-2e8b57)
Restaurar o backup das 2 VMS, e instalar o docker na VM01


### Clonar a VM utilizada na Sprint 1
Como eu havia criado alguns Snapshots da VM01, restaurei até ao ponto seguinte ao da instalação do Oracle Linux 8.8, lá no Oracle VM Virtual Box e clonei a VM01. 

<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/6d32a090-243e-42f7-af7d-ef3d0fffa460"/> </div>


### Instalação do Docker

Assim que eu acessei a VM01 pelo root e com a senha, inseri o comando abaixo para atualizar o conjunto de utilitários e extensões para o gerenciador de pacotes mais recente.
```
yum install yum-utils -y
```
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/fcfc989b-cfbc-4792-bfab-6d2f0e1320d4"/> </div>

Este comando adiciona o repositório do Docker Community Edition (Docker CE) ao sistema, permite que instale o Docker a partir deste repositório é usado para adicionar o repositório do Docker ao gerenciador de pacotes.
```
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/ccd5ac6e-4b40-46ec-b865-983700512bbd"/> </div>


Os comandos abaixo são para a instalação do Docker no Linux. O comando `dnf remove -y runc` remove o pacote runc, e `dnf install -y docker-ce --nobest` instala o Docker CE.
```
dnf remove -y runc
dnf install -y docker-ce --nobest
```
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/3e399305-48d8-4cc1-bd37-bfafc9483eba"/> </div>
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/01cb29cd-3418-44a8-a494-dc663149f782"/> </div>


### Inicialização e verificação da instalação do Docker

É chegada a hora de habilitar, iniciar e verificar o status da instalação do Docker.
```
systemctl enable docker
systemctl start docker
systemctl status docker
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/76a85312-639b-4994-afc0-de647ee9b359"/> </div>

Verificar agora a versão e fazer o "hello-world":
```
docker --version
docker run hello-world
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/a38c39d7-2579-4060-8a75-82da938872df"/> </div>


Agora que o Docker foi instalado na VM01, vamos ao próximo passo, que é o desafio 2.



># Desafio 2 ![Static Badge](https://img.shields.io/badge/STATUS-Resolvido-2e8b57)
Criar uma imagem do postgresql rodar a imagem e persistir os dados do banco em um volume


### Criar uma imagem PostgreSQL
O próximo passo para é obter a imagem do PostgreSQL do Docker Hub. Para realizar isso, executei o comando a seguir:    
```
docker pull postgres
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/1f6a8f30-7597-43b5-9a8a-37ad0ee2ffbe"/> </div>

### Manter a persistência de dados
Para garantir a persistência de dados, foi criado o volume `pgdata`. Isso assegura que os dados do PostgreSQL não sejam perdidos caso o contêiner seja interrompido ou reiniciado. 
```
docker volume create pgdata
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/e535f9ad-4159-4eda-a816-e557d23461f9"/> </div>

### Acessar o PostgreSQL
Para colocar o contêiner `postgres` em funcionamento, executei o comando a seguir no terminal:
```
docker run -d --name postgres -p 5432:5432 -e POSTGRES_PASSWORD=Senha@ -v pgdata:/var/lib/postgresql/data postgres
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/d8ae3f39-199d-460e-9209-72a0571edfce"/> </div>

+ `-d --name` possibilita nomear o contêiner e `postgres` é o nome dele. 
+ `-p` mapea a porta 5432 que é a padrão do PostgreSQL
+ `-e POSTGRES_PASSWORD` define a senha `Senh@`
+ `-v pgdata:/var/lib/postgresql/data` define o volume `pgdata` como o local onde os dados do PostgreSQL serão armazenados
+ `postgres` é o nome da imagem que foi usada para criar o contêiner homônino `postgres`.


Para entrar no contêiner, usei o comando:
```
docker exec -it postgres /bin/bash
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/83087ea9-63dc-4ed6-adea-83225a9e6095"/> </div>

Agora que o contêiner PostgreSQL está rodando, consegue estabelecer uma conexão com ele pelo `psql` pela linha de comando do PostgreSQL.
```
psql -h localhost -p 5432 -U postgres
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/d72ff90a-96b7-4a81-90d9-bfd6fc25baa0"/> </div>


### Criação de um banco de dados e inserção de dados


Já que estamos no PostgreSQL, é possível criar um banco de dados. Além disso, logo em seguida inseri alguns dados:
```
create table cor(id INTEGER PRIMARY KEY. nome VARCHAR);
insert into cor values(1,'azul'):
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/e77180be-519d-440f-8dd3-460aa9b64f9e"/> </div>


### Verificação da persistência dos dados


Saí do PostgreSQL, saí do Docker, reiniciei a VM01.

<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/8be6f48f-46a3-44c0-aafa-7ec71191b9cf"/> </div>

Depois disso, reiniciei o Docker com `docker restart`, entrei novamente no PostgreSQL com `psql -h localhost -p 5432 -U postgres
` e acessei a tabela criada antes do reboot com `\dt`:
```
docker restart postgres
docker exec -it postgres /bin/bash
```
```
psql -h localhost -p 5432 -U postgres
```
```
\dt
```
<div align="center"> <img src="https://github.com/bmsousa9/CompassUOL-Semana-02/assets/111213549/1def5629-0fe7-496e-8991-d8f785deeed8"/> </div>

Foi verificada a persistência dos dados no PostgreSQL e agora, vamos ao próximo passo: desafio 3.


># Desafio 3 ![Static Badge](https://img.shields.io/badge/STATUS-Em_Desenvolvimento-FFC000)
Instalar o docker no linux, criar uma imagem do wordpress com banco de dados e persistir os dados usando docker-compose
Em desenvolvimento ⚠️⚠️


### Criação de uma imagem do Wordpress
ENTRAR
```
ENTRAR
```
<div align="center"> <img src=""/> </div>
Em desenvolvimento ⚠️⚠️
