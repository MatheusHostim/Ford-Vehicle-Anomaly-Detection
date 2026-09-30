# Ford Vehicle Anomaly Detection

Projeto desenvolvido durante a Sprint 3 de Inteligência Artificial & Machine Learning da FIAP, dentro do Challenge realizado em parceria com a Ford.

O projeto trabalha com especificações técnicas de veículos e utiliza um Autoencoder para encontrar possíveis dados que fogem do padrão.

> **Status:** projeto acadêmico concluído.

## Integrantes

| Nome | RM | GitHub |
| --- | --- | --- |
| Eduardo da Silva Lima | RM554804 | [@Eduardo-25](https://github.com/Eduardo-25) |
| Estevam Melo | RM555124 | [@StkStevens](https://github.com/StkStevens) |
| Enzo Bonacasata Motta | RM555372 | [@Enzo-B-Motta](https://github.com/Enzo-B-Motta) |
| Guilherme Ulacco | RM558418 | [@GuilhermeUcadete](https://github.com/GuilhermeUcadete) |
| Matheus Hostim | RM556517 | [@MatheusHostim](https://github.com/MatheusHostim) |

---

## O desafio

O desafio escolhido pelo grupo envolve a consulta de especificações técnicas de veículos.

A partir da marca, modelo e versão de um veículo, a ideia é permitir a consulta de diferentes atributos, como motor, potência, torque, transmissão, tração, rodas, pneus e outros dados técnicos.

Caso alguma das informações procuradas não esteja disponível, o sistema deve deixar isso claro.

Dentro da Sprint de Inteligência Artificial & Machine Learning, também precisávamos desenvolver uma solução de Machine Learning relacionada ao desafio, passando pela preparação dos dados, treinamento, comparação de diferentes configurações e avaliação dos resultados.

## Nossa solução

Para a parte de Machine Learning, utilizamos um Autoencoder para tentar encontrar possíveis anomalias nas especificações técnicas dos veículos.

Como não utilizamos uma base real completa de veículos nessa etapa, foi criada uma base sintética para os testes.

Entre as informações utilizadas estão:

- Motorização
- Número de cilindros
- Potência
- Torque
- Número de marchas
- Tempo de 0 a 100 km/h
- Tamanho das rodas
- Largura e perfil dos pneus
- Tração
- Modos de condução
- Modos de volante
- Modos de escapamento
- Modos de amortecedor
- Faróis Matrix LED

A base foi criada com 1000 registros considerados normais e outros 200 registros com alterações propositalmente fora do padrão para serem usados como anomalias.

O Autoencoder foi treinado apenas com os registros normais para aprender o padrão desses dados.

Depois do treinamento, utilizamos o erro de reconstrução para verificar quais registros se afastavam mais do padrão aprendido pelo modelo.

## Configurações testadas

Foram testadas três configurações do Autoencoder, alterando o tamanho do gargalo da rede.

| Configuração | Gargalo | Accuracy | Precision | Recall | F1 |
| --- | ---: | ---: | ---: | ---: | ---: |
| 1 | 4 | 0,7975 | 0,8993 | 0,6700 | 0,7679 |
| 2 | 2 | 0,7825 | 0,9124 | 0,6250 | 0,7418 |
| 3 | 6 | 0,7825 | 0,9124 | 0,6250 | 0,7418 |

Entre as três configurações testadas, o modelo com gargalo de 4 neurônios apresentou o melhor resultado geral, principalmente considerando Accuracy, Recall e F1.

Por isso, essa configuração foi escolhida como modelo final.

O objetivo do Autoencoder não é afirmar com certeza que uma informação está errada. Ele serve como uma forma de encontrar registros que fogem do padrão e que talvez precisem ser revisados.

## Validação com a Ranger Raptor

Além da parte de Machine Learning, também foi criada uma função para consultar os atributos técnicos de um veículo.

Para validar essa parte do projeto, utilizamos a Ford Ranger Raptor como exemplo.

Entre os dados consultados estão:

- Motor V6 3.0L Nano bi turbo
- Potência de 397 cv
- Torque máximo de 583 Nm
- Transmissão automática de 10 velocidades
- Tração 4WD
- Aceleração de 0 a 100 km/h em 5,8 segundos
- Modos de condução
- Faróis Matrix LED
- Rodas e pneus

A função recebe a marca, modelo, versão e os atributos desejados. Caso algum atributo não esteja cadastrado, é retornado `Não disponível`.

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Scikit-learn
- TensorFlow
- Keras
- Matplotlib
- Google Colab / Jupyter Notebook

## Como executar

O projeto foi desenvolvido em um notebook `.ipynb` e pode ser executado pelo Google Colab ou Jupyter Notebook.

### Google Colab

1. Abra o arquivo `.ipynb` no Google Colab.
2. No menu superior, selecione a opção para executar todas as células.
3. Os dados sintéticos serão gerados durante a execução.
4. Os Autoencoders serão treinados e avaliados.
5. Ao final serão mostradas as métricas das três configurações e a consulta da Ranger Raptor.

Não é necessário baixar uma base de dados separada, já que os dados utilizados nos testes são gerados dentro do próprio notebook.

## Estrutura do projeto

```text
Ford-Vehicle-Anomaly-Detection/
│
├── README.md
└── Ford_Vehicle_Anomaly_Detection.ipynb
```

## Limitações e possíveis melhorias

Os dados utilizados no treinamento são sintéticos, então os resultados representam o cenário criado para os testes do projeto.

A consulta de veículos também funciona atualmente como um protótipo, com os dados cadastrados diretamente no código.

Como melhoria, seria possível utilizar uma base real com uma quantidade maior de veículos e fazer a consulta das especificações através de uma fonte externa de dados.
