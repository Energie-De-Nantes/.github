# ⚡️ Outils libres – Énergie De Nantes

**Énergie De Nantes** est une association qui développe des outils open source pour **reprendre le contrôle des données du réseau électrique français** : déchiffrer les flux Enedis, en vérifier la cohérence, calculer les taxes et produire une facturation juste — sans dépendre d'outils propriétaires opaques.

> Tout est publié sous licence **AGPL-3.0** et pensé pour être réutilisé par d'autres collectifs, coopératives et fournisseurs locaux.

<p align="center">
  <img src="https://raw.githubusercontent.com/Energie-De-Nantes/.github/main/profile/assets/bascule-controle.png" alt="La bascule du contrôle — les outils libres d'Énergie De Nantes font basculer le contrôle des données du réseau, du monopole et sa boîte noire vers le collectif qui maîtrise ses données : electricore (le moteur) et souscriptions_odoo (l'addon de facturation) sont le levier." width="900">
</p>

---

## 🎯 Pourquoi ?

Les données qui décrivent ta consommation et fondent ta facture sont distribuées par un monopole, sous une forme **chiffrée et opaque**. Nos outils font levier pour faire **basculer ce contrôle vers le collectif** :

- **🔓 Réappropriation & souveraineté** — déchiffrer et structurer soi-même les flux Enedis. Tes données t'appartiennent.
- **♻️ Libre & réutilisable** — open source (AGPL-3.0), réutilisable par d'autres collectifs, coopératives et fournisseurs locaux.
- **🧾 Transparence de la facturation** — une facturation juste, traçable et maîtrisée de bout en bout : tu sais d'où vient chaque euro.
- **🛠️ Maîtrise technique** — une stack moderne (Polars, DuckDB, dbt, FastAPI), testée et documentée, sans boîte noire.

---

## 🧩 Les outils

### 🧠 [electricore](https://github.com/Energie-De-Nantes/electricore) — le moteur

Le cœur du système. Il **ingère** les flux Enedis (SFTP + déchiffrement AES) et les linéarise (dlt + dbt → DuckDB), **vérifie** leur cohérence (doublons, ruptures, trous), **calcule** les indicateurs métier (périmètre, abonnements, consommations HP/HC, **TURPE**, **CTA**, **Accise**) et **expose** le tout via une API REST sécurisée (FastAPI). Un bot Telegram pilote l'exploitation au quotidien.

- Pur **Polars + DuckDB**, architecture fonctionnelle (query builders immuables).
- `core/` ERP-agnostique ; les intégrations (Odoo) vivent à part.
- Déployable sur un VPS en une commande (Docker, TLS automatique).

### 🧾 [souscriptions_odoo](https://github.com/Energie-De-Nantes/souscriptions_odoo) — l'addon de facturation

Un addon **Odoo** qui **consomme l'API d'electricore** (via le client léger `electricore-client`, httpx + pydantic) pour gérer les **souscriptions** et leurs **périodes**, puis produire les **factures** directement dans l'ERP. C'est la couche métier de facturation, branchée sur le moteur sans le dupliquer.

> Le pont entre les deux est un flux **JSONL typé** : electricore calcule l'assiette (énergie, TURPE…), souscriptions_odoo construit la facture.

---

## 🛠 Comment ça s'assemble

```
Flux Enedis (chiffrés, opaques)
        │   SFTP + déchiffrement AES
        ▼
   electricore  ──►  ingestion (dlt + dbt → DuckDB)
        │            vérification · calculs · taxes (TURPE, CTA, Accise)
        │   API REST — flux JSONL typé
        ▼
 souscriptions_odoo  ──►  souscriptions · périodes · factures (Odoo)
```

1. **Réappropriation** — electricore télécharge et déchiffre les flux Enedis, puis les transforme en données structurées et vérifiées.
2. **Calcul** — il calcule consommations, abonnements et taxes : la matière première d'une facture juste.
3. **Facturation** — souscriptions_odoo tire ces données via l'API et produit les factures dans Odoo.

---

## 📜 Origines

Ces outils sont nés de deux dépôts antérieurs, aujourd'hui consolidés :
[**electriflux**](https://github.com/Energie-De-Nantes/electriflux) (téléchargement / déchiffrement / parsing des flux) a été absorbé dans le moteur d'ingestion d'electricore, et [**stationreappropriation**](https://github.com/Energie-De-Nantes/stationreappropriation) (notebooks Marimo) a laissé place à souscriptions_odoo. On les garde en archive pour la mémoire du projet.

---

## 🤝 Contribution

Ces outils sont pensés pour être réutilisés par d'autres collectifs, coopératives ou structures souhaitant se réapproprier la gestion de leurs données énergétiques.
N'hésitez pas à ouvrir des issues, proposer des améliorations ou poser des questions.
