---
title: "jlevy/simple-modern-uv: A minimal, modern Python project template using uv. An instantiated version of this template here"
source: https://github.com/jlevy/simple-modern-uv
author:
  - "[[jlevy]]"
published:
created: 2025-10-01
description: A minimal, modern Python project template using uv. An instantiated version of this template here - jlevy/simple-modern-uv
tags:
  - clippings
  - uv
---
**[simple-modern-uv](https://github.com/jlevy/simple-modern-uv)** Public

A minimal, modern Python project template using uv. An instantiated version of this template here

[github.com/jlevy/simple-modern-uv-template](https://github.com/jlevy/simple-modern-uv-template "https://github.com/jlevy/simple-modern-uv-template")

[MIT license](https://github.com/jlevy/simple-modern-uv/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/jlevy/simple-modern-uv?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"><p><span><a href="https://github.com/jlevy/simple-modern-uv/commit/1ee5f8487bc91c38e2a3e365df95e7d2c05abe32">Upgrade uv to v0.8.13.</a></span></p><p><span><a href="https://github.com/jlevy/simple-modern-uv/commit/1ee5f8487bc91c38e2a3e365df95e7d2c05abe32">1ee5f84</a> ·</span></p><p><a href="https://github.com/jlevy/simple-modern-uv/commits/main/"><span><span><span>101 Commits</span></span></span></a></p></td></tr><tr><td colspan="2"><p><a href="https://github.com/jlevy/simple-modern-uv/tree/main/template">template</a></p></td><td colspan="1"><p><a href="https://github.com/jlevy/simple-modern-uv/tree/main/template">template</a></p></td><td><p><a href="https://github.com/jlevy/simple-modern-uv/commit/1ee5f8487bc91c38e2a3e365df95e7d2c05abe32">Upgrade uv to v0.8.13.</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/jlevy/simple-modern-uv/commit/98316a724ad68f67ac9e91606c6216f164778bb2">Minor additions to.gitignore.</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/LICENSE">LICENSE</a></p></td><td colspan="1"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/LICENSE">LICENSE</a></p></td><td><p><a href="https://github.com/jlevy/simple-modern-uv/commit/d2df3b583d219f3293be513564f49da9ddb22845">Initial commit</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/README.md">README.md</a></p></td><td colspan="1"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/README.md">README.md</a></p></td><td><p><a href="https://github.com/jlevy/simple-modern-uv/commit/4efc5a68e32ee90f40b67e55f72861ae58c87422">Improve docs, a few more links.</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/copier.yml">copier.yml</a></p></td><td colspan="1"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/copier.yml">copier.yml</a></p></td><td><p><a href="https://github.com/jlevy/simple-modern-uv/commit/72c91117d9cd37138ea3034e378183615687a445">Update dummy args.</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/pyproject.toml">pyproject.toml</a></p></td><td colspan="1"><p><a href="https://github.com/jlevy/simple-modern-uv/blob/main/pyproject.toml">pyproject.toml</a></p></td><td><p><a href="https://github.com/jlevy/simple-modern-uv/commit/77436b3ec361e93968d9718d77c4cf4f3d172793">Change slightly confusing emoji.</a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

[![As usual, XKCD has a comic for this](https://camo.githubusercontent.com/25145e1b839fca2ae932a7dac63f61040b09675717991e9102588a4b724735b2/68747470733a2f2f696d67732e786b63642e636f6d2f636f6d6963732f707974686f6e5f656e7669726f6e6d656e742e706e67)](https://xkcd.com/1987/)

(As usual, XKCD has a comic for this. Appropriately enough, the comic is out of date.)

## simple-modern-uv

**simple-modern-uv** is a minimal, modern **Python project template** for new projects (Python 3.11–3.13) based on [**uv**](https://docs.astral.sh/uv/). This template aims to be a good base for serious work but also simple so it's an easy option for any small project, like an open source library or tool.

> **The Story So Far**
> 
> In the beginning, there was a hack called [`setup.py`](https://github.com/pypa/setuptools) for packaging (1990s–2000s) and it was not good.
> 
> Then there arose [`virtualenv`](https://github.com/pypa/virtualenv),[`pip`](https://github.com/pypa/pip), and `requirements.txt` for isolated environments (2008–2011). Yet confusion still reigned.
> 
> Meanwhile, [`conda`](https://github.com/conda/conda),[`pyenv`](https://github.com/pyenv/pyenv), [`brew`](https://github.com/Homebrew/brew), and [`PyInstaller`](https://github.com/pyinstaller/pyinstaller) vied to rule the system installations (2010s).
> 
> Years of dissatisfaction led to the spread of a new religion,[`pyproject.toml`](https://github.com/pypa/pyproject.toml). Adherents of [`poetry`](https://github.com/python-poetry/poetry),[`pipenv`](https://github.com/pypa/pipenv), and [`pipx`](https://github.com/pypa/pipx) promised peace and prosperity (2020s) yet somehow, life felt mostly the same.
> 
> Then AI robots began to invade. Rebel forces [`uv`](https://github.com/astral-sh/uv) and [`pixi`](https://github.com/prefix-dev/pixi) aligned with Rust gathered strength …

Apologies for the digression. The point is that unfortunately, the accidents of history make it quite confusing to learn best practices for setting up Python projects and dependencies. But it shouldn't have to be this difficult, especially since uv has now significantly simplified Python dev tooling.

If you haven't switched to uv, I can say I too was a little hesitant. It's often possible to switch dev tooling prematurely because a the new tool is shiny and exciting. But the advantages of uv have become too numerous to ignore.[This article](https://www.bitecode.dev/p/a-year-of-uv-pros-cons-and-should) (Feb 2025) has a good overview.

This is the template I now use myself as I have been migrating from Poetry to uv for several projects. It's new but it's working well.

A lot of more senior engineers have justified hesitancy about templates. Templates can be a real problem if they add mindless, unexamined complexity. But if done carefully, I think they are better than official docs (they show real-world code you can adapt, instead of leaving you to figure out each tool choice and setting) or blog posts (that are typically not maintained or updated).

I think a good project template should be **3 Ms: minimalist, modern, and maintained**. I looked at [other templates](https://github.com/jlevy/#alternatives) but wanted one that was modern and "done right" but *absolutely as simple as possible*. Few existing templates seem to be both simple and use the newest generation of tools and best practices.

The template is short enough to read and understand in about 10 minutes. It's **only ~300 lines of code** so you can just look at it, use it, and change what you want without fuss.

Because this template is minimal, you can always start with it and then pull in other tools and features if you want them. (In fact, even if you don't like this template, you might want to use it as inspiration for your *own* Copier template, to take advantage of the Copier update workflow discussed next.)

One other benefit of this template is it uses [**copier**](https://github.com/copier-org/copier).

Unlike with many previous project template tools, Copier allows you [pull future changes](https://github.com/jlevy/#updating-your-project-template) to a template back into your instantiated copy any time.

You can start a project now, then if this template improves or is updated with other tools, you can pull those improvements back into your project, much like a git merge. You could even fork this repo yourself, then build your own forked template, and maintain it yourself.

simple-modern-uv uses uses the tools I've come to think are best for new projects:

- [**uv**](https://github.com/astral-sh/uv) for project setup and dependencies. There is also a simple makefile for dev workflows, but it simply is a convenience for running uv commands.
- [**ruff**](https://github.com/charliermarsh/ruff) for modern linting and formatting. Previously, [black](https://github.com/psf/black) was the definitive formatting tool, but ruff now handles linting and fast, black-compatible formatting.
- [**GitHub Actions**](https://github.com/actions/setup-python) for CI and publishing workflows.
- [**Dynamic versioning**](https://github.com/ninoseki/uv-dynamic-versioning/) so release and package publication is as simple as creating a tag/release on GitHub (no machinery needed to manually bump versions and commit files every release).
- Workflows for **packaging and publishing to PyPI** with uv. This has always been more confusing than it should be. The [official docs](https://packaging.python.org/en/latest/tutorials/packaging-projects/) about packaging are several pages long, and then even [toy tutorials](https://realpython.com/pypi-publish-python-package/) about publishing are even longer. This template makes all of that basically automatic with uv, GitHub Actions, and dynamic versioning.
- Type checking with [**BasedPyright**](https://github.com/detachhead/basedpyright). (See below for more on this.)
- [**Pytest**](https://github.com/pytest-dev/pytest) for tests (with the excellent plugin [**pytest-sugar**](https://github.com/Teemu/pytest-sugar) for faster errors and nicer output).
- [**codespell**](https://github.com/codespell-project/codespell) for drop-in spell checking.

## Starter Docs

The template includes a few **starter docs** for you, collaborators, and users:

- [README.md](https://github.com/jlevy/simple-modern-uv/blob/main/template/README.md.jinja) is a placeholder for your project readme.
- [installation.md](https://github.com/jlevy/simple-modern-uv/blob/main/template/installation.md) has brief reminders on the modern ways to install uv and Python.
- [development.md](https://github.com/jlevy/simple-modern-uv/blob/main/template/development.md.jinja) covers basic developer workflows.
- [publishing.md](https://github.com/jlevy/simple-modern-uv/blob/main/template/publishing.md) covers how to publish your project to PyPI.

You can edit or delete these, but typically it's sufficient to just edit the README.md. It helps to have the others in separate files so they get updated whenever you update the template.

## Agent Rules

This template also includes a few **agent rules** for use with Cursor, Claude Code, and OpenAI Codex.

These cover a few specific rules for modern Python as well as remind agents to build, lint, and run tests correctly using uv.

The rules are in [.cursor/rules](https://github.com/jlevy/simple-modern-uv/blob/main/template/.cursor/rules) and copied by the [Makefile](https://github.com/jlevy/simple-modern-uv/blob/main/template/Makefile) to [`CLAUDE.md`](https://docs.anthropic.com/en/docs/claude-code/memory) and [`AGENTS.md`](https://github.com/openai/codex#memory--project-docs) so that the same rules work for Claude Code and OpenAI Codex. (Of course you can adjust these as you wish.)

The choice of what tool to use for type checking deserves some explanation. This seems to be a confusing area.

Like many, I'd previously been using [Mypy](https://github.com/python/mypy), the OG type checker for Python. Mypy has since been enhanced with [BasedMypy](https://github.com/KotlinIsland/basedmypy).

The other popular alternative is Microsoft's [Pyright](https://github.com/microsoft/pyright). And it has a newer extension and fork called [BasedPyright](https://github.com/DetachHead/basedpyright).

All of these work in build systems. But this is a choice not just of build tooling—it is far preferable to have your type checker warnings align with your IDE warnings. With the rises of AI-powered IDEs like Cursor and Windsurf that are VSCode extensions, it seems like type checking support as a VSCode-compatible extension is essential.

However, Microsoft's popular [Mypy VSCode extension](https://marketplace.visualstudio.com/items?itemName=ms-python.mypy-type-checker) is licensed only for use in VSCode (not other IDEs) and [sometimes](https://forum.cursor.com/t/pylance-server-fails-to-initialize-due-to-licensing-restriction/48548) [refuses](https://forum.cursor.com/t/does-pylance-just-not-work-with-cursor-how-to-get-imports-in-quick-fix-menu/5747) to work in Cursor. [Cursor's docs](https://docs.cursor.com/guides/languages/python) suggest Mypy but don't suggest a VSCode extension.

After some experimentation, I found [BasedPyright](https://github.com/detachhead/basedpyright) to be a credible improvement on [Pyright](https://github.com/microsoft/pyright). BasedPyright is well maintained, is faster than Mypy, and has a good [VSCode extension](https://marketplace.visualstudio.com/items?itemName=detachhead.basedpyright) that works with Cursor and other VSCode forks. So I have now switched this template to use BasedPyright. (But please drop a note in the Discussion tab if you have better suggestions.)

The template doesn't have lots of options or try to use every bell and whistle. It just adds the above essentials.

This template **does not** handle:

- Using Docker
- Private or enterprise package repositories (but you can add this—see [uv's docs on alternative indexes](https://docs.astral.sh/uv/guides/integration/alternative-indexes/))
- Building websites or docs, e.g. with [mkdocs](https://github.com/mkdocs/mkdocs)
- Using [Conda](https://github.com/conda/conda) for dependencies (but note many deep learning libraries like PyTorch now support pip so this isn't as necessary as often as it used to be)
- Using a code repo or build system that isn't GitHub and GitHub Actions
- Boilerplate docs or project management of any kind, like issue templates, contributing guidelines, code of conduct, etc.

Docker and private repo use can be added by you manually to the project after you get started. Similarly, you can change CI/CD workflows if you are not using GitHub or GitHub Actions or PyPI.

Also see [below](https://github.com/jlevy/#alternatives) for other templates you can look at or use as references.

The template can be used in three ways. Option 1 is the quickest option with full flexibility. Option 2 is the normal way to use a Copier template by hand. Option 3 is handy if you prefer a GitHub template.

I've now created a little tool, [uvinit](https://www.github.com/jlevy/uvinit) that copies this template for you and walks you through everything:

```
uvx uvinit
```

It's the same as running `copier` and a few `git` commands yourself, with a little more guidance and less typing.

This template uses [Copier](https://github.com/copier-org/copier), which seems like the best tool nowadays for project templates. Using Copier is the recommended approach since it then lets you instantiate the template variables and makes future updates possible. But it requires a few more commands.

To create a new project repo with `copier`:

```
# Install Copier:
uv tool install copier

# Change dirs to the place you want the new GitHub repo to be.
cd ~/projects/github   # Wherever you do your project work.

# Clone this template. This does everything!
# It will fetch from this GitHub repo and create a new directory
# with whatever name you put below:
copier copy gh:jlevy/simple-modern-uv YOURNEWREPO
# Then follow the instructions.
```

You can enter names for the project, description, etc., or just press enter and later look for `changeme` in the code.

Once you have the template set up, you will need to check the code into Git for uv to work. [Create a new GitHub repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository) and add your initial code:

```
cd PROJECT
git init
# Make license or other initial adjustments if needed.
git add .
git commit -m "Initial commit from simple-modern-uv."
# Create repo on GitHub.
git remote add origin git@github.com:OWNER/PROJECT.git  # or https://github.com/...
git branch -M main
git push -u origin main
```

If you prefer you can click the **use this template** on [**this repository**](https://github.com/jlevy/simple-modern-uv-template), which is the current output of this template.

Go there and hit the "Use this template" button. Once you have the code, search for **`changeme`** for all field names like project name, author, etc. You want to do this to the `.copier-answers.yml` file as well. You will also want to check the license/copyright.

Everything to get started is linked from the project **README.md**. It links to the **installation.md**, **development.md**, and **publishing.md** [starter docs](https://github.com/jlevy/#starter-docs).

If you use Option 1 or Option 2 or if you pick Option 3 and correctly fill in your`.copier-answers.yml` file, you have the option to update your project with any future updates to this template at any time.

If this file is updated with your project name etc., then you can [update your project](https://copier.readthedocs.io/en/latest/updating/) to reflect any changes to this template by running `copier update`.

## Alternatives

There are a couple other good uv templates, especially [**cookiecutter-uv**](https://github.com/fpgmaas/cookiecutter-uv) and [**copier-uv**](https://github.com/pawamoy/copier-uv) you may wish to consider.

This template takes a somewhat different philosophy. I found existing templates to have machinery or files you often don't need. And it's hard to maintain a complex template repo. This is intended instead to be a very simple template. You can always add to it if you want.

There is also [**uv-migrator**](https://github.com/stvnksslr/uv-migrator) to help you migrate projects to uv.

Previously, [Poetry](https://python-poetry.org/docs/basic-usage/) was probably the best modern tool for managing dependencies. It is not as new as uv and arguably more mature (it just hit version 2.0). In fact, this template is based on my earlier Poetry template,[simple-modern-poetry](https://github.com/jlevy/simple-modern-poetry).

Another great resource to check is [**python-blueprint**](https://github.com/johnthagen/python-blueprint), which is a more established template with an excellent overview of other standard Python project best practices. It uses [Poetry](https://python-poetry.org/docs/basic-usage/),[nox](https://github.com/wntrblm/nox),[Material for Mkdocs](https://github.com/squidfunk/mkdocs-material), and Docker.

For [Conda](https://github.com/conda/conda) dependencies, also consider the newer [**pixi**](https://github.com/prefix-dev/pixi/) package manager.

## Contributing

I'm new to uv, so please help me improve this! Please use the Discussions thread with any feedback or suggestions. PRs welcome on [this repository](https://github.com/jlevy/simple-modern-uv) (not on the GitHub template repo, which mirrors this one).

## Releases 19

[\+ 18 releases](https://github.com/jlevy/simple-modern-uv/releases)

## Languages

- [Jinja 77.8%](https://github.com/jlevy/simple-modern-uv/search?l=jinja)
- [Python 13.4%](https://github.com/jlevy/simple-modern-uv/search?l=python)
- [Makefile 8.8%](https://github.com/jlevy/simple-modern-uv/search?l=makefile)