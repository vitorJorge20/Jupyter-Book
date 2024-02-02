<style>
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# 4.5 Boosting

O boosting é uma técnica de aprendizado de máquina que combina vários classificadores base para criar um classificador forte. Os classificadores base são modelos que são capazes de aprender com os dados, mas que ainda cometem erros. Esse algoritmo funciona treinando os classificadores base sequencialmente, onde cada classificador é treinado para corrigir os erros cometidos pelos classificadores anteriores.Isso significa que os modelos seguintes dão mais atenção aos dados que foram classificados incorretamente nas etapas anteriores, como se pode reconhecer na Figura 4.6:

<div align="center"> 

![figura46](images/figura46.png "figura 4.6") <legend>Figura 4.6 - Representação da estratégia boosting.</legend></div>

O boosting é uma técnica poderosa que pode ser usada para resolver uma ampla gama de problemas de aprendizado de máquina. É especialmente eficaz em problemas onde os classificadores base individuais são capazes de aprender com os dados, mas ainda cometem erros.

Alguns dos algoritmos de boosting mais populares incluem:

- AdaBoost: Este algoritmo atribui pesos aos exemplos de dados de acordo com o grau em que são difíceis de prever;

- Gradient Boosting: Este algoritmo usa o gradiente da função de perda para ajustar os pesos dos exemplos de dados;

- XGBoost: Este algoritmo é uma versão acelerada do gradient boosting.Ele se baseia em árvores de decisão, combinando várias árvores fracas para criar uma árvore forte.
