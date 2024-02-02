<style>
    h1 {
        font-size: 39px;
    }
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# Capítulo 4: Combinação de classificadores

A aplicação dos algoritmos de classificação depende diretamente da características dos dados e seu contexto e, embora existam muitos tipos de classificadores, a escolha de um só não é suficiente para distinguir as classes dos dados de forma eficiente e robusta. O aprendizado em conjunto é  uma vertente que busca ampliar essas possibilidades dos métodos de classificação, ao combinar classificadores conhecidos para resolver os problemas de distinção de classes.

A combinação dos classificadores tem como objetivo explorar as melhores características que diferentes classificadores desempenham diante de uma aplicação. Ao unir esses modelos ajustados é esperado que se obtenha um desempenho de classificação mais robusto e menores taxas de erro.

As técnicas de combinação são diversas e podem ser aplicadas tanto na saída dos classificadores quanto nas etapas de ajuste dos algoritmos. Além disso, os modelos podem dispor ou não de técnicas de otimização, o que aumenta ainda mais as possibilidades dos arranjos. A seguir, são apresentados os algoritmos de aprendizado em conjunto mais comumente utilizados em problemas de classificação.