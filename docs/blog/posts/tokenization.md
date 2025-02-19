---
Autor: Abdel-aziz Harane
date:
  created: 2025-02-19
categories:
  - Tokenization
  - Preprocessing
title: Tokenization
---

## Tokenization

Dans le cadre de ce projet, nous avons appliqué **trois principaux algorithmes** de tokenization.
Chacun présente des avantages et des inconvénients, nous permettant d'explorer et de mieux comprendre le fonctionnement de la tokenization, notamment pour la langue arabe tchadienne.

Nous allons d'abord expliquer ce qu'est la tokenization, pourquoi elle est importante et comment elle fonctionne, avant de découvrir ensemble les trois méthodes que nous avons utilisées.

??? info "Qu'est-ce qu'un tokenizer ?"

    Imagine que tu veux apprendre à un ordinateur à lire et comprendre une phrase. Mais pour lui, une phrase est juste une suite de lettres collées les unes aux autres. Il a donc besoin d'un outil pour découper la phrase en petits morceaux compréhensibles. Ce découpage s'appelle la **tokenization**.

    Par exemple, la phrase :

    **"الولد يلعب بالكرة"** (Le garçon joue avec le ballon)

    Peut être transformée en :

    - **"الولد"** (le garçon)
    - **"يلعب"** (joue)
    - **"بالكرة"** (avec le ballon)

    Ces morceaux sont appelés des **tokens**, et l'ordinateur peut maintenant travailler avec eux plus facilement.

!!! note "Les langues tchadiennes et la tokenization"

    Les langues tchadiennes, comme l'arabe tchadien et le ngambaye, présentent des défis uniques en tokenization. L'arabe tchadien, par exemple, utilise une écriture attachée et des mots qui peuvent être très longs lorsqu'ils contiennent des préfixes et suffixes. Il est donc essentiel d'utiliser des algorithmes adaptés à ces spécificités.

### Les 3 algorithmes les plus utilisés

=== "BPE (Byte Pair Encoding)"

    ??? info "C'est quoi BPE ?"

        Imagine que tu veux apprendre à écrire un texte en utilisant le moins de place possible. Plutôt que de stocker chaque mot individuellement, tu peux repérer les lettres ou les groupes de lettres les plus fréquents et les remplacer par un symbole plus court.

        Par exemple, dans **"الولد يلعب بالكرة"**, si on remarque que **"ال"** revient souvent, on peut le remplacer par un seul symbole. Ainsi, l'ordinateur aura moins de morceaux à gérer.

    **Exemple en arabe tchadien :**
    - Phrase originale : **"الولد يلعب بالكرة"**
    - Découpage en tokens : **["ال", "ولد", "يلعب", "بال", "كرة"]**
    - Après BPE : **["#A", "ولد", "#B", "كرة"]** (où #A et #B sont des unités apprises)

=== "SentencePiece"

    ??? info "C'est quoi SentencePiece ?"

        Imagine que tu as une phrase et que tu veux la découper, mais tu ne veux pas seulement couper aux espaces (car certaines langues n'ont pas d'espaces clairs entre les mots). SentencePiece apprend à découper la phrase en morceaux de manière plus flexible.

    **Exemple en arabe tchadien :**
    - Phrase originale : **"أنا أدرس في الجامعة"** (Je fais mes études à l’université)
    - Tokenization avec SentencePiece : **["أنا", "أدرس", "في", "الجامعة"]**
    - SentencePiece peut aussi découper : **["أنا", "أ", "درس", "في", "ال", "جامعة"]** pour plus de flexibilité.

=== "Unigram"

    ??? info "C'est quoi Unigram ?"

        Imagine que tu veux découper une phrase en morceaux, mais au lieu de toujours prendre les mêmes morceaux, tu regardes quelles parties sont les plus utiles statistiquement. Tu essayes plusieurs options et tu choisis celle qui minimise le nombre total de morceaux tout en gardant du sens.

    **Exemple en arabe tchadien :**
    - Phrase originale : **"الأطفال يلعبون في الحديقة"** (Les enfants jouent dans le jardin)
    - Tokenization avec Unigram : **["الأطفال", "يلعبون", "في", "الحديقة"]**
    - Mais il pourrait aussi décider de : **["الأ", "طفال", "يلعبون", "في", "الحديقة"]** si cela est plus efficace.

---

Ces trois méthodes nous ont permit de mieux adapter la tokenization en créant notre propre tokenizer sur le vocabulaire de l'arabe tchadienne.
\_Cette approche pourrais être étendue à d'autres langues locales telles que : Sara, Kanembou, Moundang, Zaghawa, ... C'est une première expérimentation et nous l'adapterons à nos autres langues locales.

Ci-dessous les scripts pour chaque algo en R et python

### Code Blocks in Content Tabs

=== "Python"

    ```py
    def main():
        print("Hello world!")

    if __name__ == "__main__":
        main()
    ```

=== "R"

    ```js
    function main() {
        console.log("Hello world!");
    }

    main();
    ```
