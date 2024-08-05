# CPS1 Documentation

## Requirements

This project requires Python and Poetry to run and build.

If you don't have Poetry and/or Python:

1. [Install pyenv](https://github.com/pyenv/pyenv#installation) to manage Python
2. [Install poetry](https://python-poetry.org/docs/#installation) to manage dependencies

⚠️ Due to a limitation of Cloudflare's Build System, we must use Poetry version 1.6.1.

```
pip install pipx
pipx install poetry==1.6.1
```

For more details: https://developers.cloudflare.com/pages/configuration/language-support-and-tools/

## Configure Cloudflare Pages

When creating a new page, make sure the section *Build configurations* looks like this:

* Build command: `poetry run mkdocs build`
* Build output directory: `/site`
* Build comments on pull requests: `Enabled`

In case to change the configuration after creating the page, follow this steps: *Workers & Pages -> [Page name] -> Settings -> Build & Deployments -> Build configurations*


## Setup

1. Make sure you are using the correct Python with `pyenv version`
2. Install dependencies with `poetry install`

## Running

1. Start the dev server with `poetry run mkdocs serve`
2. Open the site at `http://localhost:8000`

