---
Autor: Abdel-aziz Harane
date:
  created: 2025-02-20
categories:
  - Data collection
  - Python
  - R
---

# Collecte et traitement des données pour SHU avec R et Python

Dans un projet NLP, la phase la plus complexe est la collecte et le traitement des données. Pour ce projet, c'est un défi majeur (qui m'a pris 4 mois), notamment en raison du manque de ressources structurées et de la diversité des formats de données. Dans cet article, nous allons aborder **les différentes étapes et défis liés à l’extraction, la transformation et la structuration des données linguistiques** obtenues à partir de sources variées (textes religieux, vocabulaires, grammaires) en utilisant **R et Python**.

J'espère qu'il vous s'avérera utile.
Il y a beaucoup de choses à discuter ici du côté pratique de cette collecte mais j'essayerai d'être plus précis en vous fournissant que les nécessaires.

#### Les points abordés dans cet article :

- `Scraping avec le package rvest de R`: Extraction de textes de la Bible en arabe tchadien (shu)
- `Extraction de textes depuis des PDF`: Pourquoi l’OCR pose problème sur certains documents anciens et mal structurés
- `Nettoyage et prétraitement des données`: Techniques pour normaliser et améliorer la qualité des textes extraits
- `Structuration et tokenization des données`: Transformation des données pour une meilleure exploitation en NLP
- `Export et intégration des données`: Formats adaptés pour entraîner des modèles NLP

### 1. Scraping avec R et `rvest`

Une grande partie des textes disponibles en langues tchadiennes sont dispersés sur des sites non structurés. Le package **rvest** permet d’extraire ces textes efficacement.

```r title="scraping_shu.r" linenums="1"
library(rvest)

url <- "https://bible.com/arabe-tchadien"
page <- read_html(url)

textes <- page %>%
  html_nodes("p") %>%  # Sélectionne les paragraphes contenant du texte
  html_text()

writeLines(textes, "bible_arabe_tchadien.txt")
```

#### Défi rencontré :

- Certains sites affichent du texte en JavaScript, ce qui rend l’extraction plus complexe.
- Les chapitres et versets sont parfois imbriqués dans des balises non standardisées.

**Solutions possibles :**

- Utilisation de Selenium pour exécuter le JavaScript avant d’extraire les données.
- Extraction et nettoyage des balises avec des expressions régulières.

### 2. Extraction de textes depuis des PDF

Les PDF contenant des documents en langues tchadiennes sont souvent **anciens et mal structurés**. Même les outils OCR comme `tesseract` rencontrent des difficultés.

#### Problèmes observés :

- Mauvaise segmentation des caractères (ex : "b'Allah" devient "b Allah").
- Perte d’information due à des polices de caractères non standardisées.
- Disposition des colonnes non uniforme, ce qui fausse l’extraction.

```python title="ocr_extractionPDF.py" linenums="1"
import pytesseract
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf")

for i, page in enumerate(pages):
    text = pytesseract.image_to_string(page, lang='ara')
    with open(f"output_{i}.txt", "w", encoding="utf-8") as f:
        f.write(text)
```

#### Solutions et améliorations :

- Utiliser **pdfminer.six** pour extraire directement le texte au lieu de l'OCR si la couche texte est présente.
- **Segmenter les colonnes manuellement** pour reconstruire des phrases cohérentes.
- Convertir les documents en **format HTML** avant de les traiter pour un alignement plus précis.

### 3. Nettoyage et prétraitement des données

Une fois les données extraites, elles nécessitent un prétraitement rigoureux avant d’être utilisées pour le NLP.

#### Étapes principales :

- **Normalisation des caractères** (suppression des accents, homogénéisation de l’écriture des mots).
- **Correction des erreurs OCR** avec des dictionnaires de mots.
- **Segmentation des phrases et tokenization**.

Exemple de nettoyage en Python :

```python
import re

def clean_text(text):
    text = text.lower()
    text = re.sub(r"[^a-zA-Z0-9\s]", "", text)  # Supprime les caractères spéciaux
    return text

text_cleaned = clean_text("Allâh est mis en forme étrangement !")
print(text_cleaned)  # 'allah est mis en forme etrangement'
```

Code APE vrai labelisé par le moteur de règles – nace (732 modalités)
Prétraitements standards :

- Passage en minuscules
- Suppression de la ponctuation, des nombres et des stop words et la racinisation (stemming)

### 4. Structuration et tokenization des données

Pour rendre les données exploitables par un modèle NLP, nous devons structurer les textes et segmenter les mots de manière efficace.

#### Approche en R :

```r
library(tokenizers)

texte <- "Allah est grand et miséricordieux"
tokens <- tokenize_words(texte)
print(tokens)
```

#### Défi :

- Certains mots en langues tchadiennes sont **concaténés** et difficiles à segmenter sans un lexique adapté.
- Certaines langues utilisent **des déclinaisons riches**, rendant la tokenization plus complexe.

**Solutions possibles :**

- Développer un tokenizer spécifique en utilisant un **modèle statistique basé sur les fréquences des mots**.
- Entraîner un **modèle de segmentation de mots** en deep learning pour affiner la tokenization.
