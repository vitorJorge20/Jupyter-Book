<style>
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# Capítulo 1: Teoria da decisão de Bayes


A Regra de Bayes, demonstrada na equação 1, é uma equação que relaciona a ocorrência de dois eventos através de suas probabilidades condicionais. Ela é utilizada para calcular a probabilidade de um evento ocorrer, dado que outro evento já ocorreu.

<div align="center">

$\begin{equation}
    P(A|B) = \frac{\text{P(B|A)P(A)}}{\text{P(B)}}\
\end{equation}$ </div>

Onde:


*   P(A|B) é a probabilidade do evento A ocorrer dado que o evento B já ocorreu;
*   P(B|A) é a probabilidade do evento B ocorrer dado que o evento A já ocorreu;
*   P(A) é a probabilidade do evento A ocorrer independentemente do evento B;
*   P(B) é a probabilidade do evento B ocorrer independentemente do evento A.

Como ponto de partida, vamos admitir que os padrões são expressos de forma genérica por $x = [x_{1},...x_{n}]^T$, sobre os quais desejamos inferir sua pertinência em uma dada classe em $Ω =  ${$ω_{1},...,ω_{c}$}. No contexto estatístico, a seguinte regra geral pode ser empregada para tal processo de classificação:

<div align="center">

$\begin{equation}
    (\textbf{x},ω_{j}) \leftrightarrow arg_{ω_{j}\inΩ} max P(ω_{j}|\textbf{x})
\end{equation}$ </div>

em que $P(ω_{j}|\textbf{x})$, denominada probabilidade $\textit{a posteriori}$, representa a probabilidade de $\textbf{x}$ pertencer a $ω_{j}$.

De modo geral, em um problema de classificação, a probabilidade $\textit{a posteriori}$ que compõe a regra expressa pela a equação anterior é desconhecida. No entanto, a Regra de Bayes possibilita o seu cálculo por meio da probabilidade $\textit{a priori}$ $P(ω_{j})$, da evidência $p(\textbf{x})$ e da função de verossimilhança $p(\textbf{x}|ω_{j})$:

<div align="center">

$\begin{equation}
    P(ω_{j}|\textbf{x}) = \frac{p(\textbf{x}|ω_{j})P(ω_{j})}{p(\textbf{x})}
\end{equation}$ 

sendo $p(x) = \sum_{j=1}^{c} p(\textbf{x}|ω_{j})P(ω_{j})$. </div>

Uma vez conhecida $P(ω_{j}|\textbf{x})$, a classificação de $\textbf{x}$ segundo $ω_{j}$, com $j=1,...,c$, torna-se um problema simples.
Com o objetivo de aprofundar as discussões introduzidas, vamos realizar uma análise sobre o erro cometido ao utilizar a Regra de Bayes no processo de classificação. A fim de favorecer o entendimento, considere um problema de classificação entre apenas duas classes $ω_{1}$ e $ω_{2}$ equiprováveis, cujas observações estão definidas sobre o conjunto dos números reais (i.e., $\textbf{X} ≡ \mathbb{R}$), o qual é dividido entre as regiões $R_{1}$ e $R_{2}$. Enquanto a região $R_{1}$ compreende os valores $\textbf{x}$ tais que $P(ω_{1}|\textbf{x})>P(ω_{2}|\textbf{x})$. A Figura 1 ilustra a relação entre as regiões e as probabilidades mencionadas.

<div align="center"> 
    
![figura1](images/figura1.jpg "figura 1") <legend>Figura 1.1 - Regiões de decisão e de erro de classificação.
</legend>
</div>

Segundo essas considerações, podemos expressar a probabilidade do erro de classificação por:

<div align="center"> 

$\begin{equation}
P_{erro} = P(\textbf{x} ∈ R_{2},ω_{1}) + P(\textbf{x} ∈ R_{1},ω_{2})
\end{equation}$ </div>

em que $P(\textbf{x} ∈ R_{2},ω_{1})$ quantifica a probabilidade do padrão $\textbf{x}$ pertencer à região $R_{2}$, apesar da sua classe original ser $ω_{1}$. Partindo da equação anterior, desenvolvemos:

<div align="center">

$\begin{equation}
P_{erro} = P(\textbf{x} ∈ R_{2},ω_{1}) + P(\textbf{x} ∈ R_{1},ω_{2}) = [ \int_{R_{2}} p(\textbf{x}|ω_{1}) \,dx]P(ω_{1}) + [ \int_{R_{1}} p(\textbf{x}|ω_{2}) \,dx]P(ω_{2}) = \frac{1}{2}\int_{R_{2}} p(\textbf{x}|ω_{1}) \,dx + \frac{1}{2}\int_{R_{1}} p(\textbf{x}|ω_{2}) \,dx = \frac{1}{2}[\int_{R_{2}} p(\textbf{x}|ω_{1}) \,dx + \int_{R_{1}} p(\textbf{x}|ω_{2})\,dx]
\end{equation}$ </div>

O desenvolvimento acima mostra acima mostra que o erro se torna mínimo ao garantir que $P(ω_{2}|\textbf{x}) < P(ω_{1}|\textbf{x})$, quando $\textbf{x}\inω_{1}$, e $P(ω_{1}|\textbf{x})< P(ω_{2}|\textbf{x})$, para $\textbf{x}\in ω_{2}$. De fato, ao mover o ponto $\textbf{x}_{0}$, conforme apresentada a Figura 2, verifica-se que a região associada à ocorrência de erro de classificação tem sua área aumentada.

<div align="center">

![figura2](images/figura2.png "figura 2")<legend>Figura 1.2 - Noção de erro dada a alteração sobre as regiões de decisão.
</legend>
</div>

Baseados nas discussões anteriores, voltamos a admitir o espaço de classes $Ω={ω_{1},...,ω_{c}}$, de modo que $\textbf{x}$ está associado a $ω_{i}$ se $P(ω_{i}|\textbf{x}) > P(ω_{j}|\textbf{x})$, para $i \neq j$ e $j=1,...c$. Ainda, a partir dos desenvolvimentos apresentados, é possível associar um risco a cada decisão tomada. Tais casos englobam questões, por exemplo, em que o impacto causado na decisão de $ω_{1}$, em vez de $ω_{2}$, apresenta maior relevância ao decidir sobre $ω_{2}$ como alternativa à $ω_{1}$.

Neste contexto, sendo $R_{i}$ a região do espaço de atributos que induz a classificação em $ω_{i}$. Admitindo $λ_{ki}$ como penalidadde/perda relacionada à escolha equivocada da $ω_{i}$, cuja opção correta seria optar pela classe $ω_{k}$. Baseado neste conceito, o risco associado à classe $ω_{k}$ é dado por:

<div align="center">

$\begin{equation}
\sum_{i=1}^{c} λ_{ki} \int_{R_{i}} p(\textbf{x}|ω_{jk})dx; k=1,...c
\end{equation}$ </div>

A quantidade $\int_{R_{i}} p(\textbf{x}|ω_{jk})dx$ representa a probabilidade do padrão $\textbf{x}$, que, apesar de original da classe $ω_{k}$, ocorre na região $R_{i}$. Ainda, em um ponto de vista geométrico, $r_{k}$ proporciona a "área invadida" por $p(\textbf{x}|ω_{k}$ nas regiões $R_{i}$, com $i=,...c$ e $i \neq k$.

Uma forma de expressar o risco médio de $r$, segundo todas as classes, é tomando a combinação linear expressa pleo risco associado a cada classe e sua propagação de ocorrência:

<div align="center">

$\begin{equation}
r = \sum_{k=1}^{c} r_{k}P(ω_{k}) = \sum_{k=1}^{c} [\sum_{i=1}^{c} λ_{ki} \int_{R_{i}} p(\textbf{x}|ω_{k})dx]P(ω_{k}) = \sum_{k=1}^{c} \int_{R_{i}} [\sum_{i=1}^{c} λ_{ki} p(\textbf{x}|ω_{k}) P(ω_{k})]dx
\end{equation}$

fazendo $\sum_{i=1}^{c} λ_{ki} p(\textbf{x}|ω_{k}) P(ω_{k}) = l_{i}$, temos:

$\begin{equation}
r = \sum_{k=1}^{c} \int_{R_{i}} l_{i} dx
\end{equation}$ </div>

A manipulação algébrica realizada proporciona uma reinterpretação que expressa o risco médio em função das regiões $R_{i}$. Dessa forma, podemos concluir mais uma vez que a inimização do risco $r$ é alcançada ao estabelecer cada região $R_{i}$, com $i=1,...c$, tais que $l_{i}<l_{j}$, para $j=1,...c$ e $j \neq i$.

Vale observar que $l_{i}$ representa o risco em classificar $\textbf{x}$ como $ω_{i}$, enquanto deveria ser $ω_{k}$, para $k=1,...c$. Logo,buscamos não confundir as demais classes com $ω_{i}$.

Mais uma vez, e sem perda de generalidade, vamos admitir um problema binário com $Ω = {ω_{1},ω_{2}}$. Neste caso, temos as probabilidades $λ_{11},λ_{21},λ_{12}$ e $λ_{22}$ e os riscos:

<div align="center"> 

$\begin{equation}
l_{1} = λ_{11}p(\textbf{x}|ω_{1})P(ω_{1}) + λ_{21}p(\textbf{x}|ω_{2})P(ω_{2})
\end{equation}$

$\begin{equation}
l_{2} = λ_{12}p(\textbf{x}|ω_{1})P(ω_{1}) + λ_{22}p(\textbf{x}|ω_{2})P(ω_{2})
\end{equation}$ </div>

Optando pela classe $ω_{1}$ desde que $l_{1} < l_{2}$, é estabelecida a seguinte razão de verossimilhança:

<div align="center"> 

$\begin{equation}
l_{2} = \frac{p(\textbf{x}|ω_{1})}{p(\textbf{x}|ω_{2})} > \frac {P(ω_{2})λ_{21}-λ_{22}}{P(ω_{2})λ_{12}-λ_{11}}
\end{equation}$ </div>

De modo análogo, a razão $l_{21}$ é obtida partindo da condição $l_{2} < l_{1}$. Em tempo, simplificando a razão obtida ao caso em que as classes são equiprováveis (i.e., $P(ω_{1})=P(ω_{2})=\frac{1}{2}$) e assumindo que não há penalidade ao optar por $ω_{i}$ quando esta é a classe esperada (i.e., $λ_{ij}=0$ se $i=j$), podemos traçar as seguintes regras de decisão:

<div align="center"> 

$\begin{equation}
(\textbf{x},ω_{1}) \Leftrightarrow  p(\textbf{x}|ω_{1}) > p(\textbf{x}|ω_{2}) \frac{λ_{21}}{λ_{12}}
\end{equation}$

$\begin{equation}
(\textbf{x},ω_{2}) \Leftrightarrow  p(\textbf{x}|ω_{1}) > p(\textbf{x}|ω_{1}) \frac{λ_{12}}{λ_{21}}
\end{equation}$ </div>

Cabe notar que, ao admitir $λ_{12} = λ_{21}$, as regras desenvolvidas recaem no caso de minimização do erro de classificação, abordado anteriormente. Por outro lado, para $λ_{21} > λ_{12}$, temos como efeito colateral uma maior tendência sobre a escolha de $ω_{2}$ em comparação a $ω_{1}$. Naturalmente, ao passo que a diferença $λ_{21} - λ_{12}$ aumenta, maior é a tendenciosidade revelada.




