<style>
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# 4.4 Bagging

A estratégia de bagging começa por amostrar os dados originais com reposição, gerando um conjunto de dados bootstrap. Isso significa que cada ponto de dados original tem uma probabilidade igual de ser amostrado mais de uma vez.

Cada conjunto de dados bootstrap é então usado para treinar um modelo de aprendizado de máquina, como uma árvore de decisão, uma rede neural ou um SVM. Os resultados dos modelos são então agregados para produzir uma previsão final. A agregação pode ser feita por votação ou por média. A Figura 4.5 apresenta a estratégia.

<div align="center"> 

![figura45](images/figura45.png "figura 4.5") <legend>Figura 4.5 - Representação da estratégia bagging.</legend></div>

A estratégia de bagging funciona melhor para algoritmos de aprendizado de máquina que são propensos ao overfitting. O overfitting ocorre quando um modelo se ajusta muito bem aos dados de treinamento, mas não é capaz de generalizar para novos dados. A estratégia de bagging ajuda a reduzir o overfitting, gerando vários modelos diferentes que são menos propensos a se ajustarem aos dados de treinamento de forma excessiva.