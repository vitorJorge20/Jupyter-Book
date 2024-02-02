<style>
    main {
        text-align: justify;
    }
    legend {
        font-size: 16px;
    }
</style>

# 2.3 Estimativa baseada na soma dos erros quadráticos

Uma alternativa de classificador linear é modelada com base no conceito de soma dos erros quadráticos (SSE - $\textit{Sum of Squared Errors}$). De forma análoga ao Perceptron, iniciamos com a suposição de disponibilidade de $D = \{(\textbf{x}_{i},y_{i}) \in \textit{X} \times \textit{Y}: i=1,...,m\}$ e que o processo de aprendizado é verificado com base nos valores retornados por $J(\textbf{w})$, sendo $\textbf{w} = [ω_{0},ω_{1},...,ω_{n}]^{T}$ o vetor que parametriza a função e superfície de decisão linear. Nesta abordagem, tal função é definida por:

<div align="center">

  $\begin{equation}
  J(\textbf{w})=\sum_{i=1}^{m} (y_{i}-\textbf{x}^{T}\textbf{x})^{2} \tag{2.8}
  \end{equation}$

Sabendo que a minimização de $J(\textbf{w})$ leva a $\textbf{w}$, cujos erros de classificação proporcionados são mínimos, desenvolvemos a seguinte relação:

$\begin{equation}
\frac{∂J(\textbf{w})}{∂\textbf{w}} = 0 ⇔ \frac{∂\sum_{i=1}^{m} (y_{i}-\textbf{x}^{T}\textbf{x})^{2} }{∂\textbf{w}} = 0 ⇔ -2\sum_{i=1}^{m} y_{i}\textbf{x}_{i}^{T} + 2\sum_{i=1}^{m} y_{i}\textbf{x}_{i}^{T}\textbf{w} = 0 ⇔ \textbf{w}\sum_{i=1}^{m} \textbf{x}_{i}\textbf{x}_{i}^{T} = \sum_{i=1}^{m} y_{i}\textbf{x}_{i}^{T} \tag{2.9}
\end{equation}$ </div>

É importante observar que $\sum_{i=1}^{m}\textbf{x}_{i}\textbf{x}_{i}^{T}$ prorpociona uma matriz quadrada como resultado, assim como $\sum_{i=1}^{m} y_{i}\textbf{x}_{i}^{T}$ gera um vetor. Denominado tal matriz e o vetor por $\textbf{A}$ e $\textbf{b}$, respectivamente, a Equação 2.9 torna-se equivalente a:

<div align="center">

$\begin{equation}
\textbf{w} = \textbf{A}^{-1}\textbf{b} \tag{2.10}
\end{equation}$ </div>

O uso desta técnica implica em resultados similares aos proporcionados pelo algoritmo Perceptron associado à estratégia de relaxamento.

-

```
#Implementação de função para cálculo de w segundo o método SSE

def SSE(x,y):
  dim = x.shape[1] #Dimensão dos padrões
  w = np.zeros(dim+1) #w como vetor do "espaço estendido"

  #Definindo uma matriz (n+1)x(n+1), sendo n = dim
  A = np.zeros((x.shape[1]+1, x.shape[1]+1))

  #Definindo uma matriz/vetor 1x(n+1)
  b = np.zeros(x.shape[1]+1)

  #Cálculo de "A" e "b"
  for xi, yi in zip(x,y):
    A += (np.asmatrix(np.hstack((1,xi))).T).dot(np.asmatrix(np.hstack(np.hstack((1,xi)))))

    b += yi*np.hstack((1,xi))

  w = b.dot(np.linalg.inv(A)) #w = inversa(A)*b
  return w
```