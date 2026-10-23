# Prévision électrique par LSTM — notebook complet en français

Prévision des 24 prochaines heures à partir de 168 heures d'historique, sur le client UCI MT_001. Entraînement 2012, sélection 2013, test chronologique 2014. Le notebook explique le nettoyage, les particularités du changement d'heure, la normalisation apprise sur l'entraînement, les fenêtres sans fuite, le LSTM PyTorch, trois graines, l'ablation 24 h, Ridge et les persistances 24/168 h.

## Résultats calculés

Sur 8 760 heures de test, MAE de l'ensemble LSTM : **2,044 kW**, contre **2,162 kW** pour la persistance hebdomadaire (amélioration de 5,49 %). La persistance quotidienne reste meilleure en MAE (**1,747 kW**). Le LSTM ne gagne donc pas sur tous les critères. Les erreurs par horizon, mois, pointes et hors fenêtres de changement d'heure sont fournies. Quatre graphiques et quatre modèles entraînés `.pt` sont inclus. Une prévision historique datée du 1er janvier 2015 illustre l'inférence ; ce n'est pas une prévision actuelle.

Temps observé sur cette machine : environ cinq minutes sur CPU. Il s'agit d'une reproduction sur données publiques, pas de résultats attestant une expérience de stage antérieure.

## Ouvrir et réexécuter

Le notebook est déjà exécuté : ses tableaux et graphiques sont lisibles sans entraînement supplémentaire. Décompresser le dossier entier, conserver son arborescence et ouvrir le fichier `.ipynb` dans JupyterLab. Pour reproduire les calculs, utiliser Python 3.12 dans un environnement virtuel, puis :

```text
python -m pip install -r requirements.txt
python -m jupyterlab
```

Choisir le noyau de cet environnement et « Redémarrer le noyau et tout exécuter ». Le dossier de travail doit être celui du notebook. Les données incluses permettent une exécution sans téléchargement. Les cellules de récupération des sources restent disponibles si les fichiers de données manquent. Internet est nécessaire à l'installation et à une nouvelle récupération. L'exécution réécrit les résultats du projet.

`donnees/` contient les données sources et leur provenance avec empreintes SHA-256 ; `resultats/` contient les prédictions, métriques, graphiques et configuration. `validation_livraison.json` rapporte les contrôles indépendants effectués sur la livraison. Les versions exactes de l'exécution figurent aussi dans la configuration enregistrée. De légers écarts numériques entre plateformes sont possibles.

## Attribution des données

Trindade, A. (2015), ElectricityLoadDiagrams20112014, UCI, DOI [10.24432/C58C86](https://doi.org/10.24432/C58C86), licence [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Le fichier fourni est un sous-ensemble des dix premiers clients, extrait sans modification des mesures ; l'agrégation horaire et les autres transformations sont documentées dans le notebook. L'archive UCI intégrale (environ 249 Mio) n'est pas incluse, mais son téléchargement est prévu dans le code.
