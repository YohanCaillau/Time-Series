# Time Series

## Partie 1: Introduction aux séries temporelles

## Qu'est-ce qu'une série temporelle ?

* Quelles sont les particularités des séries temporelles ?

## Caractériser une série temporelle
* Tracer les séries choisies
* Les qualifier en termes de moyenne, tendance, saisonnalité, cycle
* Qu'est-ce que la stationnarité ?
* Appliquer le test de Dickey-Fuller à une série temporelle visiblement non stationnaire
* Rendre la série stationnaire (comment ?)
* Ré-appliquer le test à la série stationnarisée
* Prendre un exemple de série avec cycle et appliquer une méthode de désaisonnalisation

## Etude de la série temporelle

* Décomposition d'une série temporelle :
[ici](https://machinelearningmastery.com/decompose-time-series-data-trend-seasonality/)
et [là](https://anomaly.io/seasonal-trend-decomposition-in-r/index.html) et [ici](https://machinelearningmastery.com/time-series-trends-in-python/)

* Stationnarité et test de Dickey-Fuller augmenté :
[ici](https://fr.wikipedia.org/wiki/Stationnarit%C3%A9_d%27une_s%C3%A9rie_temporelle)
[ici](https://towardsdatascience.com/stationarity-in-time-series-analysis-90c94f27322)
et [là](https://machinelearningmastery.com/time-series-data-stationary-python/)
et [ici](https://nwfsc-timeseries.github.io/atsa-labs/sec-boxjenkins-aug-dickey-fuller.html)

* Désaisonnalisation : [ici](https://machinelearningmastery.com/time-series-seasonality-with-python/)

* FFT : [ici](https://www.ritchievink.com/blog/2017/04/23/understanding-the-fourier-transform-by-example/)

* Un bon notebook Kaggle utilisant la librairie statsmodel : [ici](https://www.kaggle.com/harryren/boston-arima-forecast-and-analysis)

* Un cours complet sur les séries temporelles avec des exemples en python : [ici](https://www.tutorialspoint.com/time_series/index.htm)

## Les techniques classiques de prédiction

* Les baselines les plus simples ?
* Modèles AR, MA, ARMA, ARIMA
	* Equations ?
	* Paramètres ?
	* Ordres ?

## Auto-corrélation

* Avec les séries temporelles déjà choisies, tracer l'ACF
* Avec les séries temporelles déjà choisies, tracer la PACF
* En déduire le modèle ARIMA adapté
* Implémenter le modèle ARIMA correspondant, changer ses ordres et observer

## Evaluation de la qualité des modèles

* Qu'est-ce que le backtest ?
* Walk-forward validation

## Partie 2: Modèles ARMA, ARIMA
Suite de l'introduction aux séries temporelles

### Revoir rapidement la décomposition de séries temporelles [ici](https://www.youtube.com/watch?v=0ar9extHObg)

### BigML Time Series
 * Regarder la vidéo sur les séries temporelles dans BigML ([vidéo](https://www.youtube.com/watch?v=wsyiOHUBE8c&list=PL1bKyu9GtNYHAk0PUojkLYZzASoYVcsTQ&index=10))
 * Appliquer le workflow BigML au dataset cité dans la vidéo (dataset disponible [ici](https://github.com/plotly/datasets/blob/master/monthly-milk-production-pounds.csv), suivre les étapes de la vidéo
 * Appliquer le même workflow BigML au dataset sunspot.csv (disponible sur Kaggle, github, etc.) avec l'outil Time Series : à quoi vous attendez-vous ? Que constatez-vous ?
 * Choisir une série temporelle dans une des bases ci-après et appliquer le même workflow dans BigML avec l'outil Time Series 

## Modèles auto-régressif
 * De même, dans une série temporelle, un modèle auto-régressif est une régression linéaire d'une variable sur ses valeurs passées
 * Une vidéo sur ces modèles [ici](https://www.youtube.com/watch?v=Mc6sBAUdDP4)
 * Pour illustrer le modèle AR, implémenter le notebook :
https://machinelearningmastery.com/autoregression-models-time-series-forecasting-python/

### Auto-corrélation
 * Un modèle auto-régressif fait appel à la notion d'auto-corrélation, c'est-à-dire à la corrélation entre des valeurs d'une série temporelle séparées par un intervalle de temps constant. Par exemple, la température moyenne aujourd'hui à un endroit donné est fortement corrélée avec la température au même endroit la veille et moins corrélée avec la température 3 mois avant.
 * Implémenter le notebook :
https://machinelearningmastery.com/gentle-introduction-autocorrelation-partial-autocorrelation/

*Note :* La première partie de ce canevas reprend les grandes étapes classiques d'une analyse de séries temporelles :
1. Observer la série
2. Nettoyer les données si nécessaire
3. Transformer la série en série stationnaire en enlevant sa moyenne, sa tendance, ses éléments saisonniers
4. Vérififer que le résultat de 3 est stationnaire par une méthode empirique ou un test statistique (ex. : Augmented Dickey-Fuller)
5. Etudier l'auto-corrélation en traçant l'ACF et la PACF enfin de fixer les ordres p et q d'un modèle ARMA ou ARIMA
6. Splitter les données
7. Fitter le modèle, tester des variantes du modèle autour des valeurs p et q trouvées en 5, les classer suivant une métrique
8. Evaluer le(s) modèle(s) avec des fenêtres glissantes training/test
9. Evaluer aussi la performance du modèle après avoir inversé les opérations de l'étape 3
10. Pour la production, suivre à intervalles réguliers la performance du modèle, ré-entraîner en cas de divergence avérée

*Note :* Pour le choix des ordres p et q pour les parties AR et MA du modèle,
on prend p tel que :
  * La PACF passe sous les intervalles de confiance à partir de p+1
* On prend q pour la partie MA tel que :
  * l'ACF passe sous les intervalles de confiance à partir de q+1
* Si l'ACF décroit régulièrement de façon exponentielle sans pic, le modèle sera un AR pur, q = 0
* Si le le PACF décroit régulièrement de façon exponentielle sans pic, le modèle sera un MA pur, p = 0

Voir une discussion plus détaillée (et nuancée), en français, [ici](https://didierdelignieresblog.files.wordpress.com/2019/09/arimacomplet.pdf=

## Exercice ACF/PACF
* Générer plusieurs séries temporelles simples (+1 -1, sinus, droites, etc.)
* Générer un signal AR, un signal MA, un signal ARMA
* Plotter les ACF/PACF correspondantes
 
## Partie 3: Modèle de Machine Learning
Avec le modèle persistant naïf et ARMA, nous avons une baseline comme référence pour des modèles plus sophistiqués...
Suite de l'introduction aux séries temporelles avec les techniques "modernes" venant du Machine Learning :
  * RNN/LSTM/GRU
  * Convolution 1D
  * Méthodes ensemblistes du style Random Forest/XGBoost
  * Modèles dit avec "attention" venant des problèmes seq2seq du NLP (transformers) 
  
 Rappel : le théorème No Free Lunch indique qu'aucun modèle n'est universellement le meilleur, d'où l'intérêt d'essayer diverses approches sur les mêmes données.

## Atelier
  * Partie 1
    * Produire une série suivant un sinus
    * Entraîner et évaluer un RNN simple sur cette série
    * Varier la méthode d'évaluation (par exemple Walk-forward à fenêtre fixe ou à fenêtre croissante)
    * Ajouter différents niveaux de bruit et re-tester le modèle précédent
    * Ré-entraîner, tester
    * Refaire ce qui précède avec un LSTM et comparer
    * Refaire ce qui précède avec un GRU et comparer
  * Partie 2
    * Tout refaire avec la série choisie la semaine précédente (éventuellement prendre une série plus longue pour les LSTM/GRU si moins de 1000 exemples. Les données de consommation électrique sont une bon matériau)
    * Tout refaire avec une méthode ensembliste et comparer
    * Tout refaire avec une conv-1D et comparer
    * BONUS : remplacer le LSTM par un modèle à attention

## Méthodes plus avancées
* Modèles à  seq2seq https://jeddy92.github.io/JEddy92.github.io/ts_seq2seq_intro/
* La FFT dans Python et son usage  (si pas le temps, se reporter [ici](https://www.ritchievink.com/blog/2017/04/23/understanding-the-fourier-transform-by-example/))

# Ressources
  
* Décomposition d'une série temporelle :
[ici](https://machinelearningmastery.com/decompose-time-series-data-trend-seasonality/)
et [là](https://anomaly.io/seasonal-trend-decomposition-in-r/index.html) et [ici](https://machinelearningmastery.com/time-series-trends-in-python/)

* Stationnarité et test de Dickey-Fuller augmenté :
[ici](https://fr.wikipedia.org/wiki/Stationnarit%C3%A9_d%27une_s%C3%A9rie_temporelle)
[ici](https://towardsdatascience.com/stationarity-in-time-series-analysis-90c94f27322)
et [là](https://machinelearningmastery.com/time-series-data-stationary-python/)
et [ici](https://nwfsc-timeseries.github.io/atsa-labs/sec-boxjenkins-aug-dickey-fuller.html)

* Désaisonnalisation : [ici](https://machinelearningmastery.com/time-series-seasonality-with-python/)

* FFT : [ici](https://www.ritchievink.com/blog/2017/04/23/understanding-the-fourier-transform-by-example/)

* Un bon notebook Kaggle utilisant la librairie statsmodel : [ici](https://www.kaggle.com/harryren/boston-arima-forecast-and-analysis)

* Un cours complet sur les séries temporelles avec des exemples en python : [ici](https://www.tutorialspoint.com/time_series/index.htm)

* Un exemple très complet sur la sélection des ordres d'un modèle ARMA, en français ! [ici](https://www.ceremade.dauphine.fr/~roche/Enseignement/Series_temps_exMaster/TP2_SeriesTemp.html)

* Librairie statsmodels [ici](https://www.statsmodels.org/stable/index.html)

* Méthodes de prédictions classiques : [ici](https://machinelearningmastery.com/simple-time-series-forecasting-models/) et [là](https://machinelearningmastery.com/time-series-forecasting-methods-in-python-cheat-sheet/) et [là](https://www.kaggle.com/thebrownviking20/everything-you-can-do-with-a-time-series) et [là](https://towardsdatascience.com/time-series-in-python-exponential-smoothing-and-arima-processes-2c67f2a52788)

* ACF/PACF : [ici](https://machinelearningmastery.com/gentle-introduction-autocorrelation-partial-autocorrelation/) et [là](https://towardsdatascience.com/significance-of-acf-and-pacf-plots-in-time-series-analysis-2fa11a5d10a8)

* ARIMA : [ici](https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python/), [là](http://people.duke.edu/%7Ernau/Notes_on_nonseasonal_ARIMA_models--Robert_Nau.pdf) et [là](https://people.duke.edu/~rnau/411arim2.htm)

* Validation de modèles de prédiction : [ici](https://machinelearningmastery.com/backtest-machine-learning-models-time-series-forecasting/) et [là](https://blog.insightdatascience.com/whats-wrong-with-my-time-series-model-validation-without-a-hold-out-set-94151d38cf5b)

* Des modèles plus exotiques : ARCH, GARCH [voir](https://en.wikipedia.org/wiki/Autoregressive_conditional_heteroskedasticity)

* Un exemple d'analyse de série temporelle : [ici](https://towardsdatascience.com/almost-everything-you-need-to-know-about-time-series-860241bdc578)

* Vidéo d'ouverture sur d'autres méthodes, l'exemple d'Uber : [ici](https://youtu.be/VYpAodcdFfA)

* Un livre entier sur les méthodes de prédiction : [ici](https://otexts.com/fpp2/)

* Grid search sur les time series https://machinelearningmastery.com/how-to-grid-search-deep-learning-models-for-time-series-forecasting/

* Un exemple de notebook avec un modèle ARIMA https://github.com/JTreguer/arima_example

## BigML
Les séries temporelles dans BigML ([vidéo](https://www.youtube.com/watch?v=wsyiOHUBE8c&list=PL1bKyu9GtNYHAk0PUojkLYZzASoYVcsTQ&index=10))
(et [ici](https://bigml.com/whatsnew/timeseries) pour les fonctionnalités principales)

## Datasets
 * 7 datasets collectés dans un article de Jason Brownlee : [ici](https://machinelearningmastery.com/time-series-datasets-for-machine-learning/)
 * 41 séries temporelles : [ici](https://data.world/datasets/time-series)
 * 102 datasets de l'UCI :[ici](https://archive.ics.uci.edu/ml/datasets.php?format=&task=&att=&area=&numAtt=&numIns=&type=ts&sort=taskUp&view=table)
 
## Séries multivariées
https://www.analyticsvidhya.com/blog/2018/09/multivariate-time-series-guide-forecasting-modeling-python-codes/

* RNN simple sur un sinus avec Keras : [ici](https://fairyonice.github.io/Understand-Keras%27s-RNN-behind-the-scenes-with-a-sin-wave-example.html)
* RNN simple sur un sinus avec TensorFlow : [ici](https://medium.com/@jkim2718/time-series-prediction-using-rnn-in-tensorflow-738e2dcfca96)
* Notebook de Guillaume [ici](https://github.com/guitoo/TimeSeries)

* Des explications sur les LSTM : [ici](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)

* LSTM sur un sinus : 
[ici](https://medium.com/@krzysztofbalka/training-keras-lstm-to-generate-sine-function-2e3c0ca42c3b)
[Une discussion à lire](https://datascience.stackexchange.com/questions/31923/training-an-lstm-to-track-sine-waves)

* LSTM sur série univarié [ici](https://machinelearningmastery.com/time-series-forecasting-long-short-term-memory-network-python/)

* Deep learning sur série univarié : [ici](https://machinelearningmastery.com/how-to-develop-deep-learning-models-for-univariate-time-series-forecasting/)

* Un diagramme très complet sur la forme des entrée pour un LSTM dans Keras : https://github.com/MohammadFneish7/Keras_LSTM_Diagram

* Une analyse de série temporelle très complète d'un point de vue statistique sur un cas réel avec LSTM : [ici](https://towardsdatascience.com/time-series-analysis-visualization-forecasting-with-lstm-77a905180eba)
Avec le [notebook](https://github.com/susanli2016/Machine-Learning-with-Python/blob/master/LSTM%20Time%20Series%20Power%20Consumption.ipynb)
Tiré de [ça](https://machinelearningmastery.com/multivariate-time-series-forecasting-lstms-keras/)

* ARIMA vs LSTM (vs Prophet): [ici](https://medium.com/@cdabakoglu/time-series-forecasting-arima-lstm-prophet-with-python-e73a750a9887)

* Time series generator dans Keras : [ici](https://machinelearningmastery.com/how-to-use-the-timeseriesgenerator-for-time-series-forecasting-in-keras/) [et là](https://www.dlology.com/blog/how-to-use-keras-timeseriesgenerator-for-time-series-data/)

* Changer la fréquence d'une série temporelle avec Pandas :
http://benalexkeen.com/resampling-time-series-data-with-pandas/

* LSTM et Time Series avec PyTorch : [ici](https://www.jessicayung.com/lstms-for-time-series-in-pytorch/)
[là](https://stackabuse.com/time-series-prediction-using-lstm-with-pytorch-in-python/)

* Tuto PyTorch : [ici](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html)
[ici aussi](https://www.analyticsvidhya.com/blog/2019/09/introduction-to-pytorch-from-scratch/)

* Utiliser la convolution 1D pour les séries temporelles : [ici](https://machinelearningmastery.com/how-to-develop-convolutional-neural-networks-for-multi-step-time-series-forecasting/)
[,ici](https://towardsdatascience.com/how-to-use-convolutional-neural-networks-for-time-series-classification-56b1b0a07a57)
[,ici](https://jeddy92.github.io/JEddy92.github.io/ts_seq2seq_conv/)
[et là](https://fr.slideshare.net/PyData/1d-convolutional-neural-networks-for-time-series-modeling-nathan-janos-jeff-roach)

* XGBoost pour les séries temporelles : [ici](https://towardsdatascience.com/using-gradient-boosting-for-time-series-prediction-tasks-600fac66a5fc)

* Un notebook Kaggle qui utilise XGBoost pour de la prédiction de séries temporelles : [ici](https://www.kaggle.com/furiousx7/xgboost-time-series)

* Une étude comparative sur github entre ARIMA, XGBOOST et RNN: [ici](https://github.com/Jenniferz28/Time-Series-ARIMA-XGBOOST-RNN)

* Les architectures au-delà des LSTM : [ici](https://towardsdatascience.com/the-fall-of-rnn-lstm-2d1594c74ce0)
[ici aussi](https://towardsdatascience.com/attn-illustrated-attention-5ec4ad276ee3)
[là tiens](https://medium.com/@adityathiruvengadam/transformer-architecture-attention-is-all-you-need-aeccd9f50d09)
