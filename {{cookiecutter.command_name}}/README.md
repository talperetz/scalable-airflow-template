
#Python CLI Template
This template uses
<p align="center">
  <a href="https://typer.tiangolo.com"><img src="https://typer.tiangolo.com/img/logo-margin/logo-margin-vector.svg" alt="Typer"></a>
</p>
<p align="center">
    <em>Typer, build great CLIs. Easy to code. Based on Python type hints.</em>
</p>
---

**Documentation**: <a href="https://typer.tiangolo.com" target="_blank">https://typer.tiangolo.com</a>

**Github Repo**: <a href="https://github.com/tiangolo/typer" target="_blank">https://github.com/tiangolo/typer</a>

---

# Features

* **Short & Easy**: Minimize code duplication. Multiple features from each parameter declaration. Fewer bugs.
* **Docker-Ready**: Dockerfile included, with one make command you can build and deploy it to ecr.
* **Comes With Pre-made Commands**: Available Make commands to build, deploy and clean the images.  


## Installation

```console
$ cookiecutter https://github.com/talperetz/python-cli-template
```

```console
$ pip install -r requirements.txt
```

## Usage

1. Edit [command_name].py file to execute your desired commands
2. make build
3. make ecrpush 

### Run it

Run your application:


```console
// Run your application
$ python [command_name].py

// You get a nice error, you are missing NAME
Usage: main.py [OPTIONS] NAME
Try "main.py --help" for help.

Error: Missing argument "NAME".

// You get a --help for free
$ python main.py --help

Usage: [command_name].py [OPTIONS] NAME

Options:
  --install-completion  Install completion for the current shell.
  --show-completion     Show completion for the current shell, to copy it or customize the installation.
  --help                Show this message and exit.

// You get ✨ auto completion ✨ for free, installed with --install-completion

// Now pass the NAME argument
$ python [command_name].py Camila

Hello Camila

// It works! 🎉
```

## Optional Dependencies

Typer uses <a href="https://click.palletsprojects.com/" class="external-link" target="_blank">Click</a> internally. That's the only dependency.

But you can also install extras:

* <a href="https://pypi.org/project/colorama/" class="external-link" target="_blank"><code>colorama</code></a>: and Click will automatically use it to make sure your terminal's colors always work correctly, even in Windows.
    * Then you can use any tool you want to output your terminal's colors in all the systems, including the integrated `typer.style()` and `typer.secho()` (provided by Click).
    * Or any other tool, e.g. <a href="https://pypi.org/project/wasabi/" class="external-link" target="_blank"><code>wasabi</code></a>, <a href="https://github.com/erikrose/blessings" class="external-link" target="_blank"><code>blessings</code></a>.
* <a href="https://github.com/click-contrib/click-completion" class="external-link" target="_blank"><code>click-completion</code></a>: and Typer will automatically configure it to provide completion for all the shells, including installation commands.

You can install `typer` with `colorama` and `click-completion` with `pip install typer[all]`.

## Other tools and plug-ins

Click has many plug-ins available that you can use. And there are many tools that help with command line applications that you can use as well, even if they are not related to Typer or Click.

For example:

* <a href="https://github.com/click-contrib/click-spinner" class="external-link" target="_blank"><code>click-spinner</code></a>: to show the user that you are loading data. A Click plug-in.
    * There are several other Click plug-ins at <a href="https://github.com/click-contrib" class="external-link" target="_blank">click-contrib</a> that you can explore.
* <a href="https://pypi.org/project/tabulate/" class="external-link" target="_blank"><code>tabulate</code></a>: to automatically display tabular data nicely. Independent of Click or typer.
* etc... you can re-use many of the great available tools for building CLIs.
