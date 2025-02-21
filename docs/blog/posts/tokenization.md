---
Author: Abdel-aziz Harane
date: 2025-02-19
categories:
  - Tokenization
  - Preprocessing
cover_image: ../../assets/API.png
---

<img src="../../assets/AbdelH.png" alt="Author Image" style="border-radius: 50%; width: 100px; height: 100px;">

## Tokenization

Dans le cadre de ce projet, nous avons appliqué **trois principaux algorithmes** de tokenization.
Chacun présente des avantages et des inconvénients, nous permettant d'explorer et de mieux comprendre le fonctionnement de la tokenization, notamment pour la langue arabe tchadienne (shu).

<!-- Lire plus -->

Nous allons d'abord expliquer ce qu'est la tokenization, pourquoi elle est importante et comment elle fonctionne, avant de découvrir ensemble les trois méthodes que nous avons utilisées.

??? info "Qu'est-ce qu'un tokenizer ?"

    Pour apprendre à un ordinateur à lire et comprendre une phrase, nous devons à priori numériser ces mots (vectorisation) pour qu'il puisse comprendre. Pour la machine, il est impossible de comprendre les mots brutes sans les faire passer par une moulette. C'est-à-dire une machine ne comprend que 1 et 0 et pour elle, une phrase est juste une suite de lettres collées les unes aux autres. Elle a donc besoin d'un outil pour découper la phrase en petits morceaux compréhensibles et numériques. Ce découpage s'appelle la **tokenization** et **l'encodage** lorsque cette phrase est vectorisée comme `[129, 103, 192]`.

Par exemple, la phrase :

```text title="une phrase en shu"
**"Zahra indaha khalag asfar"**
Peut être transformée en :

- `"Zahra"`
- `"indaha"`
- `"khalag"`
- `"asfar"`
```

Ces morceaux sont appelés des **tokens**, et l'ordinateur peut maintenant travailler avec eux plus facilement.

!!! note "Les langues tchadiennes et la tokenization"

      Les langues tchadiennes, comme l'arabe tchadien et le ngambaye, présentent des défis uniques en tokenization. L'arabe tchadien, par exemple, utilise une écriture attachée et des mots qui peuvent être très longs lorsqu'ils contiennent des préfixes et suffixes. Il est donc essentiel de tester plusieurs algorithmes et si besoin d'en créer un autre (ce que nous allons faire).

### Les 3 algorithmes les plus utilisés

=== "BPE (Byte Pair Encoding)"

    ??? info "C'est quoi BPE ?"

    Lors qu'on veut apprendre à écrire un texte en utilisant le moins de place possible ou plutôt que de stocker chaque mot individuellement, nous pouvons donc repérer les lettres ou les groupes de lettres les plus fréquents et les remplacer par un symbole plus court.

    ```text title="exemple en shu"
    - Phrase originale : **"Zahra indaha khalag asfar"**
    - Découpage en tokens : **["Za", "hra", "inda", "ha", "kha", "lag", "as", "far"]**
    - Après BPE : **["#A", "inda", "ha", "#B"]** (où #A et #B sont des unités apprises)
    ```

=== "Sentencepiece"

    ??? info "C'est quoi Sentencepiece ?"

    Imagineons que nous avons une phrase et voulons la découper, mais nous ne voulons pas seulement couper aux espaces (car certaines langues n'ont pas d'espaces clairs entre les mots comme le Chinois). Sentencepiece apprend à découper la phrase en morceaux de manière plus flexible.

    ```text title="exemple en shu"
    - Phrase originale : **"Al-naadum da gaa'id fil-beet"**
    - Tokenization avec SentencePiece : **["Al-", "naadum", "da", "gaa'id", "fil-", "beet"]**
    - SentencePiece peut aussi découper : **["Al", "na", "adum", "da", "gaa'", "id", "fil", "beet"]** pour plus de flexibilité.
    ```

=== "Wordpiece"

    ??? info "C'est quoi WordPiece ?"

    WordPiece est un algorithme qui coupe une phrase en sous-unités, en favorisant les segments les plus fréquemment rencontrés dans les données d'entraînement. Cette approche est utilisée dans des modèles comme BERT.

    ```r title="exemple en shu"
    - Phrase originale : **"Zahra indaha khalag asfar"**
    - Tokenization avec WordPiece : **["Zah", "##ra", "inda", "##ha", "khal", "##ag", "as", "##far"]**
    ```

    Cela permet de garder des unités fréquentes tout en fragmentant les mots moins courants.

Ces trois méthodes nous ont permit de mieux adapter la tokenization en créant notre propre `tokenizer` sur le vocabulaire de l'arabe tchadienne.
Cette approche pourrais être étendue à d'autres langues locales telles que : Sara, Kanembou, Moundang, Zaghawa, ... C'est une première expérimentation et nous l'adapterons à nos autres langues locales.
