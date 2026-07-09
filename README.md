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