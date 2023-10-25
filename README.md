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


Instalando o Docker. Os comandos mencionados são para a instalação do Docker no Linux. O comando `dnf remove -y runc` remove o pacote runc, e `dnf install -y docker-ce --nobest` instala o Docker CE.
```
dnf remove -y runc
dnf install -y docker-ce --nobest
```
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/3e399305-48d8-4cc1-bd37-bfafc9483eba"/> </div>
<div align="center"> <img src="https://github.com/bmsousa9/images/assets/111213549/01cb29cd-3418-44a8-a494-dc663149f782"/> </div>

Agora que o Docker foi instalado na VM01, vamos ao próximo passo, que é o desafio 2.



># Desafio 2 ![Static Badge](https://img.shields.io/badge/STATUS-Em_Desenvolvimento-FFC000)
Criar uma imagem do postgresql rodar a imagem e persistir os dados do
banco em um volume


### Criando uma imagem do PostgreSQL



># Desafio 3 ![Static Badge](https://img.shields.io/badge/STATUS-Ainda_ser%C3%A1_Iniciado-red)
Instalar o docker no linux, criar uma imagem do wordpress com banco de
dados e persistir os dados usando docker-compose
