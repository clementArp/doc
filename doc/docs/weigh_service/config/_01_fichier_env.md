[< Retour](index.md)

# Configuration du .env


## Sommaire

- [Modifier le .env](#modifier-le-env)
---

# Modifier le .env

Une partie de la configuration du projet s'effectue dans le ficher `.env`

Chemin du fichier :
```
C:\arp_weigh_service\
 └── .env
```

Le `slot` et l'`IP` du PLC.
```
PLC_IP=10.0.36.20
SLOT=0
```

**Note :** Il est important de doubler les backslashes (`\`) dans les chemins.

Chemin des structures dans le PLC, contenant les variables à lire / écrire
```
PATH_READ_CYC="Application.GVL_R5.g_stR5Out"
PATH_READ_STATS="Application.GVL_R6.g_stR6Out"

PATH_WRITE_CYC="Application.GVL_R5.g_stR5In"
PATH_WRITE_STATS="Application.GVL_R6.g_stR6In"
```

Chemin du dossier où `arp_weigh_service` est installé :
```
WORKDIR="C:\\arp_weigh_service"
```

Chemin du dossier où la base de données sera créée :
```
DATABASE_DIR="C:\\arp_weigh_service\\database"
```

Chemin du dossier où les fichiers de pesage seront créés :
```
FILES_DIR="C:\\arp_weigh_service\\files"
```

Exemple de configuration complète :

```env
PLC_IP=10.0.36.20
SLOT=0

# Nom de la structure PLC contenant les variables cycliques et statistiques à lire
PATH_READ_CYC="Application.GVL_R5.g_stR5Out"
PATH_READ_STATS="Application.GVL_R6.g_stR6Out"

# Nom de la structure PLC contenant les variables à écrire
PATH_WRITE_CYC="Application.GVL_R5.g_stR5In"
PATH_WRITE_STATS="Application.GVL_R6.g_stR6In"

# LES CHEMINS SUIVANTS DOIVENT PARTIR DE LA RACINE DU DISQUE

# Attention : doubler les backslash
WORKDIR="C:\\arp_weigh_service"

# Le dossier où la base de données sera créée
DATABASE_DIR="C:\\arp_weigh_service\\database"

# Le dossier où les fichiers des données cycliques seront créés
FILES_DIR="C:\\arp_weigh_service\\files"
```

### Important:
Les dossiers suivants n'ont pas d'emplacement par défaut et doivent donc être créés **manuellement** à l'emplacement souhaité :

- `files`
- `database`

pour l'exemple ci dessus, l'architecture est donc :
```
C:\arp_weigh_service\
    ├── database\
    ├── files\
```







