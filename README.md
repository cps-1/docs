# CPS1 Documentation

## Requirements

This project requires Python 3.13 and Poetry to run and build.

If you don't have Poetry and/or Python:

1. [Install pyenv](https://github.com/pyenv/pyenv#installation) to manage Python
2. [Install poetry](https://python-poetry.org/docs/#installation) to manage dependencies

```
pip install pipx
pipx install poetry
```

## Setup and running

1. Install dependencies with `poetry install`
2. Start the dev server with `poetry run mkdocs serve -a 0.0.0.0:8000`

## Versioning

Use `mike deploy <version>` to deploy a new version in the `gh-pages` branch.

Use `mike deploy <version> latest` to mark it as the default latest stable version.

To start the dev server visualizing all available versions use `mike serve -a 0.0.0.0:8000`

## Configuring Cloudflare Pages (optional)

When creating a new page, make sure the section *Build configurations* looks like this:

* Build command: `poetry run mkdocs build`
* Build output directory: `/site`
* Build comments on pull requests: `Enabled`

In case you need to change the configuration after creating the page, follow this steps: *Workers & Pages -> [Page name] -> Settings -> Build configurations*

