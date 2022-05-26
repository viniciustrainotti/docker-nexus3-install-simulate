# Simulação de Instalação Nexus 3

Somente para testes via docker imagem `ubuntu:20.04` ou similar.

```sh
docker run -itd --rm --name nexus3 -p 80:80 -p 8081:8081 ubuntu:20.04
docker exec -it 094 bash

apt-get update
apt install openjdk-8-jdk-headless -y
java -version
cd /opt/
mkdir nexus3
#adduser nexus
usermod -a -G sudo nexus
apt install sudo -y
apt install vim -y
```

Executar o `visudo` e adicionar a linha abaixo do `%sudo`

```
nexus   ALL=(ALL)       NOPASSWD: ALL
```

```sh
chown -R nexus:nexus /opt/nexus3/
apt install wget -y
cd nexus3
wget https://download.sonatype.com/nexus/3/nexus-3.39.0-01-unix.tar.gz
tar -xf nexus-3.39.0-01-unix.tar.gz
ln -s $(pwd)/nexus-3.39.0-01 nexus-running
chown -R nexus:nexus *
su - nexus
echo run_as_user="nexus" > /opt/nexus3/nexus-running/bin/nexus.rc
sudo ln -s /opt/nexus3/nexus-running/bin/nexus /etc/init.d/nexus
/etc/init.d/nexus start
```

## Links
- https://stackoverflow.com/questions/57028412/how-to-install-nexus-on-ubuntu-18-04
- https://help.sonatype.com/repomanager3/product-information/download
- https://help.sonatype.com/repomanager3/product-information/system-requirements#SystemRequirements-Java

