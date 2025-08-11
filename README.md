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

## Versioning and deployment

### Published versions

To edit a published version checkout in their branch, regenerate the docs and
push the deployed bundle in the gh-pages branch.

If you want to update the version v0.1:
```
git checkout v0.1

# Make changes

mike delete v0.1
mike deploy v0.1
# If v0.1 is the latest, use `mike deploy v0.1 latest --update-aliases` instead

# Push your changes through a PR or in the version branch

# To publish the update:
git checkout gh-pages
git push origin gh-pages
```

### Unpublished versions

To update the documentation of an unpublished version (work in progress), go
to the new version branch update the docs and use `mkdocs` normally. If there
is no branch yet, create a new one from the `main` branch.

When the new version is done:
1. Open a PR to the main branch to keep it updated
2. Run `mike deploy <new-version> latest`
3. Test the new and older versions with `mike serve -a 0.0.0.0:8000`
4. Publish it pushing the changes in the `gh-pages` branch
