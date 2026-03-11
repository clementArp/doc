# Ajouter de la documentation

La documentation ce situe dans:

``doc/docs``


# Mettre à jour le site avec les dernières modifications

**Note:** Nécessite Python 3.9.x ainsi qu’un accès à Internet

````
py -m venv venv

./venv/Scripts/activate

pip install -r ./requirement.txt

cd doc

mkdocs build
``````