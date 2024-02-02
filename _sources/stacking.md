<style>
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# 4.2 Stacking

A estratégia conhecida como $\textit{stacking}$ consiste na obtenção de um classificador que toma decisões baseadas em decisões anteriores, obtidas por um conjunto de classificadores. Portanto, o processo combina classificadores através de um outro classificador. A Figura 4.3 demonstra a estratégia descrita.

<div align="center"> 

![figura43](images/figura43.png "figura 4.3") <legend>Figura 4.3 - Representação da estratégia de stacking.</legend></div>

O conjunto de amostras $D$ é dividido em dois subconjuntos, $D_{1}$ e $D_{2}$. Em seguida, o conjunto $D_{1}$ é utilizado para ajustar $N$ classificadores, que são os modelos base. Posteriormente, um modelo final é treinado usando o conjunto $D_{2}$ e as previsões dos modelos base como dados de entrada. O classificador final aprende a combinar as previsões dos modelos base para gerar uma previsão mais precisa.

Os modelos base podem ser diferentes tipos de classificadores como regressão logística, ávore de decisão, SVM e etc. Possui custo computacional elevado, porém é considerada uma estratégia flexível e robusta. O stacking pode ser aplicado tanto em problemas de classificação, quanto em problemas de regressão.
