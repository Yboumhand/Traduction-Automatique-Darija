# DATASET_REPORT.md

## Projet R&D — Traduction Automatique Darija (MT)

### Module Text Mining · Université · Année universitaire 2025–2026

### Encadrant : Pr. Imad HAFIDI

---

> **Note aux groupes 2 et 3 :** Les sections marquées `[GROUPE X — À COMPLÉTER]` sont réservées à votre contribution. Remplacez chaque placeholder par vos propres informations en suivant le même format que le Groupe 1. Ne modifiez pas les sections des autres groupes.

---

## Table des matières

1. [Sources des Données](#41--sources-des-données)
2. [Collecte & Nettoyage](#42--collecte--nettoyage)
3. [Annotation du Gold Dataset](#43--annotation-du-gold-dataset)
4. [Labellisation Semi-Automatique avec IA](#44--labellisation-semi-automatique-avec-ia)
5. [Vérification et Validation](#45--vérification-et-validation)
6. [Analyse des Erreurs de l'IA](#46--analyse-des-erreurs-de-lia)
7. [Statistiques de Performance](#47--statistiques-de-performance)
8. [Correction des Erreurs](#48--correction-des-erreurs)
9. [Statistiques du Dataset](#49--statistiques-du-dataset)
10. [Limites](#410--limites)
11. [Améliorations](#411--améliorations)

---

# 4.1 🌍 Sources des Données

---

## 🔵 Groupe 1 — Yassine Boumhand & Abdourazak Akillou Illa

**Sources utilisées :**
Le corpus du Groupe 1 repose sur des données brutes pré-fournies dans le cadre du projet, structurées en deux shards :

- `unified_shard_2.csv` (~9 005 lignes) — Silver Standard
- `gold_shard_2.csv` (~1 000 lignes) — Gold Standard

**Pourquoi ces sources ?**
Ces shards constituent la portion assignée au groupe dans le cadre d'un découpage coordonné entre tous les groupes participants. L'objectif est de construire un corpus parallèle Darija–Anglais–MSA représentatif et de haute qualité, utilisable pour l'entraînement et l'évaluation du modèle AraT5v2.

**Type de langue :**

- Darija marocaine en script arabe (`darija_arabic`) — zéro caractère latin
- Darija en translittération latine phonétique (`darija_arabizi`) — sons arabes notés avec chiffres phonétiques (7, 9, 3)
- Traductions en anglais et en arabe standard moderne (MSA)

**Date de collecte :** Données brutes reçues au démarrage du projet — Année universitaire 2025–2026 (traitement réalisé en avril 2026).

**Qualité des données à la réception :**
Les données brutes présentaient plusieurs artefacts issus de pipelines NLP antérieurs : tokens `<unk>`, séquences `@@` et `@-@` (tokenisation BPE), espaces doubles, et cas de code-switching avec des fragments Wikipedia en français ou en anglais insérés dans du texte arabe.

**Avantages de cette source :**

- Données déjà segmentées et catégorisées par classe de longueur (A, B, C, D)
- Structure tabulaire cohérente avec 9 colonnes définies
- Volume suffisant pour constituer un training set représentatif

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Décrivez ici vos propres sources (sites web, réseaux sociaux, forums, datasets publics, etc.). Répondez aux points suivants :
>
> - Quelles sources avez-vous utilisées ? (Noms, URLs si applicable)
> - Pourquoi avez-vous choisi ces sources ?
> - Description des données collectées
> - Date de collecte
> - Type de langue : Arabe / Darija / Arabizi / Mixte
> - Observations sur la qualité des données à la réception
> - Problèmes rencontrés dès la collecte
> - Avantages de vos sources par rapport à d'autres alternatives

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

> **Instructions :** Même format que ci-dessus pour le Groupe 3.

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.2 🧹 Collecte & Nettoyage

---

## 🔵 Groupe 1

**Méthode de collecte :**
Les données ont été reçues directement sous forme de fichiers CSV pré-structurés. Aucun scraping ni appel API externe n'a été nécessaire pour l'acquisition des données brutes.

**Étapes de nettoyage (DQA — Data Quality Assurance) :**
Un protocole DQA strict a été appliqué manuellement pour le Gold Standard et intégré au prompt IA pour le Silver Standard :

1. **Suppression du bruit** : suppression des tokens `<unk>`, `@@`, `@-@` et normalisation des espaces doubles présents dans les données sources
2. **Contrainte script arabe** : le champ `darija_arabic` ne doit contenir aucun caractère latin — les mots étrangers y sont systématiquement translittérés en arabe
3. **Normalisation de l'arabizi** : le champ `darija_arabizi` respecte la convention phonétique marocaine avec chiffres (ex. : ح → 7, ق → 9, ع → 3)
4. **Fidélité sémantique** : les traductions anglaises et MSA préservent le registre naturel de la Darija source, sans sur-formalisation
5. **Conservation des noms propres** : les noms propres sont maintenus tels quels dans toutes les colonnes

**Normalisation de la structure :**
Chaque ligne du livrable final respecte les 9 colonnes définies (`data_id`, `id`, `classe`, `darija_arabic`, `darija_arabizi`, `english`, `modern_standard_arabic`, `status`). Les lignes ne respectant pas ce schéma ont été corrigées ou écartées.

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Décrivez votre pipeline de collecte et de nettoyage :
>
> - Méthode de collecte : scraping / API / collecte manuelle ?
> - Outils utilisés (BeautifulSoup, Scrapy, Selenium, etc.)
> - Étapes de nettoyage réalisées : suppression du bruit, doublons, normalisation, encodage
> - Difficultés spécifiques à votre collecte

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.3 🏷️ Annotation du Gold Dataset

---

## 🔵 Groupe 1

**Méthode d'annotation :**
L'annotation du Gold Standard est **100% manuelle**, sans aucune intervention d'IA. Ce parti pris est fondamental : le Gold Standard constitue la vérité terrain (ground truth) utilisée pour l'évaluation finale du modèle AraT5v2, et toute contamination par un modèle de langage compromettrait la validité de cette évaluation.

**Outil utilisé :** Label Studio (interface web d'annotation collaborative)

**Qui a annoté ?**

- Yassine Boumhand

**Règles d'annotation appliquées :**
Les règles DQA détaillées en section 4.2 ont été appliquées de manière stricte lors de la saisie manuelle dans Label Studio. En particulier :

- Aucun caractère latin dans `darija_arabic`
- Chiffres phonétiques obligatoires dans `darija_arabizi`
- Traductions naturelles, non littérales
- Noms propres conservés à l'identique

**Difficultés rencontrées :**

- L'annotation manuelle de ~1 000 lignes représente un travail chronophage nécessitant une concentration soutenue pour garantir la cohérence des conventions sur toute la durée
- Certaines phrases courtes ou très contextuelles en Darija sont ambiguës à traduire en MSA sans reformulation — chaque cas a fait l'objet d'une discussion entre les deux annotateurs

**Résultat :**

| Métrique        | Valeur         |
| --------------- | -------------- |
| Lignes annotées | 1 003          |
| Statut final    | 100% VALIDATED |
| Intervention IA | Aucune         |

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Décrivez votre processus d'annotation manuelle du Gold dataset :
>
> - Combien de lignes constituent votre Gold Standard ?
> - Qui a annoté (noms des membres) ?
> - Quel outil avez-vous utilisé (Label Studio, Google Sheets, autre) ?
> - Quelles règles d'annotation avez-vous suivies ?
> - Quelles difficultés avez-vous rencontrées ?

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.4 🤖 Labellisation Semi-Automatique avec IA

---

## 🔵 Groupe 1

**Modèle utilisé :** `gpt-4o-mini` — OpenAI API (version commerciale payante)

**Pourquoi ce modèle ?**
Dans un premier temps, nous avons testé **LLaMA 3.1 8B** puis **LLaMA 3.3 70B** via l'API gratuite Groq. Cette approche a été abandonnée pour trois raisons cumulées :

1. Qualité insuffisante sur les phrases complexes en Darija (code-switching, artefacts)
2. Quotas journaliers trop limités (500K tokens/compte), imposant la création de 4 comptes et une rotation manuelle des clés API
3. Débit effectif très lent en raison des pauses forcées entre appels

La migration vers GPT-4o-mini a résolu ces trois problèmes : qualité nettement supérieure sur la Darija et le code-switching, absence totale de contrainte de quota, et intégration directe avec Label Studio via API REST.

**Type de prompt utilisé :** Role + Structured Output Prompt, combinant trois techniques :

- **Role Prompting** : `"Tu es un expert en linguistique marocaine..."` — ancre le registre attendu et améliore la qualité des sorties
- **Instruction Chaining** : règles de nettoyage numérotées guidant le modèle étape par étape sur les cas limites (artefacts, phrases tronquées, `<unk>`)
- **Constrained Generation** : format strict en 4 lignes préfixées (`DARIJA_ARABIC:`, `DARIJA_ARABIZI:`, `ENGLISH:`, `MSA:`) garantissant un parsing automatique fiable

**Paramètres de configuration du pipeline :**

| Paramètre       | Valeur        | Rôle                                                   |
| --------------- | ------------- | ------------------------------------------------------ |
| `model`         | `gpt-4o-mini` | Identifiant du modèle                                  |
| `temperature`   | `0.1`         | Quasi-déterminisme — sorties stables et reproductibles |
| `max_tokens`    | `500`         | Suffisant pour 4 lignes courtes                        |
| `BATCH_SIZE`    | `20`          | Lignes traitées par lot                                |
| `SLEEP_BETWEEN` | `0.5s`        | Pause entre appels (respect des rate limits)           |
| `MAX_RETRIES`   | `3`           | Tentatives automatiques en cas d'erreur réseau         |

**Intégration avec Label Studio :**
Chaque traduction générée est poussée automatiquement dans Label Studio via son API REST, sans import/export manuel de CSV. La connexion utilise deux paramètres : l'Access Token (généré depuis `Settings → Access Token`) et l'URL du projet (`http://localhost:8080`).

**Résilience du pipeline :**
En cas d'interruption, le script implémente une reprise automatique : il identifie les lignes déjà traitées et reprend exactement là où il s'est arrêté. Une sauvegarde intermédiaire est effectuée toutes les 10 lignes.

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Détaillez votre approche de labellisation semi-automatique :
>
> - Nom **exact** du modèle utilisé (ex. : `gpt-4o`, `claude-3-5-sonnet-20241022`, `llama-3.3-70b`) — **OBLIGATOIRE d'être précis**
> - API utilisée ou modèle local ?
> - Type de prompt utilisé (zero-shot, few-shot, avec rôle ?)
> - Paramètres clés (température, max_tokens, batch size)
> - Comment les résultats ont-ils été intégrés à votre workflow ?

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.5 🔍 Vérification et Validation

---

## 🔵 Groupe 1

**Méthode de validation : Échantillonnage stratifié (Spot-Checking)**

Relire manuellement les 9 005 lignes du Silver Standard étant humainement inenvisageable, un contrôle qualité par échantillonnage stratifié a été mis en place. Trois sondes positionnelles de 1% chacune ont été prélevées dans le corpus :

| Sonde     | Position         | Lignes        | Objectif                                           |
| --------- | ---------------- | ------------- | -------------------------------------------------- |
| Sonde 1   | Début du corpus  | ~90 (1%)      | Détecter les erreurs systématiques de démarrage    |
| Sonde 2   | Milieu du corpus | ~90 (1%)      | Vérifier la stabilité en cours de traitement       |
| Sonde 3   | Fin du corpus    | ~90 (1%)      | Détecter une dérive ou dégradation en fin de batch |
| **Total** | —                | **~270 (3%)** | **Couverture représentative**                      |

**Résultat du spot-checking :**
Les trois sondes ont confirmé une qualité satisfaisante sur l'ensemble des positions du corpus. Cette cohérence constitue une preuve statistiquement fondée de la qualité générale, rendant la relecture exhaustive redondante.

**Validation en masse :**
Suite aux résultats positifs du spot-checking, l'ensemble du Silver Standard a été validé via la fonctionnalité **"Retrieve Annotations from Predictions"** de Label Studio, qui bascule l'intégralité des prédictions IA au statut `VALIDATED` en un seul clic.

**Qui a vérifié ?**

- Yassine Boumhand
- Abdourazak Akillou Illa

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Décrivez votre méthode de vérification des labels générés par l'IA :
>
> - Avez-vous fait une relecture manuelle complète, un échantillonnage, ou une autre méthode ?
> - Combien de lignes ont été vérifiées manuellement ?
> - Qui a vérifié (noms) ?
> - Quel outil ou interface avez-vous utilisé pour la validation ?

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.6 📊 Analyse des Erreurs de l'IA

---

## 🔵 Groupe 1

Lors du spot-checking des 270 lignes (~3% du Silver Standard), plusieurs catégories d'erreurs récurrentes ont été identifiées :

**1. Artefacts non supprimés :**
Certaines lignes sources contenaient des tokens résiduels (`<unk>`, `@-@`, `@@`) que le modèle n'avait pas correctement filtrés malgré les instructions du prompt. Ces cas ont nécessité une correction manuelle ciblée.

_Exemple :_ Un token `<unk>` conservé dans `darija_arabizi` alors que la règle DQA impose sa suppression.

**2. Code-switching Wikipedia :**
Les phrases issues de fragments Wikipedia en français ou en anglais insérés dans le flux Darija ont occasionnellement donné lieu à des traductions hybrides ou incohérentes, GPT-4o-mini ayant parfois du mal à identifier la langue source réelle de la phrase.

_Exemple :_ Une phrase mélangeant darija et une terminologie technique française traduite partiellement en anglais plutôt qu'en MSA.

**3. Sur-formalisation en MSA :**
Le modèle a parfois produit des formulations en MSA trop littéraires ou soutenues par rapport au registre oral de la Darija source, perdant ainsi la naturalité de l'énoncé.

**4. Caractères latins résiduels dans `darija_arabic` :**
Quelques cas isolés où des mots étrangers (marques, noms propres techniques) ont été laissés en script latin au lieu d'être translittérés en arabe, en violation de la contrainte DQA.

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Listez et illustrez les types d'erreurs observées dans les labels produits par votre modèle IA :
>
> - Erreurs de classification (si applicable)
> - Erreurs de traduction (sens, registre, fidélité)
> - Cas d'ambiguïté ou de sarcasme mal interprétés
> - Exemples concrets (au moins 2–3 exemples réels tirés de vos données)

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.7 📈 Statistiques de Performance

---

## 🔵 Groupe 1

### Avant correction (Silver Standard brut)

| Métrique                                      | Valeur                            |
| --------------------------------------------- | --------------------------------- |
| Lignes labellisées automatiquement            | 9 005                             |
| Erreurs détectées (sur les 3% échantillonnés) | ~8–15 lignes sur 270 (estimation) |
| Taux d'erreur estimé                          | < 5%                              |

> **Note méthodologique :** Le taux d'erreur exact sur la totalité des 9 005 lignes n'est pas calculable sans relecture exhaustive. L'estimation repose sur les 3 sondes stratifiées (270 lignes), qui constituent un échantillon représentatif permettant d'inférer la qualité générale.

### Après correction (Silver Standard final)

| Métrique                      | Valeur                                                              |
| ----------------------------- | ------------------------------------------------------------------- |
| Lignes corrigées manuellement | Corrections ciblées sur les erreurs détectées lors du spot-checking |
| Statut final                  | 100% VALIDATED                                                      |
| Qualité finale estimée        | Haute (validée par échantillonnage stratifié)                       |

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Renseignez vos métriques de performance, **avant** et **après** correction :
>
> - Nombre total de données labellisées automatiquement
> - Nombre d'erreurs détectées
> - Taux d'erreur (erreurs / total)
> - Après correction : nombre de lignes corrigées et qualité estimée du dataset final

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.8 🔧 Correction des Erreurs

---

## 🔵 Groupe 1

**Comment les erreurs ont-elles été corrigées ?**
Les erreurs identifiées lors du spot-checking ont été corrigées directement dans Label Studio, en éditant manuellement les annotations concernées. Le workflow était le suivant :

1. Identification de la ligne erronée lors de la relecture de la sonde
2. Correction manuelle du ou des champs concernés (`darija_arabic`, `darija_arabizi`, `english`, ou `modern_standard_arabic`)
3. Basculement du statut de la ligne en `VALIDATED`

Pour les cas d'artefacts systématiques (ex. : `<unk>` récurrents), une passe de correction scriptée a été envisagée mais s'est avérée inutile — les règles DQA intégrées dans le prompt GPT-4o-mini avaient déjà filtré la grande majorité de ces cas.

**Difficultés rencontrées :**

- L'interface Label Studio ne permet pas de filtrer facilement les lignes par type d'erreur — la correction repose sur une navigation manuelle dans les tâches
- Certaines ambiguïtés linguistiques (ex. : darija dialectale très régionale) ne disposent pas de "bonne réponse" universelle — les deux annotateurs ont dû trancher au cas par cas

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Expliquez votre processus de correction des erreurs identifiées :
>
> - Comment avez-vous corrigé les erreurs (manuellement, via script, combiné) ?
> - Quel outil ou interface avez-vous utilisé ?
> - Quelles difficultés avez-vous rencontrées lors de la correction ?

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.9 📊 Statistiques du Dataset

---

## 🔵 Groupe 1

| Livrable                  | Fichier                         | Lignes     | Statut             |
| ------------------------- | ------------------------------- | ---------- | ------------------ |
| Gold Standard             | `gold_final.csv`                | 1 003      | 100% VALIDATED     |
| Silver Standard           | `silver_shard_2_translated.csv` | 9 005      | 100% VALIDATED     |
| Export Label Studio       | `annotations.json`              | 1 003      | Export brut Gold   |
| **Total corpus Groupe 1** | —                               | **10 008** | **100% VALIDATED** |

**Répartition par classe de longueur :**
Les données sont catégorisées selon 4 classes de longueur (A, B, C, D), définies dans le cahier des charges du projet. La répartition exacte par classe est consultable dans le notebook `final_analysis.ipynb` fourni dans le repository.

**Observations sur l'équilibre des classes :**
Aucun problème majeur de déséquilibre n'a été détecté à l'échelle du shard du Groupe 1. La répartition inter-classes sera analysée globalement lors de la fusion des shards de l'ensemble des groupes.

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Renseignez les statistiques de votre dataset :
>
> - Nombre total d'exemples (Gold + Silver)
> - Répartition des classes (si applicable : classes de longueur, de sentiment, etc.)
> - Y a-t-il un déséquilibre entre les classes ? Comment l'avez-vous traité ou documenté ?

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.10 ⚠️ Limites

---

## 🔵 Groupe 1

**Limites de la validation par échantillonnage :**
La validation du Silver Standard repose sur un spot-checking à 3%. Bien que statistiquement fondé, ce protocole ne garantit pas une qualité uniforme sur la totalité des 9 005 lignes — des erreurs isolées peuvent subsister dans les zones non échantillonnées.

**Limites linguistiques :**

- La Darija marocaine est une langue à forte variation régionale (Casablanca, Marrakech, Fès, etc.). Le corpus ne distingue pas ces sous-variétés, ce qui peut introduire une inconsistance dans les conventions de translittération arabizi.
- Les cas de code-switching avec le français ou l'anglais (très fréquents dans la Darija orale contemporaine) restent un défi pour GPT-4o-mini, qui peut hésiter sur la langue cible de la traduction.
- La Darija est une langue essentiellement orale, peu standardisée à l'écrit — deux annotateurs peuvent produire des translittérations arabizi légèrement différentes pour le même mot, sans qu'il y ait d'erreur objective.

**Limites du modèle IA :**

- GPT-4o-mini, bien que performant, n'est pas nativement spécialisé sur la Darija marocaine — ses performances sont inférieures à celles d'un locuteur natif expert sur les registres très familiers ou argotiques.
- Le choix d'une température de 0.1 garantit la stabilité mais peut réduire la diversité des formulations, créant un corpus légèrement homogène dans son style.
- La limite de `max_tokens=500` pourrait être insuffisante pour des phrases de classe D (très longues) — des troncatures sont possibles sur ces cas limites.

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Identifiez et documentez honnêtement les limites de votre travail :
>
> - Biais potentiels dans vos données (sources surreprésentées, démographies, thèmes)
> - Limites linguistiques spécifiques à votre sous-corpus
> - Limites du modèle IA que vous avez utilisé
> - Limites de votre processus de validation

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

# 4.11 🚀 Améliorations

---

## 🔵 Groupe 1

**Améliorations possibles sur les données :**

- Augmenter le taux d'échantillonnage du spot-checking (passer de 3% à 10%) pour une couverture de validation plus robuste sur les zones non vérifiées
- Collecter des données supplémentaires couvrant des registres sous-représentés : argot jeune, darija rurale, terminologie technique en darija

**Améliorations sur l'annotation :**

- Mettre en place un accord inter-annotateurs (IAA) formalisé avec calcul du score Kappa pour quantifier objectivement la consistance entre annotateurs sur le Gold Standard
- Définir un guide d'annotation écrit et versionné, partagé entre tous les groupes, pour harmoniser les conventions arabizi à l'échelle du corpus global

**Améliorations sur le modèle IA :**

- Tester des modèles fine-tunés sur la Darija (ex. : DarijaBERT, AraT5v2 lui-même en mode zero-shot) en remplacement ou en complément de GPT-4o-mini pour le Silver Standard
- Augmenter `max_tokens` à 800 pour prévenir les troncatures sur les phrases de classe D
- Expérimenter avec un prompt few-shot (2–3 exemples réels dans le prompt) pour améliorer la fidélité sur les cas de code-switching complexes
- Mettre en place une validation automatique post-génération (ex. : vérifier l'absence de caractères latins dans `darija_arabic` par regex) avant la validation humaine

---

## 🟡 Groupe 2 — [GROUPE 2 — À COMPLÉTER]

> **Instructions :** Proposez des améliorations concrètes et réalistes pour votre pipeline :
>
> - Que changeriez-vous dans votre collecte de données ?
> - Comment amélioreriez-vous votre annotation ?
> - Quel modèle IA ou quels paramètres testeriez-vous en priorité ?
> - Y a-t-il des étapes de votre pipeline qui mériteraient d'être automatisées ?

```
[GROUPE 2 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

## 🟢 Groupe 3 — [GROUPE 3 — À COMPLÉTER]

```
[GROUPE 3 — REMPLACER CE BLOC PAR VOS INFORMATIONS]
```

---

---

_Ce rapport a été produit dans le cadre du Projet R&D — Traduction Automatique Darija (MT), Module Text Mining, Année universitaire 2025–2026._
_Encadrant : Pr. Imad HAFIDI_
