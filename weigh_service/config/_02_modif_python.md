[< Retour](index.md)

# Configuration dans les fichiers python

**Note :** Les variables notées en majuscules sont des variables globales et/ou d'environnement.

Par exemple :
`PATH_READ_CYC` et `PATH_WRITE_CYC` correspondent aux chemins définis dans le fichier `.env`.

## Sommaire

- [Modifier les variables lues](#modifier-les-variables-lues)
- [Modifier les variables écrites](#modifier-les-variables-écrites)

---

# Modifier les variables lues

Ouvrir le fichier `app_weighing_eip.py`:

Chemin du fichier :
```
C:\arp_weigh_service
└── com\
    └── main\
        └── com\
            ├── app_weighing_eip.py
```

Puis se rendre dans la fonction `def _cfg(self):`

Les variables `self.cfg_cyclic_data` et `self.cfg_stats_data` contiennent les valeurs lues.

Chaque structure a la forme suivante :
- `{"dbName": "X", "colFile":"X", "dbType": X, "var" : X"}`

Correspond à une variable à lire, telle que :

- `dbName` : le nom de la colonne dans la base de données
- `colFile` : le nom de la colonne dans le fichier CSV qui sera créé
- `dbType` : le type de la variable (`TEXT`, `REAL` ou `INTEGER`)
- `var` : le nom de la variable dans le programme

Si la variable à lire est un tableau, il faut ajouter une structure correspondante dans les paramètres de `self._config_var_array()`.

Exemple d'ajout de variable à lire
```python
self.cfg_cyclic_data = [
    {"dbName": "NomDansBDD", "colFile": "NomDansFichier", "dbType": DatabaseType.INTEGER, "var":f"{PATH_READ_CYC}.MaVariableALire"},
]
```

---

# Modifier les variables écrites

Ouvrir le fichier `app_weighing_eip.py`:

Chemin du fichier :
```
C:\arp_weigh_service
└── com\
    └── main\
        └── com\
            ├── app_weighing_eip.py
```

Puis se rendre dans la fonction `def _nodes(self):`

Ajouter la variable a lire dans la variable `write_vars`
Exemple :
```python
write_vars = [
    f"{PATH_WRITE_CYC}.MaVariableAEcrireDansLePLC",
]
```

---