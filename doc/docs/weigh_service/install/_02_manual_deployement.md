[< Retour](index.md)

# Installation manuelle AWS

⚠️ Le déploiement ne peut être effectué **qu'après l'installation des logiciels nécessaires**.

## Sommaire

- [Prérequis](#-prérequis)
- [Installation du projet](#-projet)
- [Création de l'environnement virtuel Python](#création-de-lenvironnement-virtuel-python)
- [Création du services windows (NSSM)](#-création-du-services-windows-nssm)

## 📋 Prérequis

- Accès à internet
- Python 3.9.x
- NSSM

- Récupérer le projet de base sur le partage :

```
Z:\Electrique\developpement\arp_weigh_service\DerniereVersion
```

## 📁 Projet

1. Copier le projet vers le dossier cible.

⚠️ Sur un **superviseur**, le projet doit **toujours** être installé dans :

```
C:\arp_weigh_service
```

La configuration du projet est expliquée ici:

- **[Configuration d'**A**rp **W**eigh **S**ervice](../config/index.md)**

## Création de l'environnement virtuel Python

1. Ouvrir **PowerShell** ou **CMD** en mode administrateur
2. Se déplacer dans le dossier **arp_weigh_service**

```bash
cd C:\arp_weigh_service
```

3. Autoriser l'exécution de scripts (si nécessaire)

```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

4. Créer un nouvel environnement virtuel

```bash
py -3.9 -m venv venv
```

5. Activer l'environnement

```bash
.\venv\Scripts\Activate.ps1
```

6. Installer les dépendances

```bash
pip install -r .\requirements.txt
```

## 🔁 Création du services windows (NSSM)

Le déploiement AWS utilise **1 service Windows** :

- **ARP_WEIGH_SERVICE**

### Se déplacer dans le dossier NSSM

```bash
cd C:\nssm\
```



### Créer le service ARP_WEIGH_SERVICE

```bash
.\nssm.exe install ARP_WEIGH_SERVICE
```



### Configurer le service

<details>
<summary>📷 Capture écran</summary>
<img src="img/NSSM_1.png">
<img src="img/NSSM_2.png">
<img src="img/NSSM_3.png">
<img src="img/NSSM_4.png">
</details>

### Onglet **Application**

| Champ                   | Valeur                                         |
| ----------------------- | -----------------------------------------------|
| Chemin                  | `C:\arp_weigh_service\venv\Scripts\python.exe` |
| Répertoire de démarrage | `C:\arp_weigh_service\`                        |
| Paramètres              | `-u C:\arp_weigh_service\com\main\main.py`     |


### Onglet **Actions d'arrêt**

```
Retarder le redémarrage : 5000 ms
```



### Onglet **E/S**

```
Sortie standard : C:\arp_weigh_service\logs\com_weigh_out.txt
Sortie d'erreur : C:\arp_weigh_service\logs\com_weigh_err.txt
```



### Onglet **Rotation des fichiers**
- Cocher :
    - Effectuer la rotation des fichiers
    - Pendant que le service tourne

```
Restreindre la rotation aux fichiers plus gros que : 100000000
```
Puis cliquer sur `Installer le service`

## 🧹 Nettoyage automatique des logs

Une tâche planifiée Windows doit etre créée afin de **nettoyer régulièrement les fichiers de logs**.

Cette tâche parcourt le dossier :

```
C:\arp_weigh_service\logs
```

et **supprime les fichiers vieux de plus de 14 jours**.

## Créer la tâche planifiée

Ouvrir **Planificateur de tâches** (`taskschd.msc`)

Cliquer sur **Créer une tâche…**

Configurer les paramètres suivants :

**Nom de la tâche**

```
AWS_LogCleanup_<ID>
```

Exemple :

```
AWS_LogCleanup_105
```

---

### 3️⃣ Déclencheur

Créer un déclencheur :

```
Tous les jours
Heure : 12:00
```

---

### 4️⃣ Action

Configurer l'action suivante :

**Programme :**

```
powershell.exe
```

**Arguments :**

```
-ExecutionPolicy Bypass -File C:\arp_weigh_service\cleanup_logs.ps1
```

---

### 5️⃣ Vérification

Après création, la tâche doit apparaître dans :

```
Task Scheduler Library
```

et être dans l'état :

```
Ready
```

---

### 6️⃣ Test manuel

Le script peut être exécuté manuellement avec :

```bash
powershell -ExecutionPolicy Bypass -File C:\arp_weigh_service\cleanup_logs.ps1
```

---

### Résultat

Cette tâche permet de :

- éviter un remplissage du disque
- maintenir uniquement **14 jours d'historique**



## Etape suivante

Passer à la configuration du projet
- **[Configuration d'**A**rp **W**eigh **S**ervice](../config/index.md)**