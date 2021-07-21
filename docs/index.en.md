# S2I MkDocs Example

An `index.md` file is mandatory for those who don't want to use the plugin i18n, and hence their documentation will be in one language. More information on how to configure a single language site [here](https://how-to.docs.cern.ch/advanced/single_language/){target=_blank}.

For those who want to have multilanguage sites or simply want to configure their single language sites through the i18n plugin, this file has to be removed, since the use of the i18n plugin requires following the file name convection `filename.<language>.md`. You can see more information on how to configure a multilanguage site [here](https://how-to.docs.cern.ch/advanced/multi_language/){target=_blank}.

More information on how this page was created is available at [S2I MkDocs Container GitLab repository](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-container){target=_blank}.

## Source files

The source files for this example can be found in the [MkDocs Example GitLab repository](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example){target=_blank}.

## Theme

This example is using the [Material theme for MkDocs](https://squidfunk.github.io/mkdocs-material/){target=_blank}. To use this theme yourself all you have to do is add the following in your MkDocs configuration file ([`mkdocs.yml`](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example/blob/master/mkdocs.yml){target=_blank}):
```yaml
theme:
    name: material
```

On your left you'll find the content structure of the entire site and on your right the table of conents of this specific page.

## Multi-language support i18n

It is possible to publish your documentation in different languages using the [plugin mkdocs-static-i18n](https://github.com/ultrabug/mkdocs-static-i18n){target=_blank}.

You have to add into your MkDocs configuration file ([`mkdocs.yml`](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example/blob/master/mkdocs.yml){target=_blank}) the languages that you want to make your documentation available.
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

Furthermore, you have to add the plugin `i18n` to the list of plugins used, along with the default language and the list of languages that your documentation is available. You can [check the available languages here](https://squidfunk.github.io/mkdocs-material/setup/changing-the-language/#configuration){target=_blank}. In addition, it is possible to translate section titles in the navigation:
```yaml
plugins:
  - search
  - i18n:
    default_language: en          # Here you specify the default language, English in this example
    languages:
      en: english
      fr: français
      gl: galego
    nav_translations:
      en:                          # <= YOU ARE HERE
        Chapter1: Chapter 1        # Translate section titles into English
        Subchapter1: Chapter 1.1
        Subchapter1a: Chapter 1.1.1
        Chapter2: Chapter 2
        Interesting links: Links to resources
      fr:                           # Translate section titles into French
        Chapter1: Chapitre 1
        Subchapter1: Chapitre 1.1
        Subchapter1a: Chapitre 1.1.1
        Chapter2: Chapitre 2
        Interesting links: Liens vers des ressources
      gl:                           # Translate section titles into Galician
        Chapter1: Capítulo 1
        Subchapter1: Capítulo 1.1
        Subchapter1a: Capítulo 1.1.1
        Chapter2: Capítulo 2
        Interesting links: Links a fontes
```

Notice that all your files have to follow the naming format `<file_name>.<language>.md` in order to place them on the correct language page. You can see that this example contains a file `index.md`, which is used to illustrate the cases for those who don't want to use the plugin i18n, and hence their documentation will be in one language. **If you want to deploy a multilanguage site please, remove this file**.

**IMPORTANT**: Notice that the key of the sections mapping tuples of the MkDocs configuration file `mkdocs.yml` is the name of the folder that contains your files inside the `docs` folder (Chapter1, Subchapter1a, etc.). This mapping is case sensitive and always starts with a capital letter, even if the folder name does not as in this example. Also, underscore `_` on folder's name are translated into spaces on `mkdocs.yml` mapping (see the example `interesting_links` as the name of the folder and `Interesting links: Links to resources` on the `mkdocs.yml`). It is mandatory to follow this convention, otherwise, the nav title will not be translated.
