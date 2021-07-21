# Titre chapitre 1

Ceci est le chapitre 1 en français.

## Section 1

Ceci est la première section du premièr chapitre.

Voici du `code source Python` :

```python
def build(config, live_server=False, dirty=False):
    """ Perform a full site build. """
    from time import time
    start = time()

    # Run `config` plugin events.
    config = config['plugins'].run_event('config', config)

    # Run `pre_build` plugin events.
    config['plugins'].run_event('pre_build', config=config)
```

## Section 2

Ceci est la deuxième section du premièr chapitre.
