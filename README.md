# 📘 Guide de Convention de Labellisation : Projet R&D Darija-MT

**Objectif :** Transformation du corpus "Silver Standard" en "Gold Standard" (Vérité Terrain) pour l'entraînement du modèle AraT5v2.

---

## 1. Principes de Nettoyage Automatique (DQA)

Pour garantir la pureté des données injectées dans le modèle, les règles de nettoyage suivantes sont appliquées systématiquement :

- **Suppression du Bruit IA :** Retrait des artefacts de génération tels que `@@`, `<unk>`, et les symboles de hachage `#`.
- **Normalisation Spatiale :** Suppression des espaces doubles, ainsi que des espaces inutiles en début et fin de segment (trimming).
- **Gestion des Segments Incomplets :** Si une phrase est tronquée ou sans suite logique (ex: _"band named <unk>"_), elle est simplifiée pour conserver un sens complet (ex: _"band"_).

---

## 2. Règles de Script et Orthographe

La séparation stricte des alphabets est une contrainte majeure du projet :

### 2.1 Colonne `darija_arabic` (Script Arabe Unifié)

- **Zéro Latin :** Aucun caractère latin n'est toléré.
- **Mots Étrangers :** Les termes d'origine française, espagnole ou anglaise intégrés au Darija doivent être écrits en caractères arabes.
  - _Exemple :_ `album` ➔ `ألبوم` | `bus` ➔ `طوبيس`.
- **Chiffres :** Utilisation des chiffres arabes occidentaux (`1`, `2`, `3`...) pour maintenir la cohérence avec les autres colonnes.

### 2.2 Colonne `darija_arabizi` (Phonétique Latine)

<- **Harmonisation Phonétique :** Bien que la variation soit tolérée, une préférence est donnée à l'usage des chiffres pour les sons inexistants en latin (ex: `7` pour `ح`, `9` pour `ق`, `3` pour `ع`).

- **Mots d'origine étrangère :** Conservés dans leur alphabet d'origine s'ils sont prononcés tels quels.

---

## 3. Stratégie de Traduction (MSA & English)

L'objectif est d'assurer la **fidélité sémantique** tout en respectant le **flux naturel** de la langue cible :

- **Noms Propres & Titres :**
  - **English :** Le titre original est conservé (ex: _Fire and Glass_).
  - **MSA :** Le titre est traduit ou adapté pour ne pas briser la fluidité de la phrase arabe (ex: _النار والزجاج_).
- **Correction du "Flow" :** Les traductions automatiques (Silver) trop littérales sont reformulées manuellement pour correspondre au registre utilisé par un locuteur natif.

---

## 4. Annexe : Lexique de Convergence (Exemples)

Afin d'assurer la consistance du modèle, les choix suivants ont été standardisés :

| Terme Source | darija_arabizi | darija_arabic | Règle appliquée                    |
| :----------- | :------------- | :------------ | :--------------------------------- |
| Album        | album          | ألبوم         | Translittération arabe obligatoire |
| Gardien      | 7arris         | حارس          | Usage du '7' pour la consistance   |
| Région       | minta9a        | منطقة         | Usage du '9' pour la consistance   |
| Tragedy      | trajediya      | تراجيديا      | Adaptation phonétique en arabe     |
