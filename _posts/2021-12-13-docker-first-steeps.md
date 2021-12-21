---
layout: post-page
title: Docker
subtitle: Ferramenta para criar e compartilhar containers
cover-img: /assets/img/page-docker/container2.jpg
thumbnail-img: assets/img/page-docker/homepage-docker-logo.png
share-img: /assets/img/rosa-logo-redondo.png
comments: true
tags: [docker, rasc]
---

<center><img src="{{ 'assets/img/page-docker/homepage-docker-logo.png' | relative_url }}" alt="Docker logo" width="380"/></center>

<div class="before-content">
  <center>
    {%- for tag in tags_list -%}
      <br>
      <a href="#{{- tag -}}" class="btn btn-primary tag-btn"><i class="fas fa-tag" aria-hidden="true"></i>&nbsp;{{- tag -}}-posts&nbsp;({{site.tags[tag].size}})</a>
    {%- endfor -%}
  </center>    
  <!--hr class="mark"-->
</div>

<!-- ## Introdução -->
Docker é uma plataforma *open source* para desenvolver, compartilhar e rodar aplicações em um ambiente isolado chamado de **contêiner**. Utilizando contêineres é possível empacotar todo o código e suas dependências (ferramentas do sistema, biliotecas) que podem ser compartilhadas e utilizadas em diferentes máquinas de forma segura e rápida. A ferramenta foi iniciada em 2013 pela *Docker Engine*, para sistemas Linux e devido ao sucesso foi expandida para o sistema *Windows*.

### O que é *container?*
<!--objetivo, data-->
É uma unidade padrão de software, um ambiente isolado no qual é empacotado o código e todas as suas dependências. De maneira superfical, funciona com uma máquina virtual modularizada, pois não precisa copiar informações do sistema operacional e criar um novo ambiente para cada aplicação, como mostra a comparação feita na imagem abaixo. Um contêiner utiliza o mesmo *kernel* do sistema operacional, que inclusive é compartilhado com os demais contêires em execução, permitindo a comunicação entre eles. Então, é perceptível a melhoria na rapidez das aplicações e menor uso de espaço do servidor.


<table class="table-borderless highlight">
  <thead>
    <tr>
      <th><center><img src="{{ 'assets/img/page-docker/container-vm-whatcontainer_2.png' | relative_url }}" alt="Semelhantes" width="600" /></center></th>
      <th><center><img src="{{ 'assets/img/page-docker/docker-containerized-appliction-blue-border_2.png' | relative_url }}" alt="Semelhantes" width="600"/></center></th>
    </tr>
  </thead>
</table>

Contêineres são criados utilizando uma **imagem docker**, que consiste em um arquivo de leitura com as intruções para configurar o ambiente. Estas imagens são armazenas no *Docker Hub*, um repositório de imagens docker, no qual você pode encontrar imagens padrões, como diferentes versões do ubuntu, armazenar as suas próprias, enviar novas versões e compartilhá-las com o mundo. Geralmente imagens são criadas baseando-se em outras imagens, adicionando modificações conforme a necessidade, mas também é possível criá-las do zero, escrevendo um *Dockerfile*.

## Por que usar Docker?

Tratando de desenvolvimento, é muito comum que você se depare com problemas de incompatibilidade de sistemas. Este problema pode ser resolvido ao rodar um contêiner com a imagem do sistema desejado, por exemplo, é possível rodar um contêiner com o ubuntu 18.04 em uma máquina com o ubuntu 20.04 instalado e vice-versa. Além disso, em um trabalho em equipe pode ser necessário que se tenha o mesmo ambiente (com as mesmas dependências) em diferentes máquinas, o que também pode ser facilitado utilizando contêineres, ao compartilhar uma mesma imagem entre o grupo.


----------------------------------------------------------------
Se você se interessou por essa ferramenta, acompanhe as nossas instruções de como rodar um *container* e outras dicas de como utilizar o **ROS** nesta ferramenta!

- [Como usar um container?](https://mhar-vell.github.io/rasc/2021-12-13-docker-instructions/)
- [ROS + Docker](https://mhar-vell.github.io/rasc/2021-12-13-docker-ROS/)



<br>
<hr>

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
