# S2I Exemple MkDocs

Un fichier `index.md` est obligatoire pour ceux qui ne veulent pas utiliser le plugin i18n, et donc leur documentation sera dans une seule langue. Plus d'informations sur la configuration d'un site en une seule langue [ici](https://how-to.docs.cern.ch/advanced/single_language/){target=_blank}.

Pour ceux qui souhaitent avoir des sites multilingues ou qui souhaitent simplement configurer leurs sites monolingues via le plugin i18n, ce fichier doit être supprimé, car l'utilisation du plugin i18n nécessite de suivre le nom de fichier convection `nom_fichier.<langue>.md `. Vous pouvez voir plus d'informations sur la façon de configurer un site multilingue [ici] (https://how-to.docs.cern.ch/advanced/multi_language/){target=_blank}.

Plus d'informations sur la création de cette page sont disponibles sur le [repo S2I MkDocs Container GitLab](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-container){target=_blank}.

## Fichiers source

Les fichiers source de cet exemple se trouvent dans le [repo MkDocs Example GitLab](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example){target=_blank}.

## Thème

Cet exemple utilise le [thème Material for MkDocs](https://squidfunk.github.io/mkdocs-material/){target=_blank}. Pour utiliser vous-même ce thème, il vous suffit d'ajouter ce qui suit dans votre fichier de configuration MkDocs ([`mkdocs.yml`](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example/blob/master/mkdocs.yml){target=_blank}):
```yaml
theme:
    name: material
```

Sur votre gauche, vous trouverez la structure du contenu de l'ensemble du site et sur votre droite le table des matières de cette page spécifique.

## I18n multilingue

Il est possible de publier votre documentation dans différentes langues en utilisant le [plugin mkdocs-static-i18n](https://github.com/ultrabug/mkdocs-static-i18n){target=_blank}.

Vous devez ajouter dans votre fichier de configuration MkDocs ([`mkdocs.yml`](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example/blob/master/mkdocs.yml){target=_blank}) les langues dans lesquelles vous souhaitez rendre votre documentation disponible.
```yaml
extra:
  alternate:
    - name: English
      link: ./
      lang: en
    - name: Français
      link: ./fr/
      lang: fr
    - name: Galego
      link: ./gl/
      lang: gl
```

De plus, vous devez ajouter le plugin `i18n` à la liste des plugins utilisés, ainsi que la langue par défaut et la liste des langues dans lesquelles votre documentation est disponible. Vous pouvez [regarder les langues disponibles ici](https://squidfunk.github.io/mkdocs-material/setup/changing-the-language/#configuration){target=_blank}. Il est possible de traduire les titres des sections dans la navigation aussi:
```yaml
plugins:
  - search
  - i18n:
    default_language: en            # Ici, vous spécifiez la langue par défaut, l'anglais dans cet exemple
    languages:
      en: english
      fr: français
      gl: galego
    nav_translations:
      en:                           # Traduire les titres de section en anglais
        Chapter1: Chapter 1
        Subchapter1: Chapter 1.1
        Subchapter1a: Chapter 1.1.1
        Chapter2: Chapter 2
        Interesting links: Links to resources
      fr:                          # <= VOUS ÊTES ICI MAINTENANT
        Chapter1: Chapitre 1       # Traduire les titres de section en français
        Subchapter1: Chapitre 1.1
        Subchapter1a: Chapitre 1.1.1
        Chapter2: Chapitre 2
        Interesting links: Liens vers des ressources
      gl:                           # Traduire les titres de section en galicien
        Chapter1: Capítulo 1
        Subchapter1: Capítulo 1.1
        Subchapter1a: Capítulo 1.1.1
        Chapter2: Capítulo 2
        Interesting links: Links a fontes
```

Notez que tous vos fichiers doivent suivre le format de dénomination `<nom_de_fichier>.<langue>.md` afin de les placer sur la bonne page de langue. Vous pouvez voir que cet exemple contient un fichier `index.md`, qui est utilisé pour illustrer les cas pour ceux qui ne veulent pas utiliser le plugin i18n, et donc leur documentation sera dans une langue. **Si vous souhaitez déployer un site multilingue s'il vous plaît, supprimez ce fichier**. 

**IMPORTANT** : Notez que la clé des tuples de mappage des sections du fichier de configuration MkDocs `mkdocs.yml` est le nom du folder qui contient vos fichiers dans le folder `docs` (Chapter1, Subchapter1a, etc.). Ce mappage est sensible à la casse et commence toujours par une majuscule, même si le nom du folder n'est pas comme dans cet exemple. De plus, les traits de soulignement `_` sur le nom du folder sont traduits en espaces sur le mappage `mkdocs.yml` (voir l'exemple `interesting_links` comme le nom du folder et `Interesting links: Liens vers des ressources` sur le `mkdocs.yml`). Il est obligatoire de suivre cette convention, sinon, le titre de navigation ne sera pas traduit.
