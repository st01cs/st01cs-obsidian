---
title: "The Python Developer’s Guide: From pip to uv"
source: "https://python.plainenglish.io/from-pip-to-uv-a-comprehensive-guide-for-python-developers-01507b6b8875"
author:
  - "[[Mayuresh K]]"
published: 2025-04-15
created: 2025-10-01
description: "Developer Guides The Python Developer’s Guide: From pip to uv Accelerating Your Python Development with a Faster and Modern Package Manager — uv. As Python developers, most of us have grown used …"
tags:
  - "clippings"
---
[Sitemap](https://python.plainenglish.io/sitemap/sitemap.xml)

Get unlimited access to the best of Medium for less than $1/week.[Become a member](https://medium.com/plans?source=upgrade_membership---post_top_nav_upsell-----------------------------------------)

[

Become a member

](https://medium.com/plans?source=upgrade_membership---post_top_nav_upsell-----------------------------------------)## [Python in Plain English](https://python.plainenglish.io/?source=post_page---publication_nav-78073def27b8-01507b6b8875---------------------------------------)



New Python content every day. Follow to join our 3.5M+ monthly readers.

## Developer Guides

Photo by Christin Hume on Unsplash

As Python developers, most of us have grown used to using `pip` as our primary package manager. With good reason too. It has been the default tool bundled with Python, it is stable, well-documented, and gets the job done. However, the Python ecosystem continues to evolve, and new tools emerge to address limitations in our existing workflows. One such tool that's been gaining traction is `uv`, a fast Python package manager written in [Rust](https://www.rust-lang.org/).

> **See also**: [The Python Developer’s Guide: Moving from pip to Poetry](https://medium.com/@mskadu/the-python-developers-guide-from-pip-to-poetry-220876ce914c)

In this article, we will go through the process of switching from `pip` to `uv`, exploring both the technical aspects and the general considerations behind making such a change. We will also examine the pros and cons, provide installation instructions, and share practical tips for integrating `uv` into your development workflow.

![A screenshot of the top 6 features of the “uv” tool](https://miro.medium.com/v2/resize:fit:640/format:webp/1*CHNrTrTM6_eOaVaQt_1KuA.png)

Just the top 5–6 features of uv are very attractive! (source: uv docs )

## So — What is uv?

`uv` is a modern Python package manager written in [Rust](https://www.rust-lang.org/learn). It aims to be a drop-in replacement for `pip` and other Python packaging tools, offering significant performance improvements and additional features.

The project's name "uv" comes from "universal virtualenv"—reflecting its goal to provide a comprehensive solution for Python environment management.

## Why Bother Switching from pip to uv?

Before we dive into the technical details, let’s explore some reasons *why* you might consider making the switch:

### Performance

The most immediately noticeable advantage of `uv` is its speed. Being written in Rust rather than Python, `uv` can install packages significantly faster than `pip` — [often by an order of magnitude](https://github.com/astral-sh/uv/blob/main/BENCHMARKS.md). This performance boost becomes particularly valuable when:

- Working with projects that have numerous dependencies
- Setting up CI/CD pipelines where installation time impacts overall build time
- Managing multiple virtual environments across different projects

### Dependency Resolution

`uv` implements its own dependency resolver that aims to be both faster and more reliable than pip's. It can potentially handle complex dependency graphs more efficiently and with fewer conflicts.

### Modern Features

`uv` also comes with several modern features that address common pain points in Python package management, including better caching mechanisms and more intuitive command-line interfaces.

## Installation

Let’s start with installing `uv` on macOS (see [here](https://docs.astral.sh/uv/getting-started/installation/) for other operating systems):

```c
# Using Homebrew
brew install uv

# Alternatively, using pip
pip install uv
```

## Basic Usage: Converting pip Commands to uv

If you’re familiar with `pip`, transitioning to `uv` is relatively straightforward as many commands have direct equivalents:

### Installing Packages

```c
# With pip
pip install requests

# With uv
uv pip install requests
```

When you run this command, you’ll see output similar to:

```c
Installing packages...
Successfully installed requests-2.31.0 certifi-2023.7.22 charset-normalizer-3.2.0 idna-3.4 urllib3-2.0.4
Resolved 5 packages in 0.12s
```

I find that `uv` typically tends to provide more detailed timing information, highlighting its performance advantages

### Installing from Requirements File

```c
# With pip
pip install -r requirements.txt

# With uv
uv pip install -r requirements.txt
```

The command reads the specified requirements file and installs all listed packages, usually much faster than pip would.

### Creating a Virtual Environment

```c
# With standard tools
python -m venv .venv

# With uv
uv venv
```

By default, `uv venv` creates a virtual environment in the `.venv` directory of your project, just like the standard `venv` module. For additional options and customizations when creating virtual environments, please check out the [uv venv documentation](https://github.com/astral-sh/uv/blob/main/docs/venv.md).

## Advanced Usage

### uv-Specific Commands Without pip Equivalents

One of the advantages of `uv` is that it provides some unique commands that don't have direct equivalents in `pip`. Here are some of the most useful ones:

### Quickly create a new project

```c
# method 1 - i am lazy, i prefer this ;)
uv init hello-world

# method 2 
mkdir hello-world
cd hello-world
uv init
```

in either case, your new project folder should look like this:

```c
.
├── .venv
│   ├── bin
│   ├── lib
│   └── pyvenv.cfg
├── .git
├── .gitignore
├── .python-version
├── README.md
├── main.py
├── pyproject.toml
└── uv.lock
```

`uv` [documentation](https://docs.astral.sh/uv/guides/projects/) has a detailed explanation on each of the files it creates when initialising a project.

### Quickly create a python script — with dependencies

Although I don’t use this as much, it is a pretty useful feature to have handy:

```c
uv init --script example.py

# Use a specific version of python
uv init --script example.py --python 3.11
```

### Quickly Setup your (uv) Project from scratch

This is useful if you’ve just `git clone` -d a repository created using `uv`

```c
uv sync
```

This will create a virtual environment, if one was not already present. It will activate it and then go on to add/ remove packages.

Note: This uses the lock file (typically `uv.lock`)

For more details on `uv sync` and its advanced options, see the [sync command documentation](https://docs.astral.sh/uv/reference/cli/#uv-sync).

### Quickly Setup your (pip) Project from scratch

In case your repository used `pip` then:

```c
# this should work similar to - uv sync
uv pip sync requirements.txt

# use this if you'd much rather only install new packages and not remove old ones
uv pip install --requirements requirements.txt
```

### Cache Management

```c
# View the cache
uv cache dir

# Clear the cache
uv cache clean
```

These commands give you more direct control over the package cache than what’s available in `pip`.

For a full list of commands that are unique to uv without pip equivalents, consult the [uv CLI reference](https://docs.astral.sh/uv/reference/cli/).

## Lock files and Reproducibility

One of the significant advantages of `uv` is its first-class support for lock files, which help ensure reproducible environments:

```c
# Generate a lockfile (uv.lock by default)
uv lock

# Bring the environment up to speed with your lock file
uv sync

# Is your environment in sync with your lock file?
uv lock --check
```

and I have not even began to scratch the surface of `uv` 's lock and sync feature is capable of. Check out [this documentation](https://docs.astral.sh/uv/concepts/projects/sync/#automatic-lock-and-sync) for further details.

## Pros and Cons of Switching to uv

Now, let’s look at the advantages and disadvantages of making the switch from `pip` to `uv`:

### Pros

1. **Speed**: The performance improvement is substantial, particularly for projects with many dependencies or in CI/CD environments.
2. **Modern Features**: `uv` incorporates lessons learned from years of Python packaging experience and from other language ecosystems.
3. **Better Dependency Resolution**: The resolver in `uv` can handle complex dependency situations more effectively.
4. **Active Development**: The tool is being actively developed and improved.
5. **Drop-in Replacement**: You can largely use it as a direct replacement for `pip` without significant workflow changes.

### Cons

1. **Relative Newness**: As a newer tool in the ecosystem, `uv` hasn't been battle-tested to the same extent as `pip`.
2. **Community Support**: The vast majority of Python documentation and tutorials still reference `pip`, which could make troubleshooting more challenging.
3. **Compatibility**: While `uv` aims to be a drop-in replacement, there might be edge cases or specific packages that cause issues.
4. **Learning Curve**: There are some differences in command structure and options that require learning.
5. **Integration**: Some tools or workflows that expect `pip` to be used might require adaptation.

## Using uv in Corporate Settings

For those of us who use office laptops, corporate environments often present unique challenges for Python package management, particularly when dealing with firewalls, proxies, etc. Here’s how to effectively use `uv` in these settings:

### Working Behind Corporate Firewalls

When dealing a corporate firewall, you’ll typically need to configure proxy settings:

```c
# Configure HTTP proxy for uv
export HTTP_PROXY="http://proxy.example.com:8080"
export HTTPS_PROXY="http://proxy.example.com:8080"

# Then run uv commands as normal
uv install requests
```

Unlike `pip`, which reads from a `pip.conf` file, `uv` primarily uses environment variables for proxy configuration. This can actually be simpler to set up in some corporate environments.

### Using Private Package Repositories

Many organisations maintain private PyPI-compatible repositories (such as Artefactory, Nexus, or private DevPI servers) for internal packages:

```c
# Install from a private repository
uv install --index-url https://pypi.internal.company.com/simple/ internal-package

# Or use an additional index alongside PyPI
uv install --extra-index-url https://pypi.internal.company.com/simple/ internal-package
```

For persistent configuration, you can create a `uv.toml` file in your project directory:

```c
[pip]
index-url = "https://pypi.internal.company.com/simple/"
trusted-host = "pypi.internal.company.com"
```

Note: `uv` is also designed to look for a config file with the same name under:

- `~/.config/uv/)` — which will serve as user-level configuration
- `/etc/uv/` — which will serve as a system-level configuration

### Handling Self-Signed Certificates

Corporate environments often use self-signed certificates which can cause SSL verification issues:

```c
# Disable SSL verification (use with caution)
uv install --trusted-host pypi.internal.company.com --trusted-host files.pythonhosted.org package-name

# or
uv pip install --trusted-host pypi.internal.company.com --trusted-host files.pythonhosted.org package-name
```

Alternatively, configure your system’s certificate store to include your corporate certificates for a more secure approach.

For more detailed information on handling certificates and security in corporate environments, refer to the [security documentation](https://docs.astral.sh/uv/configuration/authentication/#custom-ca-certificates).

### Bandwidth Considerations

`uv` 's improved caching mechanisms can be particularly valuable in corporate settings where internet bandwidth might be limited or closely monitored:

```c
# View cache location
uv cache dir

# Cache packages for offline use
uv pip download -r requirements.txt -d ./offline-packages
```

This allows you to prepare packages when connected to the network, then install them later even when offline.

## Integration with Development Workflows

### Poetry Integration

If you’re using Poetry for project management, you can still benefit from `uv` 's speed:

```c
# Install dependencies using uv
poetry export -f requirements.txt | uv pip install -r -
```

> **See also**: [Python Developer’ Guide: From pip to Poetry](https://mskadu.medium.com/the-python-developers-guide-from-pip-to-poetry-220876ce914c)

### Working with CI/CD

For CI/CD pipelines, where installation speed can significantly impact build times, one could consider adding this to your GitHub Actions workflow:

```c
# GitHub Actions example
- name: Install dependencies
  run: |
    pip install uv
    uv pip install -r requirements.txt
```

This simple change can potentially reduce your build times substantially.

## Making the Transition: A Step-by-Step Approach

Rather than switching all your projects at once, consider a phased approach:

1. **Start with new projects**: Use `uv` for new development to get familiar with it.
2. **Try it on CI/CD first**: Implement `uv` in your continuous integration pipelines to benefit from faster builds.
3. **Gradually transition existing projects**: As you revisit older codebases, update their workflows to use `uv`.

## Summary

Switching from `pip` to `uv` offers compelling advantages, particularly around performance and modern dependency management. While there are trade-offs to consider, the seamless drop-in replacement nature of `uv` makes it relatively low-risk to try.

For most Python developers, incorporating `uv` into their workflow represents a valuable opportunity to improve productivity and address some of the long-standing pain points in Python package management. Whether you're managing complex dependency graphs or simply trying to speed up your development and deployment processes, `uv` is certainly worth considering.

As with any tool, evaluate it in the context of your specific needs and workflows. The Python ecosystem is all about choices and innovation. And `uv` represents an interesting step that direction.

If you’ve made the switch from pip to uv — What has your experience been like? Share your thoughts in the comments below!

## Further Reading

If you’ve enjoyed reading this article, please check out more at:

- [My Other Python-related Articles](https://mskadu.medium.com/list/all-my-python-related-articles-7b1adb2f14fe)
- [All My Technical Articles](https://mskadu.medium.com/list/all-my-technical-articles-f5f751fdb545)
- [All My AI-related Articles](https://mskadu.medium.com/list/all-my-ai-articles-02945f6a762f)
- [My Non-technical Articles](https://mskadu.medium.com/list/all-my-nontech-articles-cffc11238581)

**Disclaimer**: This article was proofread and edited with the assistance of AI technology to ensure clarity and accuracy of information. But if you still spot any errors or inconsistencies, please drop me a comment.

## Thank you for being a part of the community

*Before you go:*

- Be sure to **clap** and **follow** the writer ️👏 **️️**
- Follow us: [**X**](https://x.com/inPlainEngHQ) | [**LinkedIn**](https://www.linkedin.com/company/inplainenglish/) | [**YouTube**](https://www.youtube.com/@InPlainEnglish) | [**Newsletter**](https://newsletter.plainenglish.io/) | [**Podcast**](https://open.spotify.com/show/7qxylRWKhvZwMz2WuEoua0) | [**Twitch**](https://twitch.tv/inplainenglish)
- [**Start your own free AI-powered blog on Differ**](https://differ.blog/) 🚀
- [**Join our content creators community on Discord**](https://discord.gg/in-plain-english-709094664682340443) 🧑🏻💻
- For more content, visit [**plainenglish.io**](https://plainenglish.io/) + [**stackademic.com**](https://stackademic.com/)

[![Python in Plain English](https://miro.medium.com/v2/resize:fill:96:96/1*VA3oGfprJgj5fRsTjXp6fA@2x.png)](https://python.plainenglish.io/?source=post_page---post_publication_info--01507b6b8875---------------------------------------)

[![Python in Plain English](https://miro.medium.com/v2/resize:fill:128:128/1*VA3oGfprJgj5fRsTjXp6fA@2x.png)](https://python.plainenglish.io/?source=post_page---post_publication_info--01507b6b8875---------------------------------------)

[Last published 2 hours ago](https://python.plainenglish.io/these-9-python-skills-are-the-only-ones-that-actually-mattered-in-2025-90fa73ac9feb?source=post_page---post_publication_info--01507b6b8875---------------------------------------)

New Python content every day. Follow to join our 3.5M+ monthly readers.

Curious mind, husband, father, son, techie and voracious reader - in that particular order:) My articles will always be FREE reads.

## Responses (1)

5wun9

What are your thoughts?  

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--01507b6b8875---------------------------------------)