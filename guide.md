# 📁 Consignes du Projet NLP — Repository & Rapport Dataset

---

# 1. 📌 Création du Repository GitHub (OBLIGATOIRE)

- Un seul étudiant par groupe combiné doit créer un **repository privé GitHub**
- Invitez-moi avec cet email : **achrafmsa@hotmail.fr**
- Ajouter **tous les membres** du groupe comme collaborateurs (IMPORTANT : chacun doit pouvoir push)

---

# 2. 📂 Structure du Repository

Le repository doit contenir :

---

# 📓 Notebook Utilisé

Le fichier Jupyter Notebook utilisé pour générer ce rapport et analyser la data finale est inclus dans le repository :

- Nom du fichier : `final_analysis.ipynb`

## Contenu du notebook :
- Chargement du dataset final
- Analyse des données (statistiques, distribution des classes)
- Vérification des labels
- Calcul des métriques (taux d’erreur, corrections)
- Visualisations (si applicable)

Ce notebook permet de reproduire toutes les analyses présentées dans ce rapport.

---

## 📄 2.1 Fichier `GROUPS.md`
- Liste de tous les étudiants
- Numéro de groupe de chaque étudiant

---

## 📊 2.2 Dataset Final
- Dataset **fusionné entre tous les groupes**
- Dataset **nettoyé et final**
- Format clair (CSV / JSON)

---

## 📁 2.3 Dossiers par groupe
Créer un dossier pour chaque groupe :

/group_1
/group_2
/group_3
...


Chaque dossier doit contenir :
- Les notebooks du groupe
- Le travail individuel du groupe

---

## 📓 2.4 Notebook Final (OBLIGATOIRE)
Un notebook global contenant :
- Le workflow complet de fusion des données
- Les étapes de nettoyage
- Les étapes finales

---

## 📄 2.5 Méthode de Fusion (si différente)
Si vous utilisez une méthode différente :
- Ajouter un fichier `.md`
- Expliquer clairement votre approche

---

# 3. 📄 Rapport Dataset (Fichier Markdown OBLIGATOIRE)

Créer un fichier : `DATASET_REPORT.md`

---

# 4. 🧾 Contenu du DATASET_REPORT.md

---

## 4.1 🌍 Sources des Données

- Sources utilisées (sites, réseaux sociaux…)
- Pourquoi ces sources ?
- Description des sources
- Date de collecte
- Type de langue :
  - Arabe / Darija / Arabizi / Mixte
- Observations :
  - Qualité des données
  - Problèmes rencontrés
- Avantages de ces sources

---

## 4.2 🧹 Collecte & Nettoyage

- Méthode de collecte :
  - Scraping / API / manuel
- Étapes de nettoyage :
  - Suppression du bruit
  - Doublons
  - Normalisation

---

## 4.3 🏷️ Annotation du Gold Dataset

- Comment le gold dataset a été créé :
  - Annotation manuelle
- Qui a annoté ?
- Règles d’annotation utilisées
- Difficultés rencontrées

---

## 4.4 🤖 Labellisation Semi-Automatique avec IA

- Méthode utilisée :
  - API ou modèle local
- Nom exact du modèle utilisé :
  - Exemple : ChatGPT 5.4 (OBLIGATOIRE d’être précis)
- Description du processus :
  - Comment l’IA a labellisé les données

---

## 4.5 🔍 Vérification et Validation

- Comment vous avez vérifié les labels :
  - Relecture manuelle
  - Correction
- Qui a vérifié ?
- Méthode utilisée

---

## 4.6 📊 Analyse des Erreurs de l’IA

- Types d’erreurs :
  - Mauvaise classification
  - Ambiguïté
  - Sarcasme
- Exemples concrets

---

## 4.7 📈 Statistiques de Performance

### Avant correction :
- Nombre total de données labellisées automatiquement
- Nombre d’erreurs
- Taux d’erreur

### Après correction :
- Nombre corrigé
- Qualité finale estimée

---

## 4.8 🔧 Correction des Erreurs

- Comment les erreurs ont été corrigées
- Difficultés rencontrées

---

## 4.9 📊 Statistiques du Dataset

- Nombre total d’exemples
- Répartition des classes
- Problèmes de déséquilibre

---

## 4.10 ⚠️ Limites

- Biais des données
- Limites linguistiques (darija, arabizi…)
- Limites du modèle IA

---

## 4.11 🚀 Améliorations

- Ce qui peut être amélioré :
  - Données
  - Annotation
  - Modèle IA

---

# 5. ✅ Règles Importantes

- Soyez clairs et précis
- Justifiez vos choix
- Donnez des exemples
- Mentionnez toutes les erreurs rencontrées
- Soyez honnêtes (même sur les problèmes)

---