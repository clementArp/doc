[< Retour](index.md)

# Installation automatique AWM

⚠️ Le déploiement ne peut être effectué **qu'après l'installation des logiciels nécessaires**.

Ce script automatise :

✔ Installation de l'environnement Python
✔ Configuration MySQL
✔ Configuration IIS
✔ Création des services Windows
✔ Démarrage automatique

Cette documentation explique **comment utiliser l'outil de déploiement**, mais ne détaille pas toutes les actions effectuées.

Si l'outil ne peut pas être utilisé, la documentation suivante explique **les actions réalisées** qui peuvent aussi être réalisées **manuellements** :

[Installation manuelle AWM](_03_manual_deployement.md)

---

## Sommaire

- [Prérequis](#-prérequis)
- [Utilisation](#-utilisation)
- [Lancer le script en administrateur](#2️⃣-lancer-le-script-en-administrateur)
- [Vérifier le déploiement](#3️⃣-vérifier-le-déploiement)

---

# 📋 Prérequis

- Accès à internet vers `pypi.org:443` (optionnel mais conseillé)
  ⚠️ Si pas d'accés internet, une installation sera faite grâce au dossier **wheelhouse**
- MySQL accessible sur `127.0.0.1:3306`
- Récupérer le dossier suivant sur le partage :

```
Z:\Electrique\developpement\arp_web_machine\Utilitaires\awm_utils
```

- Récupérer le projet de base sur le partage :

```
Z:\Electrique\developpement\arp_web_machine\DerniereVersion\AWM
```

---

# 🚀 Utilisation

## 1️⃣ Paramètres demandés

Prévoir les paramètres suivants avant d'exécuter le script.

Le script demandera :

### Chemin du projet source AWM

Chemin du projet à copier.

Exemple :

```
D:/AWM
```

(peut être situé sur une clé USB par exemple)

---

### Numéro machine

Pour la machine **ARP105** :

```
105
```

⚠️ Pour **ARP99**, utiliser :

```
099
```

---

### Dossier cible

Sur un **superviseur**, le projet doit **toujours** être installé dans :

```
C:\AWM
```

💡 Si aucun chemin n'est renseigné, le dossier `C:\AWM` sera utilisé automatiquement.

---

### Langues recettes

Choisir les langues proposées à l'utilisateur.

Exemple :

```
FR,EN
```

Langues disponibles :

```
FR, EN, ES, DE, GR
```

---

### ALLOWED_IPS

Adresses IP des cartes réseau autorisées à accéder à l'application.

Exemple :

```
192.168.1.10 10.50.99.10
```

---

## 2️⃣ Lancer le script en administrateur

1. Ouvrir **PowerShell** ou **CMD** en mode administrateur
2. Se déplacer dans le dossier **awm_utils**

```bash
cd C:/.../awm_utils
```

3. Lancer le script

```bash
py deploy_v3.py
```

---

## 3️⃣ Vérifier le déploiement

### Accéder aux applications

```
APPS   : http://localhost:8000 + <ID>/
RECIPE : http://localhost:9000 + <ID>/
```

---

### Vérifier les services Windows

10 services doivent être actifs :

```
AWM_COM_APPS_1 → AWM_COM_APPS_5
AWM_COM_RECIPE_1 → AWM_COM_RECIPE_5
```

### Tâche planifiée de nettoyage des logs

Une tâche planifiée Windows est automatiquement créée lors du déploiement afin de **nettoyer les anciens logs du projet**.

Cette tâche :

- parcourt le dossier :

```
C:\AWM\logs
```

- ainsi que **tous ses sous-dossiers** (ex : `IIS_APPS\W3SVC*`)
- supprime tous les fichiers **plus vieux que 14 jours**

---

### Nom de la tâche

La tâche créée suit le format :

```
AWM_LogCleanup_<ID_MACHINE>
```

Exemple pour la machine **ARP301** :

```
AWM_LogCleanup_301
```

---

### Planification

La tâche est configurée pour s’exécuter :

```
Tous les jours à 12:00
```

Elle exécute le script :

```
C:\AWM\cleanup_logs.ps1
```

---

### Vérifier dans le planificateur de tâches

1. Ouvrir **Planificateur de tâches** (`taskschd.msc`)
2. Aller dans :

```
Task Scheduler Library
```

3. Rechercher la tâche :

```
AWM_LogCleanup_<ID_MACHINE>
```

4. Vérifier que l’état est :

```
Ready
```

---
