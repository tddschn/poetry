---
title: "Introduction"
draft: false
type: docs
layout: "single"

menu:
  docs:
    weight: 0
---

# Introduction

Poetry is a tool for **dependency management** and **packaging** in Python.
It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.
Poetry offers a lockfile to ensure repeatable installs, and can build your project for distribution.


## System requirements

Poetry requires **Python 3.7+**. It is multi-platform and the goal is to make it work equally well
on Linux, macOS and Windows.

## Installation

{{% note %}}
If you are viewing documentation for the development branch, you may wish to install a preview or development version of Poetry.
See the **advanced** installation instructions to use a preview or alternate version of Poetry.
{{% /note %}}

{{< tabs tabTotal="3" tabID1="installing-with-the-official-installer" tabID2="installing-with-pipx" tabID3="installing-manually" tabName1="With the official installer" tabName2="With pipx" tabName3="Manually (advanced)" >}}

{{< tab tabID="installing-with-the-official-installer" >}}

We provide a custom installer that will install Poetry in a new virtual environment to isolate it
from the rest of your system. This ensures that dependencies will not be accidentally upgraded or
uninstalled, and allows Poetry to manage its own environment.

{{< steps >}}
{{< step >}}
**Install Poetry**

The installer script is available directly at [install.python-poetry.org](https://install.python-poetry.org),
and is developed in [its own repository](https://github.com/python-poetry/install.python-poetry.org).
The script can be executed directly (i.e. 'curl python') or downloaded and then executed from disk
(e.g. in a CI environment).

{{% warning %}}
The previous `get-poetry.py` and `install-poetry.py` installers are deprecated. Any installs performed
using `get-poetry.py` should be uninstalled and reinstalled using `install.python-poetry.org` to ensure
in-place upgrades are possible.
{{% /warning %}}

**Linux, macOS, Windows (WSL)**

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

{{% note %}}
Note: On some systems, `python` may still refer to Python 2 instead of Python 3. We always suggest the
`python3` binary to avoid ambiguity.
{{% /note %}}

**Windows (Powershell)**
```powershell
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
```

{{% note %}}
If you have installed Python through the Microsoft Store, replace `py` with `python` in the command
above.
{{% /note %}}

{{< /step >}}
{{< step >}}
**Install Poetry (advanced)**

By default, Poetry is installed into a platform and user-specific directory:

- `~/Library/Application Support/pypoetry` on MacOS.
- `~/.local/share/pypoetry` on Linux/Unix.
- `%APPDATA%\pypoetry` on Windows.

If you wish to change this, you may define the `$POETRY_HOME` environment variable:

```bash
curl -sSL https://install.python-poetry.org | POETRY_HOME=/etc/poetry python3 -
```

If you want to install prerelease versions, you can do so by passing `--preview` option to `install-poetry.py`
or by using the `$POETRY_PREVIEW` environment variable:

```bash
curl -sSL https://install.python-poetry.org | python3 - --preview
curl -sSL https://install.python-poetry.org | POETRY_PREVIEW=1 python3 -
```

Similarly, if you want to install a specific version, you can use `--version` option or the `$POETRY_VERSION`
environment variable:

```bash
curl -sSL https://install.python-poetry.org | python3 - --version 1.2.0
curl -sSL https://install.python-poetry.org | POETRY_VERSION=1.2.0 python3 -
```

You can also install Poetry from a `git` repository by using the `--git` option:

```bash
curl -sSL https://install.python-poetry.org | python3 - --git https://github.com/python-poetry/poetry.git@master
````
{{< /step >}}
{{< step >}}
**Add Poetry to your PATH**

The installer creates a `poetry` wrapper in a well-known, platform-specific directory:

- `$HOME/.local/bin` on Unix.
- `%APPDATA%\Python\Scripts` on Windows.

If this directory is not present in your `$PATH`, you can add it in order to invoke Poetry
as `poetry`.

Alternatively, the full path to the `poetry` binary can always be used:

- `$POETRY_HOME/bin/poetry` if `$POETRY_HOME` is set.
- `~/Library/Application Support/pypoetry/bin/poetry` on MacOS.
- `~/.local/share/pypoetry/bin/poetry` on Linux/Unix.
- `%APPDATA%\pypoetry\Scripts\poetry` on Windows.

{{< /step >}}
{{< step >}}
**Use Poetry**

Once Poetry is installed and in your `$PATH`, you can execute the following:

```bash
poetry --version
```

If you see something like `Poetry (version 1.2.0)`, your install is ready to use!
{{< /step >}}
{{< step >}}
**Update Poetry**

Poetry is able to update itself when installed using the official installer.

```bash
poetry self update
```

If you want to install pre-release versions, you can use the `--preview` option.

```bash
poetry self update --preview
```

And finally, if you want to install a specific version, you can pass it as an argument
to `self update`.

```bash
poetry self update 1.2.0
```

{{% warning %}}
Poetry `1.1` series releases are not able to update in-place to `1.2` or newer series releases.
To migrate to newer releases, uninstall using your original install method, and then reinstall
using the [methods above]({{< ref "#installation" >}} "Installation").
{{% /warning %}}
{{< /step >}}
{{< step >}}
**Uninstall Poetry**

If you decide Poetry isn't your thing, you can completely remove it from your system
by running the installer again with the `--uninstall` option or by setting
the `POETRY_UNINSTALL` environment variable before executing the installer.

```bash
curl -sSL https://install.python-poetry.org | python3 - --uninstall
curl -sSL https://install.python-poetry.org | POETRY_UNINSTALL=1 python3 -
```

{{% warning %}}
If you installed using the deprecated `get-poetry.py` script, you should use it to uninstall instead:

```bash
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 - --uninstall
```
{{% /warning %}}

{{< /step >}}
{{< /steps >}}

{{< /tab >}}
{{< tab tabID="installing-with-pipx" >}}

Using [`pipx`](https://github.com/pypa/pipx) to install Poetry is also possible and fully supported.

`pipx` is used to install Python CLI applications globally while still isolating them in virtual environments.
`pipx` will manage upgrades and uninstalls when used to install Poetry.

{{< steps >}}
{{< step >}}
**Install Poetry**

```bash
pipx install poetry
```
{{< /step >}}
{{< step >}}
**Install Poetry (advanced)**

`pipx` can be install different versions of Poetry, using the same syntax as pip:

```bash
pipx install poetry==1.2.0
```

`pipx` can also install versions of Poetry in parallel, which allows for easy testing of alternate or prerelease
versions. Each version is given a unique, user-specified suffix, which will be used to create a unique binary name:

```bash
pipx install --suffix=@1.2.0 poetry==1.2.0
poetry@1.2.0 --version
```

```bash
pipx install --suffix=@preview --pip-args=--pre poetry
poetry@preview --version
```

Finally, `pipx` can install any valid [pip requirement spec](https://pip.pypa.io/en/stable/cli/pip_install/), which
allows for installations of the development version from `git`, or even for local testing of pull requests:

```
pipx install --suffix @master git+https://github.com/python-poetry/poetry.git@master
pipx install --suffix @pr1234 git+https://github.com/python-poetry/poetry.git@refs/pull/1234/head

```
{{< /step >}}
{{< step >}}
**Update Poetry**

```bash
pipx upgrade poetry
```
{{< /step >}}
{{< step >}}
**Uninstall Poetry**

```bash
pipx uninstall poetry
```
{{< /step >}}
{{< /steps >}}

{{< /tab >}}
{{< tab tabID="installing-manually" >}}

Poetry can be installed manually using `pip` and the `venv` module. By doing so you will essentially perform the steps carried
out by the official installer. As this is an advanced installation method, these instructions are Unix-only and omit specific
examples such as installing from `git`.

The variable `$VENV_PATH` will be used to indicate the path at which the virtual environment was created.

```bash
python3 -m venv $VENV_PATH
$VENV_PATH/bin/pip install -U pip setuptools
$VENV_PATH/bin/pip install poetry
```

Poetry will be available at `$VENV_PATH/bin/poetry` and can be invoked directly or symlinked elsewhere.

To uninstall Poetry, simply delete the entire `$VENV_PATH` directory.

{{< /tab >}}
{{< /tabs >}}


## Enable tab completion for Bash, Fish, or Zsh

`poetry` supports generating completion scripts for Bash, Fish, and Zsh.
See `poetry help completions` for full details, but the gist is as simple as using one of the following:


```bash
# Bash
poetry completions bash > /etc/bash_completion.d/poetry

# Fish
poetry completions fish > ~/.config/fish/completions/poetry.fish

# Zsh
poetry completions zsh > ~/.zfunc/_poetry

# Oh-My-Zsh
mkdir $ZSH_CUSTOM/plugins/poetry
poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry

# prezto
poetry completions zsh > ~/.zprezto/modules/completion/external/src/_poetry

```

{{% note %}}
You may need to restart your shell in order for the changes to take effect.
{{% /note %}}

For `zsh`, you must then add the following lines in your `~/.zshrc`

```bash
fpath+=~/.zfunc
autoload -Uz compinit && compinit
```

For `oh-my-zsh`, you must then enable poetry in your `~/.zshrc` plugins

```text
plugins(
	poetry
	...
	)
```
