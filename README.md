# 🚗 Analyse des trajets Uber 2024

##  Contexte et problématique
- Uber souhaite **réduire les annulations de trajets** et **optimiser les revenus**.  
- Les annulations entraînent des pertes financières et impactent la satisfaction client.  
- Objectif : utiliser les données de 148 770 réservations Uber pour **prédire les annulations** et identifier les facteurs clés influençant les revenus.

---

## Parties prenantes
- **Gestionnaires opérationnels** : optimiser la flotte et réduire les pertes.  
- **Équipes marketing et satisfaction client** : améliorer l’expérience utilisateur.  
- **Data scientists** : construire des modèles prédictifs et interprétables.

---

##  Données utilisées
- 148 770 réservations Uber pour 2024.  
- Informations disponibles :
  - Type de véhicule
  - Localisation de prise en charge et de dépose
  - Durée et tarif du trajet
  - Statut du trajet : complété, annulé, incomplet
  - Notes et évaluations clients et chauffeurs
- Objectif : identifier les motifs d’annulation et les facteurs influençant les revenus.

---

##  Méthodologie
1. **Préparation des données**
   - Nettoyage : suppression des doublons et valeurs manquantes  
   - Transformation : extraction de l’heure, du jour, création de variables weekend  
   - Encodage des variables catégorielles et mise à l’échelle des variables numériques
2. **Modélisation**
   - **Classification** : prédire les annulations  
   - Modèles testés : KNN, Random Forest  
   - Hyperparamètres optimisés pour de meilleures performances
3. **Évaluation**
   - Séparation des données en jeu d’entraînement et test
   - Métriques : Accuracy, F1-score, précision et rappel  
   - Visualisation : matrice de confusion et importance des variables

---

## 5️⃣ Résultats clés
- **Meilleur modèle** : Random Forest optimisé  
- Les variables les plus influentes sur les annulations :
  - Notes clients et chauffeurs  
  - Distance du trajet  
  - Valeur de la réservation  
- Le modèle prédit efficacement les trajets susceptibles d’être annulés.

---

## Modèle K-Nearest Neighbors (KNN)

Nous allons entraîner un modèle KNN pour prédire les annulations et évaluer sa performance.
```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, ConfusionMatrixDisplay

# Initialisation du modèle KNN
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train, y_train)

# Prédictions
y_pred_knn = knn.predict(X_test)

# Évaluation
acc_knn = accuracy_score(y_test, y_pred_knn)
print("Accuracy KNN :", acc_knn)

# Matrice de confusion
ConfusionMatrixDisplay.from_predictions(y_test, y_pred_knn)
```
<img src="Screenshot 2025-09-21 163453.png" width="400" style="display: block; margin: 0 auto;">
<p style='text-align: center; font-style: italic; color: #7f8c8d;'>
</p>

##  Modèle Random Forest

Nous allons entraîner un modèle Random Forest pour prédire les annulations et comparer la performance avec KNN.
```python
from sklearn.ensemble import RandomForestClassifier

# Initialisation du modèle Random Forest
rf = RandomForestClassifier(n_estimators=200, max_depth=10, random_state=42)
rf.fit(X_train, y_train)

# Prédictions
y_pred_rf = rf.predict(X_test)

# Évaluation
acc_rf = accuracy_score(y_test, y_pred_rf)
print("Accuracy Random Forest :", acc_rf)

# Matrice de confusion
ConfusionMatrixDisplay.from_predictions(y_test, y_pred_rf)

```
<img src="Screenshot 2025-09-21 163554.png" width="400" style="display: block; margin: 0 auto;">
<p style='text-align: center; font-style: italic; color: #7f8c8d;'>
</p>
##  Évaluation des modèles

Nous allons évaluer les modèles KNN et Random Forest avec plusieurs métriques pour mieux comprendre leur performance sur la classification des annulations.


```python
from sklearn.metrics import precision_score, recall_score, f1_score, classification_report

# --- KNN ---
print(" KNN :")
print("Accuracy :", accuracy_score(y_test, y_pred_knn))
print("Precision :", precision_score(y_test, y_pred_knn))
print("Recall :", recall_score(y_test, y_pred_knn))
print("F1-score :", f1_score(y_test, y_pred_knn))
print("\nClassification report :\n", classification_report(y_test, y_pred_knn))

# --- Random Forest ---
print(" Random Forest :")
print("Accuracy :", accuracy_score(y_test, y_pred_rf))
print("Precision :", precision_score(y_test, y_pred_rf))
print("Recall :", recall_score(y_test, y_pred_rf))
print("F1-score :", f1_score(y_test, y_pred_rf))
print("\nClassification report :\n", classification_report(y_test, y_pred_rf))
```
<img src="Screenshot 2025-09-21 163624.png" width="400" style="display: block; margin: 0 auto;">
<p style='text-align: center; font-style: italic; color: #7f8c8d;'>
</p>

##  Optimisation des hyperparamètres : Random Forest

Nous allons utiliser GridSearchCV pour trouver les meilleurs hyperparamètres du modèle Random Forest et améliorer sa performance sur la classification des annulations.
```python
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.metrics import ConfusionMatrixDisplay, classification_report

# =========================
# 1️⃣ Matrice de confusion
# =========================
disp = ConfusionMatrixDisplay.from_estimator(
    best_rf, X_test, y_test, 
    cmap="Blues", 
    xticks_rotation=45
)
plt.title("Matrice de confusion - Random Forest")
plt.show()
```
<img src="Screenshot 2025-09-21 163649.png" width="400" style="display: block; margin: 0 auto;">
<p style='text-align: center; font-style: italic; color: #7f8c8d;'>
</p>

```python
plt.figure(figsize=(10,6))
sns.barplot(x=importances, y=features, color="skyblue")  # couleur unique
plt.title("Importance des variables - Random Forest")
plt.xlabel("Importance")
plt.ylabel("Variables")
plt.show()
```
<img src="Screenshot 2025-09-21 163726.png" width="400" style="display: block; margin: 0 auto;">
<p style='text-align: center; font-style: italic; color: #7f8c8d;'>
</p>

##  Limites du projet
- Déséquilibre des classes : la majorité des trajets sont complétés.  
- Certaines informations manquantes : raisons d’annulation, facteurs externes.  
- Le modèle reste en partie une **boîte noire**, même si l’importance des variables est informative.  

---

##  Recommandations pour Uber
1. **Réduire les annulations**
   - Prédire le risque d’annulation au moment de la réservation  
   - Proposer des alternatives pour les trajets à risque élevé
2. **Optimiser la flotte**
   - Redistribuer les chauffeurs selon la demande prévue  
   - Réduire les temps d’attente
3. **Améliorer l’expérience client**
   - Offrir des incitations ciblées pour les clients susceptibles d’annuler  
   - Surveiller la qualité des chauffeurs
4. **Analyses futures**
   - Intégrer météo, trafic et événements locaux  
   - Tester des modèles plus avancés et un système de recommandation

---

##  Conclusion
- L’utilisation des données et du **modèle prédictif Random Forest** permet à Uber de :  
  - Réduire les annulations  
  - Optimiser les revenus par trajet  
  - Améliorer la satisfaction des clients  
- Prochaine étape : **déploiement en production et suivi des performances** pour ajuster le modèle en continu.

Email:septamalouison634@gmail.com
  
