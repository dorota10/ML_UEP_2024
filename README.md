### Autor: Dorota Woźna

# Cel zadania:
Celem zadania było oczyszczenie danych i znalezienie klasyfikatora, który skutecznie będzie przewidywał oszustwa w transakcjach.
Największe znaczenie w macierzy pomyłek będzie miał FN (False Negative), ponieważ chcemy minimalizować przypadki, gdy oszustwo nastąpiło, a nie zostało wychwycone.

# Opis rozwiązania:
Braki w danych numerycznych uzupełniono metodą KNN. Przeprowadzono dla nich standaryzację.
Ze względu na duże braki w danych tekstowych zrezygnowano z One Hot Encodingu. Dodano nowe zmienne, które pomagają ocenić, jak wysokie jest prawdopodobieństwo, że gdy występuje dane słowo, to mamy do czynienia z oszustwem.
Nastepnie użyto następujących klasyfikatorów:

- RandomForestClassifier(n_estimators= 100, min_samples_split= 5, min_samples_leaf= 1),
- xgb.XGBClassifier(),
- KNeighborsClassifier(n_neighbors=5),
- KNeighborsClassifier(n_neighbors=10),
- LogisticRegression(),
- LogisticRegression(solver='lbfgs', class_weight=weights),
- SVC()

Najlepszy okazał się model XGBoost.
W dalszej części przeprowadzono częściowe zbalansowanie próbki (najpierw metodą SMOTE, następnie RandomUnderSampling). Sprawdzono, czy wyniki klasyfikatora XGBoost będą lepsze, gdy zostaną wyuczone na nowym zbiorze.

# Wyniki
Ostatecznie najlepszy okazał się model XGBoost po resamplingu. Na danych testowych otrzymano czułość (recall) na poziomie: 0,95, co wynikało z 22 niewykrytych przestępstw.
