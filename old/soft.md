# Installation des logiciels

📂 Les installateurs sont disponibles ici :

```
Z:\Electrique\developpement\arp_web_machine\Logiciels
```

Fichiers nécessaires :

- `python-3.9.1-amd64.exe`
- `mysql-installer-community-8.0.35.0.msi`
- `nssm.exe`
- `httpPlatformHandler_amd64.msi`

---

## Résumé Ultra Rapide

1. IIS (+ httpPlatformHandler)
2. Installer MySQL (Custom + mot de passe arp360arp360)
3. Installer Python 3.9 (Add to PATH)
4. Donner droits IIS_IUSRS à Python39
5. Copier nssm.exe dans C:\nssm
6. Lancer le script

---

## 1️⃣ Activer IIS

1. Ouvrir **Panneau de configuration**
2. Aller dans **Programmes > Activer ou désactiver des fonctionnalités Windows**
3. Aller dans **Internet Information Services / Service World Wild / Fonctionnalités de développement d’applications**
4. Cocher **Initialisation d’applications** ✅

   <details>
    <summary>📷 Capture écran</summary>

   ![img](img/IIS_2.png)

    </details>

5. Cliquer **OK**

---

## 2️⃣ Installer httpPlatformHandler

1. Lancer :

   ```
   httpPlatformHandler_amd64.msi
   ```

2. Installer normalement (Next → Finish)

---

## 2️⃣ Installer MySQL

1. Lancer :

```
mysql-installer-community-8.0.35.0.msi
```

<details>
<summary>📷 Capture écran</summary>

![img](img/MYSQL_1.png)

</details>

#### Setup Type

1. Choisir **Custom** dans **Setup Type**

2. Sélectionner les **produits** suivants :

- ✅ Server
- ✅ Workbench
- ✅ Shell

3. Cliquer **Next → Execute**

4. Choisir : **Server Computer** dans **Type and Networking**

5. Choisir **Use Strong Password Encryption** dans **Authentication**

---

### Configurer root

- User : `root`
- Mot de passe :

  ```
  arp360arp360
  ```

---

### Ajouter un utilisateur

Cliquer **Add User**

- User Name : `arp`
- Host : `localhost`
- Role : `DB Admin`
- Mot de passe :

  ```
  arp360arp360
  ```

Next

---

### Windows Service

- Laisser par défaut
- Next

---

### Server File Permissions

- Laisser :

  ```
  Yes, grant full access […]
  ```

- Cliquer **Execute**
- Puis **Next**
- Décocher :
  - Launch MySQL Workbench
  - Launch MySQL Shell

- Cliquer **Finish**

---

# 3️⃣ Installer Python 3.9

Lancer :

```
python-3.9.1-amd64.exe
```

### IMPORTANT

✅ Cocher :

```
Add Python 3.9 to PATH
```

<details>
<summary>📷 Capture écran</summary>

![img](img/PYTHON_1.png)

</details>

Puis cliquer :

```
Install Now
```

À la fin :

- Cliquer sur **Disable Path Limit** si proposé

---

# 4️⃣ Donner les droits IIS sur Python

⚠️ Obligatoire si Python est installé en mode utilisateur.

1. Appuyer sur `Windows + R`
2. Taper

```
%localappdata%\Programs\Python
```

<details>
    <summary>📷 Capture écran</summary>
       
![img](img/IIS_IUSRS_1.png)

</details>

3. Clic droit sur **Python39**
4. Propriétés → Sécurité → Modifier → Ajouter
5. Cliquer sur **Emplacements...**
6. Sélectionner l'élément le plus haut et cliquer sur **OK**
   <details>
    <summary>📷 Capture écran</summary>

   ![img](img/IIS_IUSRS_4.png)

    </details>

7. Dans "Entrez les noms…", taper :

```
IIS_IUSRS
```

8. Cliquer sur **Vérifier les noms**
   <details>
    <summary>📷 Capture écran</summary>
       
    ![img](img/IIS_IUSRS_6.png)

    </details>

9. Cliquer sur **OK**

---

# 5️⃣ NSSM

Copier `nssm.exe` dans :

```
C:\nssm\
```

(Créer le dossier si nécessaire)

Vérifier :

```
C:\nssm\nssm.exe
```

---

# 6️⃣ Vérifications rapides

Dans PowerShell :

```bash
python --version
```

→ Doit afficher **Python 3.9.x**

```bash
mysql --version
```

→ Doit afficher version 8.0.x

---
