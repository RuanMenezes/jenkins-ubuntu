# Começando com Jenkins

Repositório para a turma Jenkins for Testers

Importante instalar o Jenkins em um ambiente linux (Você pode usar uma VM Debian ou Imagem Docker).

# Opção 1 Docker
      
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

# Opção 2
## Jenkins com Virtual Box  
  * [Debian Live] (https://www.debian.org/CD/live/) (neste site você deve baixar a ISO)
  * [Virtual Box] (https://www.virtualbox.org/wiki/Downloads)

IMPORTANTE: para VM Debian você deve usar sudo


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

* Vamos voltar para o bash do container com o comando:

```
docker exec -i -t jenkins /bin/bash
```

* Em seguida, vamos pegar a Senha Admin Inicial para ativação do Jenkins e finalizar o processo de instalação:

```
cat /var/lib/jenkins/secrets/initialAdminPassword
```

* Copie a senha e cole no campo "Administrator password", em seguida, clique em "continue".

* Na página Customize Jenkins, vamos escolher a opção "Install suggested plugins".


## Dev Dependencies
* Vamos voltar para o bash do container com o comando:

```
apt-get update
apt-get install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev -y
```

## Sudoers

* Vamos voltar para o bash do container com o comando:

```
docker exec -i -t jenkins /bin/bash
```

* Como root execute:

```
apt-get install sudo -y
vim /etc/sudoers
```

* Adicione jenkins ALL=(ALL) NOPASSWD: ALL


## Instalando o Git no Container

```
apt-get install git
sudo su - jenkins
```

* Acesse o diretório (/var/lib/jenkins) e crie o arquivo ".gitconfig" com o seguinte conteúdo:

[user]
  name = Jenkins
  email = jenkins@localhost


## Instalando os Plugins no Jenkins

### Na home do Jenkins, clique em "Gerenciar Jenkins", em seguida, "Gerenciar Plugins".

### Agora clique na aba "Disponíveis" e marque os seguintes plugins:

* Rbenv
* Junit Plugin

### Crie um job freestyle (simples) e selecione o plugin do RBenv com a versão deseja
### Exemplo: 2.4.3
### Execute o Job para instalar o Rbenv + Ruby no Jenkins Server


* Vamos voltar para o bash do container com o comando:

```
docker exec -i -t jenkins /bin/bash
```

* Execute os comandos

```
sudo su - jenkins
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
```


## Heroku Keys

* Instalação do CLI

```
wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh
```

* Adicione a chave SSH com sua conta do heroku

```
ssh-keygen
heroku keys:add
```



