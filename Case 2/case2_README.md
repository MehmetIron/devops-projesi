# 2. case

# Çalışmaları AWS ec2 üzerinde uygulandı

# 2 adet ec2 çalıştırdım

# Control node ansible, docker, docker-compose yükledim
sudo amazon-linux-extras install ansible2
ansible --version

sudo amazon-linux-extras install docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -a -G docker ec2-user
newgrp docker

curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

# key_pem i control node içine taşıdım

# proje adlı klasörü oluşturup çalışmalarımı burda yapmak üzere dizine gittim
mkdir proje
cd proje

# bulunduğum dizinde inventory.txt ve ansible.cfg dosyalarını oluşturdum bu şekilde Ansible ın configürasyon ayarlarını yaptım.

# to-do.app , templates uygulamasını control node içine yükledim

# Dockerfile oluşturdum

# Dockerfile dan image oluşturdum ve bu image DockerHub a push ettim
docker build -t mehmet2159/to-do .
docker login
docker push mehmet2159/to-do

# docker-compose oluşturdum

# redirect.conf dosyayını oluşturdum. Bu dosya "bootcamp=devops" header ı yazılırsa doğrudan nginx üzerinden "Hoşgeldin Devops" ekranına yönlendirsin

# playbook.yaml oluşturdum ve bu dosyayı çalıştırdım
ansible-playbook -b playbook.yaml

# Browserdan Target makinanın IP sini "x.x.x.x" yazıdğım da to-do.app uygulamasının root ekranını görüyoruz.

# Target makinanın IP sinin yanına "x.x.x.x/?bootcamp=devops" yazdığımızda "Hoşgeldin devops" ekranını görüyoruz.
