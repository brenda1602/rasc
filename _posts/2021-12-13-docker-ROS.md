---
layout: post-page
title: Docker + ROS
subtitle: Dicas para rodar um container ROS + GUI's by Brenda Alencar
cover-img: /assets/img/page-docker/container2.jpg
thumbnail-img: assets/img/page-docker/homepage-docker-logo.png
share-img: /assets/img/rosa-logo-redondo.png
comments: true
tags: [docker, rasc]
css: [/assets/css/tango.css]
---

Se você deseja utilizar um *container* em seus projetos de robótica junto ao ROS, este post é para você!

<center><img src="{{ 'assets/img/page-docker/rosondocker.png' | relative_url }}" alt="Docker logo" width="380"/></center>

### Como criar um contêiner ROS ?

Existem duas formas de utilizar o ROS por meio de um contêiner. A **primeira opção**, a mais simples, é criando a partir de uma imagem padrão do ROS, que são disponibilizadas no repositório oficial do [**ROS**](https://registry.hub.docker.com/_/ros). Escolha a versão adequada e siga os seguintes passos, caso esteja em dúvidas sobre os comandos, sugerimos a publicação anterior sobre [**comandos básicos**](https://mhar-vell.github.io/rasc/2021-12-13-docker-instructions/).

```shell
$ docker pull ros:kinetic-robot # instalar a imagem
$ docker run -ti --name NAME -ti osrf/ros:kinetic-desktop-full bash # criar e inicializar o contêiner
$  /# source opt/ros/kinetic/setup.bash   # configurar o ambiente ROS
```

Para configurar o ambiente do ROS prefira utilizar o arquivo que está no caminho que indicamos, *source opt/ros/kinetic/setup.bash*, ao invés do *ros_entrypoint.sh*. *Entrypoint*, **ponto de entrada**,  é o arquivo que contém as instruções necessárias para configurar todo o contêiner.

A segunda opção é criar um contêiner usando a imagem de uma *distro* do Ubuntu e em seguida instalar o ROS normalmente, como você instala em sua máquina, seguindos as [**instruções para instalação**](http://wiki.ros.org/ROS/Installation) e escolhendo a opção *Desktop-Full Install*. Então você deve procurar uma imagem do Ubuntu compatível com a versão do ROS e seguir os seguintes passos.

```shell
$ docker pull ros:kinetic-robot # instalar a imagem
$ docker run -ti --name NAME -ti osrf/ros:kinetic-desktop-full bash # criar e inicializar o contêiner
  /# source opt/ros/kinetic/setup.bash    # configurar o ambiente ROS
```
Esta segunda opção pode levar alguns minutos a mais, mas certifica que o ROS e os demais pacotes e dependências tenham sido instalados corretamente, evitando possíveis problemas futuros.

### ROS + GUI's

Até este momento, sabemos que o ROS e todos os pacotes estão devidamente instalados, mas se, por exemplo, você tentar abrir o gazebo irá se deparar com o seguinte erro: <span style="color:red">"**cannot connect to X server**"</span>. Isso ocorre porque não foi realizado a conexão necessária para que o contêiner Docker possa se comunicar com a **interface gráfica** da sua máquina (GUI- *Graphical User Interface*). Existem algumas formas ara que isso seja feito, sinalizadas na [documentação do ROS](http://wiki.ros.org/docker/Tutorials/GUI). A forma mais simples envolve expôr o *xhost* da máquina para que o contêiner possa renderizar para a exibição correta, por meio do [soquete UNIX](https://www.ibm.com/docs/en/ztpf/1.1.0.15?topic=considerations-unix-domain-sockets).

```shell
$  docker run -it \
      --env="DISPLAY" \
      --env="QT_X11_NO_MITSHM=1" \
      --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
      osrf/ros:indigo-desktop-full \
      rqt
$  export containerId=$(docker ps -l -q)

$  xhost +local:`docker inspect --format='{{ .Config.Hostname }}' $containerId`
$  docker start $containerId
```

É importante sinalizar que esta não é a opção mais segura, uma vez que você está expondo o xhost, mesmo que seja o específico da sua aplicação. A segunda opção é para quem possui uma GPU NVIDIA, uma alternativa mais segura e mais simples, utilizando o [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker). Para essa solução, você deve instalar corretamente a ferramenta e rodar o seguinte comando:

```shell
$  docker run -it --net=host --gpus all \
      --env="NVIDIA_DRIVER_CAPABILITIES=all" \
      --env="DISPLAY" \
      --env="QT_X11_NO_MITSHM=1" \
      --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
      osrf/ros:noetic-desktop-full \
      bash -it -c "rqt"
```

Nas duas situações estamos criando contêineres, definindo variáveis de ambiente pela TAG **env** e compartilhando um determinado volume da máquina com ele, referente ao X11 e em seguida executando um comando que irá mostrar que a interface gráfica do contêiner está funcionando.

## VScode + Docker

Uma outra dica é para os usuários do *VScode*. Existe uma extensão fornecida pela *Microsoft* que permite visualizar e editar as pastas e arquivos dos contêineres, assim como você faz normalmente, com id **ms-azuretools.vscode-docker**. Além disso, ela facilita também o gerenciamento dos contêineres e imagens, permitindo visualizar os status, desativar e ativá-los, dentre outras coisas.  


----------------------------------------------------------------
Ficou com alguma dúvida? Dá uma olhada na nossa [introdução sobre Docker](https://mhar-vell.github.io/rasc/2021-12-13-docker-first-steeps/) ou sobre os [comandos básicos](https://mhar-vell.github.io/rasc/2021-12-13-docker-instructions/) .Entre em contato com a gente pelos comentários! :)

<br>
<!--equipe-->
<center><h3 class="post-title">Autora</h3><br/></center>
<div class="row">
  <div class=" col-xl-auto offset-xl-0 col-lg-4 offset-lg-0">
    <table class="table-borderless highlight" style="background: #00000000">
      <thead>
        <tr>
          <th><center><img src="{{ 'assets/img/people/brendaalencar-1.png' | relative_url }}" width="100" alt="brenda" class="img-fluid rounded-circle" /></center></th>
        </tr>
      </thead>
      <tbody>
        <tr class="font-weight-bolder" style="text-align: center margin-top: 0">
          <td width="33.33%"><center>Brenda Alencar</center></td>
        </tr>
        <tr style="text-align:center" >
          <td width="33.33%" style="vertical-align: top"><small>Estagiária no CC RoSA, graduanda em Eng. Elétrica. Participou de projetos de Robótica Subaquática e Manipuladores Subaquáticos</small></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>


