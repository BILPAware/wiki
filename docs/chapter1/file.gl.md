# Título capítulo 1

Este é o primeiro capítulo en galego.

## Sección 1

Esta é a primeira sección do primeiro capítulo.

Aquí temos `código fonte Python`:

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

## Sección 2

Esta é a segunda sección do primeiro capítulo.
