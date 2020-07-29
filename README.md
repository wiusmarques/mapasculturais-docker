# Instalação Mapas Culturais - Docker

  _Este tutorial foi feito baseado em um sistema Ubuntu 18.04_

  ## 1- Instalando o Docker
  
  #### Atualize os repositórios de referência de sua máquina:
  
  ```
  ubuntu@server# sudo apt-get update -y
  ```
  ```
  ubuntu@server# sudo apt-get upgrade -y
  ````
  
  #### Instalação de pacotes que serão utilizados:
  
  ```
  ubuntu@server# sudo apt-get install curl git -y
  ```
  
  #### Em seguida, instale alguns pacotes de pré-requisitos que permitem que o apt utilize pacotes via HTTPS:
  
  ```
  ubuntu@server# sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
  ```
  
  
  #### Então adicione a chave GPG para o repositório oficial do Docker em seu sistema:
  
  ```
  ubuntu@server# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  ```
  #### Adicione o repositório do Docker às fontes do APT:
  
  ```
  ubuntu@server# sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" -y
  ```
  
  #### Atualize novamente os repositórios de referência de sua máquina:
  
  ```
  ubuntu@server# sudo apt-get update -y
  ```
  
  #### Certifique-se de que você irá instalar a partir do repositório do Docker em vez do repositório padrão do Ubuntu:
  
  ```
  ubuntu@server# sudo apt-cache policy docker-ce
  ```
  
  #### Finalmente, instale o Docker:
  
  ```
  ubuntu@server# sudo apt-get install docker-ce -y
  ```
  
  #### Iremos habilitar o serviço e criar o link:
  
  ```
  ubuntu@server# sudo systemctl start docker
  ubuntu@server# sudo systemctl enable docker
  ```
  
  #### O Docker agora deve ser instalado, o daemon iniciado e o processo ativado para iniciar na inicialização. Verifique se ele está sendo executado:
  
  ```
  ubuntu@server# sudo systemctl status docker
  output: Docker version 19.03.12, build 48a66213fe
  ```
  
  #### Conferindo a versão do docker instalado:
  
  ```
  ubuntu@server# docker --version
  ```
  
  #### A saída deve ser semelhante à seguinte, mostrando que o serviço está ativo e executando:
  
  ```
   docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2020-07-28 22:35:27 UTC; 36s ago
      Docs: https://docs.docker.com
      Main PID: 5833 (dockerd)
      Tasks: 8
   CGroup: /system.slice/docker.service
           └─5833 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
  ```
  
  _Para mais detalhes sobre docker [clique aqui](https://www.digitalocean.com/community/tutorials/como-instalar-e-usar-o-docker-no-ubuntu-18-04-pt) e confira as informações adicionais sobre o assunto_
  
  ## 2- Trabalhando com Imagens Docker:
  
  
  
  _Os containers Docker são construídos a partir de imagens Docker. Por padrão, o Docker extrai essas imagens do Docker Hub, um registro Docker mantido pela Docker, a empresa por trás do projeto Docker. Qualquer pessoa pode hospedar suas imagens do Docker no Docker Hub, portanto, a maioria dos aplicativos e distribuições do Linux que você precisa terá imagens hospedadas lá._

  #### Para verificar se você pode acessar e baixar imagens do Docker Hub, digite:
  
  
  ```
  ubuntu@server# docker run hello-world
  ```
  
  #### A saída irá indicar que o Docker está funcionando corretamente:
  
  ```
  Unable to find image 'hello-world:latest' locally
  latest: Pulling from library/hello-world
  0e03bdcc26d7: Pull complete 
  Digest: sha256:49a1c8800c94df04e9658809b006fd8a686cab8028d33cfba2cc049724254202
  Status: Downloaded newer image for hello-world:latest

  Hello from Docker!
  This message shows that your installation appears to be working correctly.
  ...
  ```
  
  #### Instalando Docker composer:
  
  ```
  ubuntu@server#  sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  ```
  
  #### Atribuindo a permissão necesária:
  
  ```
  ubuntu@server#  sudo chmod +x /usr/local/bin/docker-compose
  ```
  
  #### Verificado se foi instalado corretamente:
  
  ```
  ubuntu@server# sudo docker-compose -version
  output: docker-compose version 1.26.2, build eefe0d31
  ```
  #### Iremos clonar o repositório e acessar sua pasta
  
  ```
  ubuntu@server# sudo git clone https://github.com/mapasculturais/mapasculturais-aldirblanc.git
  ubuntu@server# cd mapasculturais-aldirblanc
  ```
  
  ### Ambiete de produção:
  
  #### Inicializando os serviços:
  
  ```
  ubuntu@server# sudo docker-compose -f docker-compose.prod.yml up
  ```
  
  #### Adicione a flag ```-d``` caso queira rodar o docker em segundo plano:
  
  ```
  ubuntu@server# sudo docker-compose -f docker-compose.prod.yml up -d
  ```
  
  _A partir deste momento você deverá ser capaz de acessar o Mapas com o Plugin para a Lei Aldir Blanc_
  
  ### Ambiete de desenvolvimento:
  
  #### Para subir o ambiente de desenvolvimento basta entrar na pasta dev-scripts e rodar o script start-dev.sh.

  ``` 
  meu-mapas/dev-scripts/$ sudo ./start-dev.sh 
  ```
  _acesse no seu navegador http://localhost:8080/_

  #### psysh

  _Este ambiente roda com o built-in web server do PHP, o que possibilita que seja utilizado o PsySH, um console interativo para debug e desenvolvimento. No lugar desejado, adicione a linha eval(\psy\sh()); e você obterá um console. Ctrl + D para continuar a execução do código.

 _Para parar o ambiente de desenvolvimento usar as teclas ```Ctrl + C```_




