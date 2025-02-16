## Tokenization

Dans le cadre de ce projet, nous avons appliqué `trois (3) principaux algorithmes` de tokenization.
Chacun avec ses avantages et inconvénients, ils nous ont permits d'explorer et de bien connaître ce qui se cache sous le capot de chaun de ces 3 qu'on exploré.

Nous vous proposons ci-dessous leur implémentation complète en utilisant la libraire `Spacy` et `Hugging 🤗`.
Avant de se plonger dans le détail, commençons par comprendre ce quoi la `tokenization`, comment fonctionne-t-il ? A quoi sert ?

??? info "Qu'est-ce que la tokenization ?"

    La tokenization est une méthode nécessaire permettant de segmenter une phrase en mots et les convertir en nombre à travers lequels la machine va apprendre.

!!! note "Les langes tchadiennes"

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

### Les 3 algo les plus utilisés

=== "BPE (Byte Pair Encoding)"

    This is some plain text

=== "SentencePiece"

    * First item
    * Second item
    * Third item

=== "Uni gramm"

    1. First item
    2. Second item
    3. Third item

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
