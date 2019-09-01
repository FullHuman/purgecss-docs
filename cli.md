# CLI

PurgeCSS is available via a CLI. You can use the CLI by itself or with a configuration file.

## Installation

```text
npm i -g purgecss
```

## Usage

To see the available options for the CLI: `purgecss --help`

```text
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

The options available through the CLI are similar to the ones available with a configuration file. You can also use the CLI with a configuration file.

### --css

```text
purgecss --css css/app.css css/palette.css --content src/index.html
```

### --content

You can specify content that should be analyzed by PurgeCSS with an array of filenames or [globs](https://github.com/isaacs/node-glob/blob/master/README.md#glob-primer). These files can be HTML, Pug, Blade, etc.

```text
purgecss --css css/app.css --content src/index.html src/**/*.js
```

### --config

You can use the CLI with a [configuration file](configuration.md). Use `--config` or `-c` with the path to the config file.

```text
purgecss --config ./purgecss.config.js
```

### --out

By default, the CLI outputs the result in the console. If you wish to return the CSS as files, specify the directory to write the purified CSS files to.

```text
purgecss --css css/app.css --content src/index.html src/**/*.js --out build/css/
```

### --whitelist

If you wish to prevent PurgeCSS from removing a specific CSS selector, you can whitelist it.

```text
purgecss --css css/app.css --content src/index.html --whitelist classnameToWhitelist
```

## Example

You can see an example [here](https://github.com/FullHuman/purgecss/tree/master/examples/cli/config-file).

