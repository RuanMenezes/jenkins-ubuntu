# Começando com Jenkins

Repositório para a turma Jenkins for Testers


## Ubuntu Server VM ou Docker
  * [Ubuntu Server](http://getgauge.io/get-started/index.html)
      
## Docker

  * [Docker CE](https://download.docker.com)

Apos a instalação do docker, no terminal, digite o comando "docker -v"
```sh
docker -v
```
Preparando o container com Ubuntu Linux

```sh
docker pull ubuntu
docker run -d -p 8080:8080 -t ubuntu /bin/bash
docker ps -a
```
###  Instalando o Jenkins no Container

```
docker rename <container_id> jenkins
docker exec -i -t jenkins /bin/bash
apt-get update
apt-get install wget
apt-get install vim
```
* Agora vamos instalar de fato o Jenkins com os seguintes comandos:

```
wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | apt-key add -
```
```
sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

```
apt-get update
apt-get install jenkins
```

* Vamos iniciar o Jenkins com o comando:

```
/etc/init.d/jenkins start
```

* Através do navegador, vamos acessar a seguinte URL http://localhost:8080

* Vamos voltar para o terminal do container com o comando:

```
docker exec -i -t jenkins_cucumber /bin/bash
```

* Em seguida, vamos pegar a Senha Admin Inicial para ativação do Jenkins e finalizar o processo de instalação:

```
cat /var/lib/jenkins/secrets/initialAdminPassword
```

* Copie a senha e cole no campo "Administrator password", em seguida, clique em "continue".

* Na página Customize Jenkins, vamos escolher a opção "Install suggested plugins".

## Instalando o Git no Container

```
apt-get install git
```

## Update do Ubuntu e Dev Dependencies

```
apt-get update
apt-get install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev -y
```

## Instalando os Plugins no Jenkins

### Na home do Jenkins, clique em "Gerenciar Jenkins", em seguida, "Gerenciar Plugins".

### Agora clique na aba "Disponíveis" e marque os seguintes plugins:

* Rbenv
* Junit Plugin


