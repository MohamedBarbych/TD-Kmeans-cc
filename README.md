# Exercice 2 – Techniques de Fouille de Données 📊

## 👨‍🎓 Réalisé par : Mohamed BARBYCH  
**Module** : Data Mining  
**Encadrant** : Prof. Abdelhadi FENNAN  
![image](https://github.com/user-attachments/assets/d27b00d8-c3a5-43eb-9294-b3f795dd1057)

---

## 📌 Contexte de l’exercice

Une entreprise de services financiers souhaite améliorer ses services en exploitant la fouille de données. Elle dispose de données transactionnelles précises concernant les produits financiers achetés par ses clients. L’objectif est de :

- Segmenter les clients selon leurs habitudes d’achat avec **K-Means**
- Identifier les corrélations entre produits à l’aide de **l’algorithme Apriori**

---

## 1️⃣ Clustering avec K-Means

### 💡 Objectif
Segmenter les clients selon leurs comportements d’achat pour mieux cibler les services, produits et campagnes de marketing.

### 📘 Explication de l’algorithme

K-Means est un algorithme de clustering non supervisé basé sur la **minimisation de la distance intra-cluster** (ici : **distance euclidienne**). Il regroupe les données en **K groupes** en suivant ces étapes :

1. Initialisation de K centres (aléatoires ou déterminés)
2. Attribution des points au cluster le plus proche (distance euclidienne)
3. Recalcul des centroïdes (moyenne des points de chaque cluster)
4. Répétition jusqu’à convergence (pas de changement d’affectation)

### ⚖️ Choix du nombre optimal de clusters

- **Elbow Method** : On trace l’inertie intra-cluster en fonction de K et on cherche "le coude"
- **Silhouette Score** : Mesure la cohésion et la séparation entre clusters

---

### ⚙️ Étapes de mise en œuvre (avec K=3)

#### 🔁 Données encodées One-Hot :

| Client   | Prêt Pers. | Épargne | Crédit | Hypothèque | Assurance | Auto | Courant |
|----------|------------|---------|--------|------------|-----------|------|---------|
| Client 1 | 1          | 1       | 1      | 0          | 0         | 0    | 0       |
| Client 2 | 0          | 0       | 0      | 1          | 1         | 0    | 0       |
| Client 3 | 0          | 0       | 0      | 0          | 1         | 1    | 1       |
| Client 4 | 0          | 1       | 1      | 0          | 0         | 0    | 0       |
| Client 5 | 1          | 1       | 0      | 0          | 1         | 0    | 0       |
| Client 6 | 0          | 0       | 0      | 1          | 0         | 0    | 1       |

# 
![image](https://github.com/user-attachments/assets/8f4715f5-243b-4b93-9b6f-5811a8fed747)


#### 🔎 Résultats finaux :

| Client   | Cluster |
|----------|---------|
| Client 1 | 1       |
| Client 2 | 2       |
| Client 3 | 3       |
| Client 4 | 1       |
| Client 5 | 1       |
| Client 6 | 2       |


#
![image](https://github.com/user-attachments/assets/20593252-9270-48f4-a5ba-c4d9e1034442)

### 🧠 Interprétation des clusters

- **Cluster 1** : Clients 1, 4, 5  
  → Produits d’épargne, crédit personnel, carte de crédit  
- **Cluster 2** : Clients 2, 6  
  → Hypothèque, assurance, comptes  
- **Cluster 3** : Client 3  
  → Crédit auto, assurance, compte courant

![image](https://github.com/user-attachments/assets/e0c2857a-3850-4c97-898c-429336503cc4)


### 📊 Visualisation graphique
Une PCA a été utilisée pour représenter les clusters dans un espace 2D pour vérification de la séparation.
![image](https://github.com/user-attachments/assets/f2d78dc7-fdae-4b76-b401-eedd82dab2d7)

---

## 2️⃣ Règles d’Association – Algorithme Apriori

### 🎯 Objectif
Découvrir les combinaisons de produits souvent achetés ensemble afin de :

- Proposer des **ventes croisées**
- Créer des **recommandations ciblées**
- Optimiser les **offres groupées**

### 📦 Données transactionnelles

- T1 : {Prêt Perso, Compte Épargne, Carte de Crédit}
- T2 : {Compte Épargne, Carte de Crédit}
- T3 : {Auto, Courant, Assurance Vie}
- T4 : {Épargne, Carte de Crédit}
- T5 : {Prêt Perso, Épargne, Assurance Vie}

### ✅ Paramètres utilisés
- **min_support** = 0.4 (au moins dans 40% des transactions)
- **min_confidence** = 0.6 (au moins 60% de confiance)


![image](https://github.com/user-attachments/assets/de093af1-2578-41df-a19d-2b815c558e76)

### 🔍 Itemsets fréquents :

| Itemset                        | Support |
|-------------------------------|---------|
| Compte Épargne                | 0.8     |
| Carte de Crédit               | 0.6     |
| Prêt Personnel                | 0.4     |
| Compte Épargne, Carte Crédit  | 0.6     |
| Compte Épargne, Prêt Perso    | 0.4     |

### 🔗 Règles générées :

| Règle                                       | Confiance | Lift |
|--------------------------------------------|-----------|------|
| {Épargne} ⟶ {Crédit}                       | 0.75      | 1.25 |
| {Crédit} ⟶ {Épargne}                       | 1.00      | 1.25 |
| {Prêt Perso} ⟶ {Épargne}                  | 1.00      | 1.25 |

![image](https://github.com/user-attachments/assets/c5822362-2ff1-439c-af9c-310474fc19a7)

### 🧠 Interprétation des règles

Exemple :
- Règle : `{Épargne, Crédit} ⟶ {Prêt Perso}`
- Cela signifie que **les clients possédant un compte épargne et une carte de crédit ont une probabilité élevée (≥60%) de souscrire à un prêt personnel.**
![image](https://github.com/user-attachments/assets/764d6914-cdd9-4205-81ea-35be664d8885)


---

## 🎯 Applications pour l'entreprise

### ✅ Ciblage marketing intelligent
- Mieux connaître les profils de clients pour proposer des **offres adaptées à leurs besoins**.

### ✅ Recommandation de produits
- Suggérer des **produits financiers associés** (comme un prêt personnel à un client ayant un compte épargne).

### ✅ Promotions croisées
- Créer des **packs de services** et des **offres promotionnelles ciblées** pour augmenter le panier moyen.

---

## 🧪 Librairies utilisées

```python
pandas
sklearn
matplotlib
seaborn
mlxtend
