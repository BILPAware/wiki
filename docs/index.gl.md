# Exemplo S2I MkDocs

Un arquivo `index.md` é obrigatorio para aqueles que non queiran usar o plugin i18n, e por ende, a súa documentación estará en unha lingua soamente. Máis información de como configurar un sitio cunha soa lingua [aquí](https://how-to.docs.cern.ch/advanced/single_language/){target=_blank}.

Para aqueles usuarios que desexen ter un sitio en multiples linguas ou que desexen configurar o seu sitio có plugin i18n, este ficheiro debe ser borrado, xa que a utilización do plugin i18n exise seguir o formato de nomeado de arquivo `nome_arquivo.<lingua>.md`. Vostede pode ver máis información de como configurar un sitio con múltiples linguas [aquí](https://how-to.docs.cern.ch/advanced/multi_language/){target=_blank}.

Máis información de como foi creada esta páxina está dispoñible no [repositorio S2I MkDocs Container GitLab](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-container){target=_blank}.

## Arquivos fonte

Os arquivos fonte deste exemplo poden atoparse [no repositorio MkDocs Example GitLab](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example){target=_blank}.

## Theme

Este exemplo emprega [o theme Material para MkDocs](https://squidfunk.github.io/mkdocs-material/){target=_blank}. Para empregar este theme tan só ten que engadilo no seu ficheiro de configuración de MkDocs ([`mkdocs.yml`](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example/blob/master/mkdocs.yml){target=_blank}):
```yaml
theme:
    name: material
```

Na parte ezquerda atopará a estrutura completa de contidos do sitio. Pola contra, na parte dereita poderá atopar a tabla de contidos da páxina na que actualmente está.

## Multi-linguaxe i18n

Se vostede quere publicar a súa documentación en diferentes idiomas, está á súa disposición o [plugin mkdocs-static-i18n](https://github.com/ultrabug/mkdocs-static-i18n){target=_blank} para este propósito.

Para elo, vostede debe engadir no seu ficheiro de configuración de MkDocs ([`mkdocs.yml`](https://gitlab.cern.ch/authoring/documentation/s2i-mkdocs-example/blob/master/mkdocs.yml){target=_blank}) as linguas que quere empregar da seguinte forma:
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

Ademáis, debe engadir o plugin `i18n` á lista de plugins empregados, xunto coa lingua por defeto e a lista de linguas na que pon a súa documentación dispoñible. Pode [consultar aquí](https://squidfunk.github.io/mkdocs-material/setup/changing-the-language/#configuration){target=_blank} as linguas aceptadas. Á súa vez, pode indicar tamén como quere traducir os títulos das diferentes seccións na parte de navegación:
```yaml
plugins:
  - search
  - i18n:
    default_language: en            # Aquí indícase a lingua por defecto, neste caso o inglés
    languages:
      en: english
      fr: français
      gl: galego
    nav_translations:
      en:                           # Traducción en inglés dos títulos das seccións
        Chapter1: Chapter 1
        Subchapter1: Chapter 1.1
        Subchapter1a: Chapter 1.1.1
        Chapter2: Chapter 2
        Interesting links: Links to resources
      fr:                           # Traducción en francés dos títulos das seccións
        Chapter1: Chapitre 1
        Subchapter1: Chapitre 1.1
        Subchapter1a: Chapitre 1.1.1
        Chapter2: Chapitre 2
        Interesting links: Liens vers des ressources
      gl:                           # <= VOSTEDE ESTÁ AQUÍ AGORA
        Chapter1: Capítulo 1        # Traducción en galego dos títulos das seccións 
        Subchapter1: Capítulo 1.1
        Subchapter1a: Capítulo 1.1.1
        Chapter2: Capítulo 2
        Interesting links: Links a fontes
```

Por outra banda, é importante que todos os seus ficheiros estén correctamente nomeados có formato `<nome_ficheiro>.<lingua>.md` para que cada un sexa ubicado na lingua correcta. Vostede pode apreciar que este exemplo contén un arquivo `index.md` que se emprega para ilustrar o caso de que un usuario non queira empregar o plugin i18n, e por ende, a súa documentación estará nunha soa lingua. **Se vostede quere desplegar un sitio con multiples linguas, por favor, ignore este arquivo**.

**IMPORTANTE**: debe darse de conta de que as chaves das tuplas do mapa do ficheiro de configuración MkDocs `mkdocs.yml` é o nome da carpeta que contén os seus ficheiros na carpeta `docs` (Chapter_1, Subchapter1a, etc.). Este mapping é sensíbel ás maiúsculas e ás minúsculas e ten que comezar sempre por maiúsculas incluso se a carpeta comeza por minúsculas coma neste exemplo. Ademáis, os guións baixos `_` nos nomes das carpetas son traducidos en espacios no mapeo do `mkdos.yml` (pode ver o examplo de `interesting_links` como nome da carpeta e `Interesting links: Links a fontes` como mapeo no `mkdos.yml`). É obrigatorio seguir esta convención xa que pola contra, se non se fai, os títulos da navegación non será traducidos.
