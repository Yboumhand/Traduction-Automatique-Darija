# 📘 Guide de Convention de Labellisation : Projet R&D Darija-MT

**Objectif :** Transformation du corpus "Silver Standard" en "Gold Standard" (Vérité Terrain) pour l'entraînement du modèle AraT5v2.

---

## 1. Principes de Nettoyage et Imputation (DQA)

Pour garantir la pureté et la complétude des données injectées dans le modèle, les règles suivantes sont appliquées :

- **Traitement du Bruit IA :** Retrait des artefacts de génération tels que `@@` et les symboles de hachage `#`.
- **Gestion des balises `<unk>` et Segments Incomplets :**
  - **Imputation Intelligente :** Si une balise `<unk>` ou un segment tronqué peut être complété par une prédiction logique basée sur le contexte ou une recherche rapide sur le net, l'information doit être restaurée.
  - **Suppression/Simplification :** Si l'information est irrécupérable, la balise est supprimée et la phrase est simplifiée pour conserver un sens complet (ex: _"band named <unk>"_ ➔ _"band"_).
- **Normalisation Spatiale :** Suppression des espaces doubles, ainsi que des espaces inutiles en début et fin de segment (trimming).

---

## 2. Règles de Script et Orthographe

La séparation stricte des alphabets est une contrainte majeure du projet :

### 2.1 Colonne `darija_arabic` (Script Arabe Unifié)

- **Zéro Latin :** Aucun caractère latin n'est toléré, y compris pour les acronymes (ex: `WWF` ➔ `دوبل في دوبل إف`).
- **Mots Étrangers :** Les termes d'origine française, espagnole ou anglaise intégrés au Darija doivent être écrits en caractères arabes.
  - _Exemple :_ `album` ➔ `ألبوم` | `bus` ➔ `طوبيس`.
- **Chiffres :** Utilisation des chiffres arabes occidentaux (`1`, `2`, `3`...) pour maintenir la cohérence avec les autres colonnes.

### 2.2 Colonne `darija_arabizi` (Phonétique Latine)

- **Harmonisation Phonétique :** Bien que la variation soit tolérée, une préférence est donnée à l'usage des chiffres pour les sons inexistants en latin (ex: `7` pour `ح`, `9` pour `ق`, `3` pour `ع`).
- **Mots d'origine étrangère :** Conservés dans leur alphabet d'origine s'ils sont prononcés tels quels.

---

## 3. Stratégie de Traduction (MSA & English)

L'objectif est d'assurer la **fidélité sémantique** tout en respectant le **flux naturel** de la langue cible :

- **Noms Propres & Titres :**
  - **English :** Le titre original est conservé (ex: _Fire and Glass_).
  - **MSA :** Le titre est traduit ou adapté pour ne pas briser la fluidité de la phrase arabe (ex: _النار والزجاج_). Les acronymes latins y sont tolérés.
- **Correction du "Flow" :** Les traductions automatiques (Silver) trop littérales sont reformulées manuellement pour correspondre au registre utilisé par un locuteur natif.

---

## 4. Annexe : Lexique de Convergence (Exemples)

| Terme Source | darija_arabizi | darija_arabic   | Règle appliquée                    |
| :----------- | :------------- | :-------------- | :--------------------------------- |
| Album        | album          | ألبوم           | Translittération arabe obligatoire |
| WWF          | WWF            | دوبل في دوبل إف | Zéro Latin en colonne arabe        |
| Gardien      | 7arris         | حارس            | Usage du '7' pour la consistance   |
| Région       | minta9a        | منطقة           | Usage du '9' pour la consistance   |
| Tragedy      | trajediya      | تراجيديا        | Adaptation phonétique en arabe     |
