# CLI

Purgecss is available via a CLI. You can use the CLI by itself or with a configuration file.

## Installation

```
npm i -g purgecss
```

## Usage

To see the available options for the CLI: `purgecss --help`

```
purgecss --css <css> --content <content> [option]

Options:
  --con, --content  glob of content files                                [array]
  -c, --config      configuration file                                  [string]
  -o, --out         Filepath directory to write purified css files to   [string]
  -w, --whitelist   List of classes that should not be removed
                                                           [array] [default: []]
  -h, --help        Show help                                          [boolean]
  -v, --version     Show version number                                [boolean]
```



