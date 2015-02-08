# Harpoon
Harpoon is a really easy to use static site deployer.  Currently we support Amazon s3 and BitBalloon, but it's pretty easy to [add integrations if you're interested](/extending-harpoon).

## Installation
To install harpoon just run:

```bash
gem install harpoon
```

## Using Harpoon
Using harpoon is also pretty straight forward, here's a breakdown of the available functions and what they do.

```bash
harpoon help
Commands:
  harpoon deploy          # Deploys the current app
  harpoon doctor          # Check the health of the current deploy strategy
  harpoon help [COMMAND]  # Describe available commands or one specific command
  harpoon init            # Initializes a config file in current directory
  harpoon list            # List available rollbacks
  harpoon rollback        # Rollback to previous release
  harpoon setup           # Setup the current app

Options:
  [--config=CONFIG]
  [--log-level=LOG_LEVEL]
```

## Contributing
We love contributions!  To get involved, hit the [github repo](https://github.com/mazondo/harpoon).
