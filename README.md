# Desafio Técnico - Cientista de Dados Junior
## Time de IA - Casa Civil / IplanRio

# Parte 1: Análise Exploratória

Na primeira parte, eu me concentrei em fazer o import dos dados com pandas, verificar como eles foram importados, os tipos e se existem dados faltantes, o que não era o caso. 

Em seguida, eu adicionei uma feature no dataset que é a zona da cidade na qual o bairro está inserido. Isso é útil principalmente para facilitar a visualização, visto que os bairros de uma mesma zona **tendem** a ter problemas semelhantes, especialmente na zona sul e centro. 

Após verificar a integridade dos dados, a primeira questão foi verificar qual a principal ocorrência e a sua distribuição.

![Texto Alternativo](results/figures/grafico_frequencia_ocorrencias_global.png)

| Categoria | Porcentagem |
|---|---|
| iluminacao_publica | 22.86% |
| buraco_via | 18.16% |
| coleta_lixo | 16.12% |
| esgoto_vazamento | 12.42% |
| poda_arvore | 9.16% |
| estacionamento_irregular | 8.74% |
| barulho_perturbacao | 8.00% |
| sinalizacao | 4.54% |

Também foi verificada a distribuição de chamados por canal:
![Texto Alternativo](/results/figures/grafico_frequencia_canal_global.png)

A distribuição dos chamados por bimestre também foi verificada:

![Texto Alternativo](/results/figures/grafico_frequencia_ocorrencias_bimestral.png)

A partir daí verificamos que a porcentagem de chamados de cada categoria estava flutuando no tempo, principalmente a quantidade de buracos.

| Categoria | 1º Bimestre | 3º Bimestre | Variação (p.p.) |
|---|---|---|---|
| barulho_perturbacao | 7.87% | 8.18% | +0.31 |
| iluminacao_publica | 23.42% | 23.00% | -0.43 |
| coleta_lixo | 15.68% | 16.48% | +0.80 |
| estacionamento_irregular | 9.12% | 8.41% | -0.71 |
| esgoto_vazamento | 12.49% | 12.30% | -0.19 |
| buraco_via | 18.68% | 17.16% | -1.51 |
| poda_arvore | 8.56% | 9.44% | +0.88 |
| sinalizacao | 4.18% | 5.03% | +0.85 |

Verificamos também que a variação no uso do canal por bimestre: 

![Texto Alternativo](/results/figures/grafico_frequencia_canal_bimestral.png)

E a quantidade de chamados por zona da cidade:

![Texto Alternativo](/results/figures/grafico_frequencia_ocorrencias_zona.png)

# Parte 2: Auditoria do modelo.

Inicialmente, foram calculadas as métricas de precision, recall e F1-Score do modelo A utilizando o classification report do scikit-learn, ele já entrega as 3 métricas de uma vez. 

Mas para além da métrica em si foi necessário o intervalo de confiança, este foi calculado com o uso do bootstraping, ou seja, as métricas foram calculadas 2000 vezes em ambientes próximos do original, mas com alguns pares de predição e resposta sendo repetidos enquanto outros ficam de fora.

O processo é simples, um vetor com n índices com valores de 0 até n é instanciado e utilizado como índice dos valores de y_pred e y_true a serem utilizados no step.

Com esses arrays de labels as métricas são calculadas, salvas em uma matriz e o processo é repetido. Por fim o alpha é calculado e os valores que marcam o início das caldas superior e inferior são selecionados. Com essas faixas foi fácil preencher a tabela:

| Categoria | Precision | IC95% (Precision) | Recall | IC95% (Recall) | F1-score | IC95% (F1) | Support |
|---|---|---|---|---|---|---|---|
| barulho_perturbacao | 0.80 | [0.761, 0.838] | 0.78 | [0.732, 0.817] | 0.79 | [0.756, 0.819] | 400 |
| buraco_via | 0.66 | [0.635, 0.692] | 0.82 | [0.792, 0.841] | 0.73 | [0.710, 0.755] | 908 |
| coleta_lixo | 0.81 | [0.787, 0.843] | 0.81 | [0.779, 0.832] | 0.81 | [0.789, 0.831] | 806 |
| esgoto_vazamento | 0.71 | [0.673, 0.749] | 0.58 | [0.538, 0.617] | 0.64 | [0.605, 0.670] | 621 |
| estacionamento_irregular | 0.80 | [0.762, 0.837] | 0.83 | [0.790, 0.859] | 0.81 | [0.784, 0.840] | 437 |
| iluminacao_publica | 0.86 | [0.835, 0.878] | 0.79 | [0.769, 0.815] | 0.82 | [0.806, 0.842] | 1143 |
| poda_arvore | 0.80 | [0.766, 0.840] | 0.78 | [0.737, 0.813] | 0.79 | [0.759, 0.817] | 458 |
| sinalizacao | 0.74 | [0.686, 0.797] | 0.80 | [0.742, 0.848] | 0.77 | [0.724, 0.809] | 227 |
| **macro avg** | 0.77 | [0.761, 0.787] | 0.77 | [0.757, 0.784] | 0.77 | [0.757, 0.782] | 5000 |

# 3. Onde o Modelo Falha?

Nesse capítulo, foi calculada uma simples matriz de confusão:


![Texto Alternativo](/results/figures/grafico_confusao_modelo_a.png)

Também defini uma funcão bem simples que particiona o dataset por algum valor de atributo e em seguida calcula a acurácia do modelo A para cada valor do atributo. Foi utilizado tanto no cal de comunicação como no bairro.