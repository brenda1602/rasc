---
layout: post-page
title: Como usar um container?
subtitle: Primeiros passos com Docker by Brenda Alencar
cover-img: /assets/img/page-docker/container1.jpg
thumbnail-img: assets/img/page-docker/homepage-docker-logo.png
share-img: /assets/img/rosa-logo-redondo.png
css: [/assets/css/tango.css]
---
Neste post serão apresentados os primeiros passos para utilizar contêineres. Iremos utilizar o [*Docker Engine*](https://docs.docker.com/engine/) que será o gerenciador dos contêineres e imagens, usando o CLI (Comand Line Interface) *docker*.

## Instalação

*Docker Engine* é compátivel com Windows, Mac (macOS) e Ubuntu, além de [outras distros](https://docs.docker.com/engine/install/#supported-platforms). Para instalar no Ubuntu (Bionic 18.04 ou Focal 20.04, 64-bit) seguimos os seguintes passos:

```shell
# Atualizar o sistema e instalar pré-requisitos
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Adicionar chave GPG oficial Docker
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Configurar repositório estável
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Instalar a versão mais recente da Docker Engine
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io

```

Após a instalação verifique se está tudo ok com um *Hello-world*. Se for a primeira vez rodando este comando perceba que na sua máquina ainda não existe a imagem chamada "hello-world", então será instalada e em seguida a saída será **"Hello from Docker!"**. Caso ocorra algum problema, reveja os passos acima ou confira o [Docker Docs](https://docs.docker.com/engine/install/ubuntu/)

```shell
$   docker run hello-world
```

Recomendamos que você crie uma conta no [**Docker Hub**](https://hub.docker.com/), um repositório público de imagens para contêineres. Em seguida faça  o login no teminal da seguinte forma:

```shell
$   docker login -u [USERNAME] ---password-stdin [PASSWORD]
```
## Comandos básicos

Contêineres são criados a partir de uma imagem, como explicamos anteriormente, para isso é necessário fazer o download da imagem. De forma direta, a imagem é adiquirida pelo comando **pull**, seguido do nome da imagem. Essas imagens ficarão armazenas em sua máquina e você pode checá-las rodando o comando **image list**, a saída será o nome do repositório, a TAG (que pode ser assimilado como a versão do repositório), o ID, quando ele foi criado e o tamanho da imagem.

```shell
$  docker pull ubuntu:xenial
$  docker image list
```
Em seguida, utilizando o comando **run**, criamos e inicializamos o contêiner. Para mantê-lo ativo passamos o argumento **-i**, juntamente com o **-t** para ligar um terminal a ele. Como sufixo deve ser colocado o comando específico que deseja, como por exemplo **bash**. Dessa forma, temos um terminal em que pode ser feito alterações no contêiner, instalar pacotes etc. Os contêineres que foram criados podem ser listados utilizando o comando **ps**, junto às informações de quando foi criado, o *status*, o comando utilizado e os IDs.

```shell
$  docker run -ti ubuntu:xenial bash
$  docker ps
```

Perceba que se não dermos um nome a ele, irá aparecer um nome aleatório. Para definir um nome deve ser utilizando a opção **--name**  seguida do nome do contêiner. Aqui você pode visualizar que cada vez que for executado o comando **run** um novo contêiner será criado com base na imagem especificada.

```shell
$  docker run --name [NAME] -ti ubuntu:xenial bash
$  docker ps
```

Para fechar estes terminais criados podemos digitar **exit** ou **Ctrl+D**, no terminal do container, ou de outro terminal utilizando o comando **stop**. Para inicializá-los novamente o comando é **start** seguido do nome ou ID do contêiner.

```shell
$  docker stop [NAME]
$  docker ps -all #para checar todos os contêineres, inclusive os fechados
$  docker start [NAME]
```

Perceba que fechar não significa apagá-los, se for este o objetivo o comando é **rm** e se o objetivo for apagar a imagem utiliza-se **rmi**.

```shell
$  docker rm [NAME]  
$  docker rmi [IMAGE NAME]
```

Cuidado ao utilizar tais comandos! Contêineres uma vez deletados não podem ser recuperados. Caso deseje salvá-los, crie uma nova imagem, realizando um **commit**, assim a nova imagem irá herdar as características da imagem que foi criado + as modificações feitas. Uma boa prática é *subir*  suas imagens um **push** para o seu repositório no **Docker Hub**, similar ao que é feito com o *GitHub*.

```shell
$  docker container commit [CONTAINER-NAME] [REPOSITORY-NAME]
$  docker push [REPOSITORY-NAME]
```

Quando desejamos reutilizar um dado contêiner, devemos realizar um *start* e executar os comandos utilizando o **exec**. Com este comando podemos reeiniciar o terminal da seguinte maneira.

```shell
$  docker start [NAME]  
$  docker exec -ti [NAME] bash
```

Estes foram os comandos básiscos para você começar a usar e compartilhar contêineres. Ficou com alguma dúvida? Entre em contato com a gente pelos comentários! :)

<br>
<br>
<!--equipe-->
<center><h3 class="post-title">Autora</h3><br/></center>
<div class="row">
  <div class=" col-xl-auto offset-xl-0 col-lg-4 offset-lg-0">
    <table class="table-borderless highlight">
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




<br>
<hr class="mark">
<div id="full-tags-list">
<h3 class="post-title"><font color="#fbb117">Posts</font></h3>
  {%- for tag in tags_list -%}
      <h4 id="{{- tag -}}" class="linked-section">
          <i class="fas fa-tag" aria-hidden="true"></i>
          &nbsp;{{- tag -}}&nbsp;({{site.tags[tag].size}})
      </h4>
      <div class="post-list">
          {%- for post in site.tags[tag] -%}
              <div class="tag-entry">
                  <a href="{{ post.url | relative_url }}">{{- post.title -}}</a>
                  <div class="entry-date">
                      <time datetime="{{- post.date | date_to_xmlschema -}}">{{- post.date | date: date_format -}}</time>
                  </div>
              </div>
          {%- endfor -%}
      </div>
  {%- endfor -%}
</div>

