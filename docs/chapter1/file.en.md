# Title chapter 1

This is the first chapter in English.

## Section 1

This is the first section in the first chapter

Here is some `Python source code`:

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

This is the second section in the first chapter
