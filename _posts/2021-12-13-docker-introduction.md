---
layout: post-page
title: Docker
subtitle: Ferramenta para criar e compartilhar containers
---
{% assign date_format = site.date_format | default: "%B %-d, %Y" %}
{%- capture site_tags -%}
    {%- for tag in site.tags -%}
      {% if tag contains 'docker' %}
        {{- tag | first -}}{%- unless forloop.last -%},{%- endunless -%}
      {% endif %} 
    {%- endfor -%}
{%- endcapture -%}
{%- assign tags_list = site_tags | split:',' | sort -%}

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

Se você se interessou por essa ferramenta, veja o próximo post com as intruções de como rodar um *container*!
<br>

<hr>

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

