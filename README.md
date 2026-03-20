# TP2 - Spring IoC et Injection de Dépendances

![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat&logo=spring&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)
![Licence](https://img.shields.io/badge/License-MIT-green)
  
---

## 📖 Plan

[📝 Objectif](#-objectif)  
[📚 Contexte](#-contexte)  
[🏗 Structure du projet](#-structure-du-projet)  
[💻 Explication des classes](#-explication-des-classes)  
[📊 Résultats et interprétation](#-résultats-et-interprétation)  
[🧪 Exercices supplémentaires](#-exercices-supplémentaires)  
[💡 Concepts clés](#-concepts-clés)  



---

## 📝 Objectif

Ce TP permet de :  
- Comprendre l'**inversion de contrôle (IoC)** et l'**injection de dépendances (DI)** avec Spring  
- Créer et gérer des **beans Spring** via annotations  
- Injecter dynamiquement différentes implémentations d’une interface  
- Découvrir l’utilisation de **qualifiers** et de **profils Spring**  
- Configurer Spring via annotations ou XML  

---

## 📚 Contexte

Spring IoC permet de **découpler le code métier de ses dépendances**, en laissant le conteneur Spring instancier et injecter les objets.  
Dans ce TP :  

- **DAO** : fournit une valeur (ex : 100.0 ou 150.0 selon l’implémentation)  
- **Métier** : récupère la valeur via DAO et effectue un calcul (ex : multiplication par 2)  
- **Spring** : gère automatiquement les beans et leurs injections  

---

## 🏗 Structure du projet

<img width="299" height="415" alt="image" src="https://github.com/user-attachments/assets/862330fc-ba3a-4004-be57-9748b9395424" />


---

## 💻 Explication des classes

### 1️⃣ DAO
- `IDao` : interface définissant la méthode `getValue()`  
- `DaoImpl` : bean Spring annoté `@Component("dao")`, retourne 100.0  
- `DaoImpl2` : bean Spring annoté `@Component("dao2")`, retourne 150.0  

### 2️⃣ Métier
- `IMetier` : interface définissant la méthode `calcul()`  
- `MetierImpl` : bean Spring annoté `@Component("metier")`  
  - Injection par champ `@Autowired`  
  - Injection spécifique avec `@Qualifier("dao2")` si nécessaire  
  - Calcul : `dao.getValue() * 2`  

### 3️⃣ Présentation
- `Presentation2` :  
  - Utilise `AnnotationConfigApplicationContext`  
  - Active un **profil Spring** si nécessaire (`dev` ou `prod`)  
  - Récupère le bean `IMetier` et affiche le résultat  

- `PresentationXML` :  
  - Charge le contexte via `applicationContext.xml`  
  - Injection des dépendances par setter  

---


## 📊 Résultats et interprétation

Injection du bean par défaut (DaoImpl) :

Résultat = 200.0
<img width="914" height="172" alt="LAB2_JEE_Resultat presentation2" src="https://github.com/user-attachments/assets/2264f889-fd8a-4ced-8b58-816996ee894e" />


Injection avec @Qualifier("dao2") :

Résultat = 300.0

<img width="568" height="154" alt="LAB JEE ETAPE6" src="https://github.com/user-attachments/assets/64c127e3-6a03-4b52-97bb-b1bc9a1e52eb" />

Injection via XML :

Résultat (XML) = 300.0

<img width="568" height="154" alt="LAB JEE ETAPE6" src="https://github.com/user-attachments/assets/fb559542-f11a-428f-8171-f91d3b847562" />


Interprétation :

Spring IoC a correctement instancié les beans

L’injection de dépendances fonctionne automatiquement

Les différents profils et qualifiers permettent de changer dynamiquement l’implémentation utilisée



## 🧪 Exercices supplémentaires

Tests unitaires avec JUnit pour MetierImpl

Injection via XML

Gestion de profils Spring (dev, prod) pour différents beans

## 💡 Concepts clés

IoC : inversion du contrôle de création des objets

DI : injection de dépendances automatiquement par Spring

Qualifiers : choisir l’implémentation spécifique

Profils Spring : activer des beans selon l’environnement




