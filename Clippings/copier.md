---
title: "copier"
source: "https://copier.readthedocs.io/en/stable/"
author:
published:
created: 2025-10-01
description: "Library and command-line utility for rendering projects templates."
tags:
  - "clippings"
---
[Skip to content](https://copier.readthedocs.io/en/stable/#_1)

## ¶

A library and CLI app for rendering project templates.

- Works with **local** paths and **Git URLs**.
- Your project can include any file and Copier can dynamically replace values in any kind of text file.
- It generates a beautiful output and takes care of not overwriting existing files unless instructed to do so.

![Sample output](https://github.com/copier-org/copier/raw/master/img/copier-output.png)

## Installation

1. Install Python 3.9 or newer.
2. Install Git 2.27 or newer.
3. To use as a CLI app: [`pipx install copier`](https://github.com/pypa/pipx) or [`uv tool install copier`](https://docs.astral.sh/uv/#tool-management)
4. To use as a library: `pip install copier` or `conda install -c conda-forge copier`

### Nix flake

To install latest Copier release with 100% reproducibility:

```js
nix profile install 'https://flakehub.com/f/copier-org/copier/*.tar.gz'
```

## Quick start

To create a template:

```js
📁 my_copier_template                        # your template project
├── 📄 copier.yml                            # your template configuration
├── 📁 .git/                                 # your template is a Git repository
├── 📁 {{project_name}}                      # a folder with a templated name
│   └── 📄 {{module_name}}.py.jinja          # a file with a templated name
└── 📄 {{_copier_conf.answers_file}}.jinja   # answers are recorded here
```
```js
copier.yml# questions
project_name:
    type: str
    help: What is your project name?

module_name:
    type: str
    help: What is your Python module name?
```
```js
{{project_name}}/{{module_name}}.py.jinjaprint("Hello from {{module_name}}!")
```
```js
{{_copier_conf.answers_file}}.jinja# Changes here will be overwritten by Copier
{{ _copier_answers|to_nice_yaml -}}
```

To generate a project from the template:

- On the command-line:
	```js
	copier copy path/to/project/template path/to/destination
	```
- Or in Python code, programmatically:
	```js
	from copier import run_copy
	# Create a project from a local path
	run_copy("path/to/project/template", "path/to/destination")
	# Or from a Git URL.
	run_copy("https://github.com/copier-org/copier.git", "path/to/destination")
	# You can also use "gh:" as a shortcut of "https://github.com/"
	run_copy("gh:copier-org/copier.git", "path/to/destination")
	# Or "gl:" as a shortcut of "https://gitlab.com/"
	run_copy("gl:copier-org/copier.git", "path/to/destination")
	```

## Basic concepts

Copier is composed of these main concepts:

1. **Templates**. They lay out how to generate the subproject.
2. **Questionnaires**. They are configured in the template. Answers are used to generate projects.
3. **Projects**. This is where your real program lives. But it is usually generated and/or updated from a template.

Copier targets these main human audiences:

1. **Template creators**. Programmers that repeat code too much and prefer a tool to do it for them.
	***Tip:*** Copier doesn't replace the DRY principle... but sometimes you simply can't be DRY and you need a DRYing machine...
2. **Template consumers**. Programmers that want to start a new project quickly, or that want to evolve it comfortably.

Non-humans should be happy also by using Copier's CLI or API, as long as their expectations are the same as for those humans... and as long as they have feelings.

Templates have these goals:

1. **[Code scaffolding](https://en.wikipedia.org/wiki/Scaffold_\(programming\))**. Help consumers have a working source code tree as quickly as possible. All templates allow scaffolding.
2. **Code lifecycle management**. When the template evolves, let consumers update their projects. Not all templates allow updating.

Copier tries to have a smooth learning curve that lets you create simple templates that can evolve into complex ones as needed.

## Browse or tag public templates

You can browse public Copier templates on GitHub using. Use them as inspiration!

If you want your template to appear in that list, just add the topic to it! 🏷

## Show your support

If you're using Copier, consider adding the Copier badge to your project's `README.md`:

```js
[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)
```

...or `README.rst`:

```js
.. image:: https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json
    :target: https://github.com/copier-org/copier
    :alt: Copier
```

...or, as HTML:

```js
<a href="https://github.com/copier-org/copier"><img src="https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json" alt="Copier" style="max-width:100%;"/></a>
```

### Copier badge variations

1. Badge Grayscale Border
2. Badge Grayscale Inverted Border
3. Badge Grayscale Inverted Border Orange
4. Badge Grayscale Inverted Border Red
5. Badge Grayscale Inverted Border Teal
6. Badge Grayscale Inverted Border Purple
7. Badge Black

## Credits

Special thanks go to [jpsca](https://github.com/jpsca) for originally creating `Copier`. This project would not be a thing without him.

Many thanks to [pykong](https://github.com/pykong) who took over maintainership on the project, promoted it, and laid out the bases of what the project is today.

Big thanks also go to [yajo](https://github.com/yajo) for his relentless zest for improving `Copier` even further.

Thanks a lot, [pawamoy](https://github.com/pawamoy) for polishing very important rough edges and improving the documentation and UX a lot.

Also special thanks to [sisp](https://github.com/sisp) for being very helpful in polishing documentation, fixing bugs, helping the community and cleaning up the codebase.

And thanks to all financial supporters and folks that give us a shiny star! ⭐

[![Star History Chart](https://api.star-history.com/svg?repos=copier-org/copier&type=Date)](https://star-history.com/#copier-org/copier&Date)