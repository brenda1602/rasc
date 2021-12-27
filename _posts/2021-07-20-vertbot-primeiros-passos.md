---
layout: post
title: Primeiros passos
subtitle: Testes de sensores e iniciando o Gazebo
cover-img: /assets/img/vertbot/jukan-tateisi-bJhT_8nbUA0-unsplash.jpg
thumbnail-img: /assets/img/vertbot/vertbot_model.png
share-img: /assets/img/rosa-logo-redondo.png
author: Breno Portela
comments: true
tags: [vertbot]
---

### Testando os sensores do Vertbot

Nesta etapa de desenvolvimento foi feita a pesquisa dos pacotes e das bibliotecas necessárias para o funcionamento dos diversos sensores presentes no projeto, seguido do teste e integração dos sensores com o ROS operando na Jetson Nano. Nos testes feitos com os sensores de corrente e de tensão foi verificada uma inconsistência do valor apresentado como resultado para o valor real que estava sendo medido, devido a uma não linearidade nas respostas dos sensores. 

![Teste Corrente](../assets/img/vertbot/test_current_sensor.jpg){: height="550"}  ![Teste Tensão](../assets/img/vertbot/test_voltage_sensor.jpg){: height="550"} 

Devido a isso, foi levantada a curva das suas respostas analógicas de saída em função das suas entradas e feita uma linearização na faixa de operação que a alimentação do robô estará operando. No teste de tensão foi medida a tensão sobre uma fonte de tensão chaveada e no teste de tensão de corrente foi medida a corrente passando por um resistor de 1R2.

![Gráfico Corrente](../assets/img/vertbot/graph_current_sensor.png){: width="45%"}  ![Gráfico Tensão](../assets/img/vertbot/graph_voltage_sensor.png){: width="45%"} 

<br>

<div>
    <img align="left" src = "{{ 'assets/img/vertbot/test_sonar.jpg' | relative_url }}" width="45%" class="float-left">
    <p style="padding-left: 50%;">Os sensores de corrente, de tensão e o sensor ultrassônico são sensores com resposta analógica de até 5 V, tensão não suportada pelas portas analógicas da Jetson Nano. Portanto tais sensores serão ligados a um microprocessador Arduino Nano, sendo necessário o pacote rosserial para a integração das respostas do Arduino com o ROS operando na Jetson Nano. No teste do sensor ultrassônico foram medidas diversas distâncias com o sensor e comparadas com os valores obtidos com uma fita métrica para avaliar os resultados.</p>
</div>

<br><br>

O pacote disponível para a câmera estéreo Mynt Eye foi desenvolvido para o Ubuntu 18.04, porém a versão usada na Jetson Nano é a 20.04, sendo necessário o uso do container [Docker](https://www.docker.com/resources/what-container) com a versão 18.04 do Ubuntu para utilizar o pacote. Na Imagem abaixo podemos ver a imagem de ambas câmeras da Mynt Eye sendo exibidas no Rviz do ROS.

![Teste Mynt Eye](../assets/img/vertbot/test_mynt-eye.jpg){: width="100%"}

Os demais sensores, a Câmera Raspberry Pi V2 e o lidar LDS-01, apresentaram respostas coerentes com as bibliotecas encontradas no estudo da arte desenvolvido.

![Teste V2](../assets/img/vertbot/test_camera_v2.jpg){: height="650"}  ![Teste LiDAR](../assets/img/vertbot/test_lidar.jpg){: height="650"}

### Desenvolvimento do URDF

Após a atualização da estrutura do modelo do robô, foi dado o início da montagem do _workspace_ e da construção do arquivo URDF (Unified Robot Description Format) para inicializar a simulação. Alguns ajustes serão feitos futuramente no chassis para adicionar os encaixes do sensor de corrente, sensor de tensão e shield do motor, além do desenvolvimento de uma peça de encaixe da _caster ball_ e possíveis redimensionamentos para o encaixe de peças que estão em processo de compra. Com o workspace da simulação já iniciado, é possível começar os testes de sensores via simulação para a criação da rede de sensores e os testes de interação entre eles, além do desenvolvimento dos algoritmos e das funcionalidades abordadas no projeto.

![Modelo Gazebo](../assets/img/vertbot/vertbot_gazebo.png){: width="100%"}

<br>

---------------------
<br>

<!-- autor -->
<center><h3 class="post-title">Autor</h3><br/></center>
<div class="row">
  <div class="col-xl-auto offset-xl-0 col-lg-4 offset-lg-0 center">
    <table class="table-borderless highlight">
      <thead>
        <tr>
          <th><img src="{{ 'assets/img/people/breno-1.png' | relative_url }}" width="100" alt="breno" class="img-fluid rounded-circle" /></th>
        </tr>
      </thead>
      <tbody>
        <tr class="font-weight-bolder" style="text-align: center margin-top: 0">
          <td>Breno Portela</td>
        </tr>
        <tr style="text-align: center" >
          <td style="vertical-align: top"><small>Engenheiro Mecânico - Senai Cimatec. Líder da équipe Vertbot.</small></td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<br>