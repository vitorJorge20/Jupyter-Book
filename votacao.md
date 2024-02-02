<style>
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# 4.1 Votação por maioria e soft voting

A votação por maioria é uma estratégia intuitiva e de simples implementação. A decisão de classificação é tomada em favor da classe com maior frequência de predição pelos classificadores que constituem a combinação, como mostrado na Figura 4.1.

<div align="center"> 

![figura41](images/figura41.png "figura 4.1") <legend>Figura 4.1 - Representação da estratégia de votação majoritária.</legend></div>

O soft voting é uma técnica de aprendizado de máquina que combina as previsões de vários modelos para gerar uma única previsão. Ele é diferente da votação majoritária, que simplesmente escolhe a previsão mais comum dos modelos. No soft voting, cada modelo atribui uma probabilidade a cada classe. Essas probabilidades são então combinadas para gerar uma nova probabilidade para cada classe. A classe com a probabilidade mais alta é então escolhida como a previsão final. A Figura 4.2 ilustra a estratégia.

<div align="center"> 

![figura42](images/figura42.png "figura 4.2") <legend>Figura 4.2 - Representação da estratégia soft voting.</legend></div>

Outra maneira de implementar o soft voting é usar uma função de ponderação. A função de ponderação atribui pesos a cada modelo, de modo que as previsões dos modelos mais confiáveis tenham mais peso.
