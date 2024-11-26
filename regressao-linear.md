# Regressão linear

> Material criado a partir das aulas do curso Machine Learning Crash Course do Google disponível no [link] (https://developers.google.com/machine-learning/crash-course).

## Definição
Regressão linear é uma técnica estatística utilizada para encontrar a relação entre variáveis. No contexto de machine learning (ML), a regressão linear encontra a relação entre os **features** (variáveis de entrada de um modelo de ML) e **labels** (em modelos supervisionados, é a "resposta" ou "resultado").

## Equação de regressão linear
Em ML, a equação para um modelo de regressão linear está descrito abaixo:
$$
y'= {b + w_1x_1}
$$
onde,
* $y'$ é a saída prevista (label).
* $b$ é o viés (bias) do modelo. Bias seria o mesmo que o intercepto de uma equação algébrica para uma linha. Em ML, algumas vezes o bias é referido como sendo $w_0$. *Bias é um parâmetro do modelo e é calculado durante o treinamento*.
* $w_1$ é o peso do valor de entrada (feature). Peso seria o mesmo conceito que a inclinação da curva $m$ de uma equação algébrica para uma linha. *Peso é um parâmetro do modelo e é calculado durante o treinamento*.
* $x_1$ é o valor de entrada (feature).

> [!NOTE]
> Durante o treinamento, o modelo calcula o peso e o bias que produz o melhor modelo.

## Modelos com multiplos valores de entrada (features)
Em ML, a equação para um modelo de regressão linear com multiplos features está descrita abaixo:
$$
y'={b + w_1x_1 + w_2x_2 + w_3x_3 + w_4x_4 + w_5x_5}
$$
Nesse modelo, cada feature tem seu próprio peso ($w_1, w_2, etc$).

## Perda
Perda é uma métrica numérica que descreve o quão erradas as predições do modelo estão erradas. Em outras palavras, a perda mede a distância entre a predição do modelo e os valores reais (labels).
O objetivo do treinamento do modelo é minimizar a perda, a reduzindo para o menor valor possível.

Na imagem abaixo, as setas indicam a perda entre os pontos de dados para o modelo. As setas indicam o quão distante a predição está dos valores reais.

<img src=https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/loss-lines.png>


## Distância da perda
Em estatística e aprendizado de máquina, a perda mede a diferença entre os valores previstos e reais. A perda se concentra na distância entre os valores, não na direção.
Por exemplo, se o modelo prevê 2, mas o valor real é 5, não importa que a perda seja negativa $-3(2-5=-3)$. O que importa é que a distância entre os valores é 3.
Os dois métodos mais comuns para remover o sinal são:
* Tomar o valor absoluto da diferença entre o valor real e o previsto.
* Elevar a diferença entre o valor real e o previsto ao quadrado.

## Tipos de perda
Em regressão linear, existem 4 tipos de perda:
| Tipo de perda | Definiçao | Equação |
| - | - | - |
| Perda $L_1$ | A soma dos valores absolutos da diferença entre os valores previstos e os valores reais. | $\sum \|valor real - valor previsto\|$ |
| Erro médio absoluto (MAE) | A média das perdas de $L_1$ em um conjunto de exemplos. | $\frac{1}{n} \sum \|valor real - valor previsto\|$ |
| Perda $L_2$ | A soma da diferença ao quadrado entre os valores previstos e os valores reais. | $\sum (valor real - valor previsto)^2$ |
| Erro quadrático médio (EQM) | A média das perdas de $L_2$ em um conjunto de exemplos. | $\frac{1}{n} \sum (valor real - valor previsto)^2$ |

A diferença funcional entre a perda $L_1$ e a perda $L_2$ (ou entre MAE e MSE) é o quadrado. Quando a diferença entre a predição e o valor real é grande, o quadrado aumenta ainda mais a perda. Quando a diferença é pequena (menos de 1), o quadrado torna a perda ainda menor.

## Como escolher uma perda
A decisão de usar MAE ou MSE pode depender do conjunto de dados e da forma como você quer processar determinadas previsões. A maioria dos valores de recursos em um conjunto de dados geralmente fica em um intervalo distinto. 
Se um valor estiver fora do intervalo distindo ele poderia ser considerado um **outlier**. 
**Outlier** também pode se referir a o quão distante a predição de um modelo está dos valores.

Ao escolher a melhor função de perda, devemos considerar como queremos que o modelo trate valores outliers. 
Por exemplo, o MSE move o modelo mais na direção dos outliers, enquanto o MAE não. A perda de $L_2$ incorre em uma penalidade muito maior para um outlier do que a perda de $L_1$. Por exemplo, as imagens a seguir mostram um modelo treinado com o MAE e um modelo treinado com o MSE. A linha vermelha representa um modelo totalmente treinado que será usado para fazer previsões. Os outliers estão mais próximos do modelo treinado com o MSE do que do modelo treinado com o MAE.

<img src=https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/model-mse.png>

> Um modelo treinado com MSE se aproxima dos valores outliers.

<img src=https://developers.google.com/static/machine-learning/crash-course/linear-regression/images/model-mae.png>

> Um modelo treinado com MAE está mais distante dos outliers.

Observe a relação entre o modelo e os dados:
* **MSE**. O modelo está mais próximo dos outliers, mas mais distante da maioria dos outros pontos de dados.
* **MAE**. O modelo está mais longe dos outliers, mas mais próximo da maioria dos outros pontos de dados.