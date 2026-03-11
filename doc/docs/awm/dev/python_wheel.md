Voici comment **pré-télécharger toutes les dépendances Python sous forme de wheels** sur une machine qui a Internet, puis de les réutiliser sur les machines hors ligne.

Le plus simple est de créer un dossier du type `wheelhouse/`.

### Machine avec Internet

```bash
python -m venv venv
source venv/bin/activate
python -m pip install --upgrade pip setuptools wheel
mkdir wheelhouse
python -m pip download -r requirements.txt -d wheelhouse
python -m pip wheel -r requirements.txt -w wheelhouse
```

### Machine sans Internet

```bash
python -m venv venv
venv\Scripts\activate
python -m pip install --no-index --find-links=wheelhouse -r requirements.txt
```
