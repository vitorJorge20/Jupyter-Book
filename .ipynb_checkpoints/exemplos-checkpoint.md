<style>
    h2 {
        font-size: 24px;
    }
    legend {
        font-size: 16px;
    }
    main {
        text-align: justify;
    }
</style>

# Capítulo 5: Exemplos

Este capítulo contém alguns exemplos de códigos que utilizam os algoritmos discutidos nos capítulos anteriores. Os exemplos são desenvolvidos em python utilizando, principalmente, a biblioteca Scikit Learn.

## Principais Importações

```
from sklearn.svm import SVC
import numpy as np
import matplotlib.pyplot as plt
from sklearn import svm, datasets
from sklearn.inspection import DecisionBoundaryDisplay
from sklearn.tree import DecisionTreeClassifier
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.neural_network import MLPClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.svm import SVC
from sklearn.decomposition import PCA
from sklearn.ensemble import RandomForestClassifier as RF
from sklearn.metrics import ConfusionMatrixDisplay
from sklearn.ensemble import GradientBoostingClassifier
from sklearn.ensemble import StackingClassifier
```

## Exemplo 1 - Plotagem da superfície de decisão e vetores de suporte do classificador SVM

```
from sklearn.datasets import make_moons
from sklearn.datasets import make_blobs
# we create 40 separable points

#Cria uma base de dados para classificação binária usando padrões linearmente separáveis
X, Y = make_blobs(n_samples=40, centers=2, random_state=0)

#Cria uma base de dados para classificação binária usando padrões não linearmente separáveis
#X,Y = make_moons(n_samples=40, noise=0.1, random_state=0)

# Ajuste do classificador SVM

clf = SVC(kernel="linear", C=1000)

clf.fit(X, Y)

plt.scatter(X[:, 0], X[:, 1], c=Y, s=30, cmap=plt.cm.Paired)

# Plotagem da superfície de decisão
ax = plt.gca()
DecisionBoundaryDisplay.from_estimator(
    clf,
    X,
    plot_method="contour",
    colors="k",
    levels=[-1, 0, 1],
    alpha=0.5,
    linestyles=["--", "-", "--"],
    ax=ax,
)
# Plotagem dos vetores de suporte
ax.scatter(
    clf.support_vectors_[:, 0],
    clf.support_vectors_[:, 1],
    s=100,
    linewidth=1,
    facecolors="none",
    edgecolors="k",
)
plt.show()
```

## Exemplo 2 - Aplicação do classificador de árvore de decisão ao dataset Iris e plotagem das superfícies de decisão

```
from sklearn.datasets import load_iris

iris = load_iris()

import matplotlib.pyplot as plt
import numpy as np

from sklearn.datasets import load_iris
from sklearn.inspection import DecisionBoundaryDisplay
from sklearn.tree import DecisionTreeClassifier

# Parâmetros
n_classes = 3
plot_colors = "ryb"
plot_step = 0.02


for pairidx, pair in enumerate([[0, 1], [0, 2], [0, 3], [1, 2], [1, 3], [2, 3]]):
    # Selecionando os atributos aos pares
    X = iris.data[:, pair]
    y = iris.target

    # Treino
    clf = DecisionTreeClassifier(criterion='entropy',min_samples_split=2,min_impurity_decrease=10**(-7)).fit(X, y)

    # Plotagem da superfície de decisão
    ax = plt.subplot(2, 3, pairidx + 1)
    plt.tight_layout(h_pad=0.5, w_pad=0.5, pad=2.5)
    DecisionBoundaryDisplay.from_estimator(
        clf,
        X,
        cmap=plt.cm.RdYlBu,
        response_method="predict",
        ax=ax,
        xlabel=iris.feature_names[pair[0]],
        ylabel=iris.feature_names[pair[1]],
    )

    # Plotagem dos pontos de treinamento
    for i, color in zip(range(n_classes), plot_colors):
        idx = np.where(y == i)
        plt.scatter(
            X[idx, 0],
            X[idx, 1],
            c=color,
            label=iris.target_names[i],
            cmap=plt.cm.RdYlBu,
            edgecolor="black",
            s=15,
        )

plt.suptitle("Superfície de decisão de árvores de decisão treinadas em pares de atributos")
plt.legend(loc="lower right", borderpad=0, handletextpad=0)
_ = plt.axis("tight")
```

## Exemplo 3 - Diferentes classificadores aplicados à base de dados Iris.

```
#Carregando e separando os dados de treino e validação

X = iris.data
y = iris.target

X_train,X_test,Y_train,Y_test = train_test_split(X,y,test_size = 0.33,random_state=42)

#Classificadores:

#LDA:

LDA = LinearDiscriminantAnalysis()
LDA.fit(X_train,Y_train)
yp = LDA.predict(X_test)
ConfusionMatrixDisplay.from_estimator(LDA, X_test, Y_test)
acc_lda = round(np.mean(yp == Y_test)*100,2)
print(acc_lda)

#Decision tree:

dt = DecisionTreeClassifier(criterion="entropy", max_depth=200)
dt.fit(X_train, Y_train)
dty = dt.predict(X_test)
ConfusionMatrixDisplay.from_estimator(dt, X_test, Y_test)
acc_dt = round(np.mean(dty == Y_test)*100,2)

#MLP:

mlp = MLPClassifier(hidden_layer_sizes=(2,2), max_iter=200, activation='logistic', verbose=False) #, random_state=42)
mlp.out_activation = 'softmax' # 'logistic', 'softmax', # mlp.outputs = 3
mlp.fit(X_train, Y_train)
ConfusionMatrixDisplay.from_estimator(mlp, X_test, Y_test)
mlpy = mlp.predict(X_test)
acc_mlp = round(np.mean(mlpy == Y_test)*100,2)
print(acc_mlp)

#SVM:

svm = SVC(kernel='rbf', C=0.01, probability=True)
svm.fit(X_train, Y_train)
ConfusionMatrixDisplay.from_estimator(svm, X_test, Y_test)
svmy = svm.predict(X_test)
acc_svm = round(np.mean(svmy == Y_test)*100,2)
print(acc_svm)
```

## Exemplo 4 - Métodos de combinação de classificadores Floresta Aleatória e Gradient Boost aplicados à base de dados Iris.

```
#Carregando e separando os dados de treino e validação

X = iris.data
y = iris.target

X_train,X_test,Y_train,Y_test = train_test_split(X,y,test_size = 0.33,random_state=42)

#Random Forest

combClass = RF(n_estimators=100,criterion = 'entropy',min_samples_split = 10,min_impurity_decrease = 10**(-5))
combClass.fit(X_train, Y_train)
RFt = combClass.predict(X_test)
ConfusionMatrixDisplay.from_estimator(combClass, X_test, Y_test)
acc_rf = round(np.mean(RFt == Y_test)*100,2)
print(acc_rf)

#Gradient Boosting

gboost = GradientBoostingClassifier(n_estimators=100, learning_rate=1.0,
    max_depth=1, random_state=0).fit(X_train, Y_train)
gboost.score(X_test, Y_test)
ConfusionMatrixDisplay.from_estimator(gboost, X_test, Y_test)

```