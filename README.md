# 11° COMPETIÇÃO DE MACHINE LEARNING FLAI

## Resultado da minha submissão
Esta é minha primeira submissão em uma compatição de ML da Flai. E com muita felicidade e esforço, fiquei em 4° lugar no Ranking geral. Em que meu modelo obteve um F1-Score de 0.79602 na métrica parcial (testando em apenas um terço do conjunto de teste), melhorando a métrica para 0.84109 na métrica total (validando em todo conjunto teste).

<div align="center">
  
![Ranking geral - métricas](https://github.com/EvelyneBomfim/Challenge-Aprovacao_de_emprestimo/assets/89544488/141919c7-9c9a-400d-8db6-a6a22b13703b)
  
</div>

## Descrição do problema 
O departamento de crédito de um banco deseja automatizar o processo de tomada de decisão para a aprovação de empréstimos fiduciários. Sua missão é avaliar um conjunto de dados sobre o tomador do empréstimo e decidir se um novo empréstimo poderá ser feito.

## Ferramentas
- Utilizado a linguagem Python sendo executado no Google Colab.
- As principais bibliotecas utilizadas foram: pandas, numpy, seaborn, matplotlib, imblearn e sklearn.

## O que foi feito

### Análise
Etapa de conhecer os dados, entende-los e ajusta-los.

Analisando o conjunto de dados no arquivo treino.csv, verifiquei que seria necessário realizar alguns ajustes:
- Transformando as colunas para os tipos corretos (string, inteiro ou float).
- Padronizando as colunas referentes a tempo, passando todas para o mesmo período (anos ou meses em média anual).
- Exclusão de dados outliers.

### Normalização
Realizado a normalizaçãodos dados para melhor entendimento do modelo machine learning. Usando [MinMaxScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html) (variáveis numéricas) e Pandas get_dummies (variáveis categóricas).

### Dados faltantes (missing)
Por haver muitos dados faltantes, não seria possível excluir essas linhas, pois geraria um impacto direto na aprendizagem do modelo. Então utilizei o [KNNImputer](https://scikit-learn.org/stable/modules/generated/sklearn.impute.KNNImputer.html) para predizer esses dados.

### Balanceamento
Para não haver uma performance enganosa, foi realizado o balanceamento dos dados utilizando a biblioteca [Imbalanced Learn](https://imbalanced-learn.org/stable/user_guide.html#user-guide). Comparando as métricas obtidas nos modelos (tanto over-sampling quanto under-sampling), foi escolhido o [ADASYN](https://imbalanced-learn.org/stable/references/generated/imblearn.over_sampling.ADASYN.html#imblearn.over_sampling.ADASYN).

### Machine learning
Criei uma função para comparar as métricas obtidas em diferentes modelos machine learning. Os modelos [RandomForestClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html) e [KNeighborsClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html) apresentaram métricas melhores e bem parecidas. Plotando as predições para verificar quais obtiveram melhor aprendizado.

Fiz algumas análises verificando as variáveis que tinham maior importância no treinamento, mas não fez diferença ou baixava muito a métrica obtida anteriormente.

Para tunagem, usei o [GridSearch](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html) para buscar os melhores parâmetros. Tanto pro RandomForestClassifier quanto KNeighborsClassifier.

Por fim, o KNeighborsClassifier ganhou com um **F1-Score de 0.97**. :tada:
