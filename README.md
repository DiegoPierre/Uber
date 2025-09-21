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
