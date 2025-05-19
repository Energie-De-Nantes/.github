# ⚡️ Outils Open Source – Énergie De Nantes

Ce dépôt présente les principaux outils open source développés par l'association **Énergie De Nantes**, pour le traitement des données issues des flux Enedis, la vérification métier et la facturation.

---

## 🧩 Projets principaux

### 🔓 [electriflux](https://github.com/Energie-De-Nantes/electriflux)

> Télé[chargement,](https://github.com/Energie-De-Nantes/electriflux) déchiffrement et transformation des flux Enedis.

* Télécharge les fichiers via SFTP ou API Enedis.
* Déchiffre les fichiers à l’aide de certificats.
* Transforme les fichiers XML bruts en **DataFrames** ou **CSV** (linéarisation des données).
* Fournit une première couche de structure aux données avant tout traitement métier.

---

### 🧠 [electricore](https://github.com/Energie-De-Nantes/electricore)

> Mote[ur métier d](https://github.com/Energie-De-Nantes/electricore)e traitement et de vérification des données énergétiques.

* Vérification de la cohérence des données (doublons, ruptures, trous).
* Calculs de consommation par plage tarifaire (HP/HC).
* Application des taxes : **TURPE**, **CTA**, **Accise**, **TVA**.
* Résumés de périmètre fournisseur, statistiques, agrégats pour la facturation.

---

### 🧾 [stationreappropriation](https://github.com/Energie-De-Nantes/stationreappropriation)

> [Interface inter](https://github.com/Energie-De-Nantes/stationreappropriation)active en notebooks **Marimo** (équivalent moderne de Jupyter).

* Interface utilisateur pour orchestrer les traitements :

  * Génération de factures.
  * Refacturation après corrections ou changements de tarifs.
  * Calculs détaillés des taxes et résumés usager·e·s.
* Intègre `electriflux` et `electricore` pour proposer un outil tout-en-un accessible aux membres de l’association.

---

## 🛠 Utilisation typique

1. **Extraction** : Utiliser `electriflux` pour transformer les fichiers bruts en jeux de données exploitables.
2. **Traitement métier** : Passer les données dans `electricore` pour validation, calculs, et génération d’indicateurs.
3. **Pilotage** : Utiliser les notebooks de `stationreappropriation` pour exécuter les traitements complets et générer les documents utiles à la gestion du périmètre (factures, bilans, etc.).

---

## 🤝 Contribution

Ces outils sont pensés pour être réutilisables par d'autres collectifs, coopératives ou structures souhaitant se réapproprier la gestion des données énergétiques.
N'hésitez pas à ouvrir des issues, proposer des améliorations ou poser des questions.

---
