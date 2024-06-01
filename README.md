# Git-lab training
This repository contain a template python project with some industry standards/best-practices included. 

For the git-lab we will use this repository to learn `git`. 

To get started it is best to mirror-clone this repository into a fresh github repository. 

- Login to your personaadfadsfl github account
  - Create an account if you don't have one already
- Create a personal git-lab repository
- Mirror this repository. _this clones the repository including all it's history and branches._
  1. `git clone --mirror https://github.com/ramsesk/git-lab.git`
  2. `cd git-lab.git`
  3. `git push --mirror https://github.com/YOURUSERNAME/YOUR-REPO.git`
    - **replace the link**
  4. `cd ..`
  5. Remove the `git-lab.git` folder.
    - windows: `Remove-Item -Path ".\git-lab.git" -Recurse -Force
    - unix: `rm -rf ./git-lab.git`
  6. Clone the newly mirrored repository: `git clone https://github.com/YOURUSERNAME/YOUR-REPO.git`

**_optional:_** go to your github repository. go to actions. Enable the actions.

Exercises:

- Create a new branch `feature/readme-update`. Change the README.MD. Push the branch to github. Merge the change via a Pull-Request (PR).
  - If you are working on github, fix atleast that the github-actions badge is pointing to your repositories badge. [**HINT**](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge)
- Which branches are available in the repository?
- Merge `feature/improve-readme` via a PR.
  - To learn, it's better to resolve any issues locally.
- Merge `feature/fix-bla` via a PR  

_Extra exercises:_

- If you are familiar with Python: fix branch `feature/extra-things-for-the-library`
  - This requires some python programming
- **Remove the Password from the repo**
  - Why doesn't it work if you just remove the `secret_password.txt` file from the repo?
  - How can we make sure no one can see the `secret_password.txt`? --> [HINT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

Example Python project
======================

[![Python Checks and Tests](https://github.com/ramsesk/git-lab/actions/workflows/test-check.yaml/badge.svg)](https://github.com/ramsesk/git-lab/actions/workflows/test-check.yaml)

This is an example of a Python Project. Use this
as a starting point for creating new python projects.

There are multiple different kinds of Python projects possible.
This project is not an app.
This project is not a library.
This project is not a data science project.

This project does cover some basics that could fit in all of the previously managed
different types of python projects.
This project features examples of:

- structuring a python module
  - readme and changelog (`README.md`, `CHANGELOG.md`)
  - package namespacing (e.g. `ff`)
- testing with `pytest`
  - unittests
  - test coverage
  - fixtures
  - property-based tests (with `hypothesis`)
- running multiple checks with `tox`
  - code style
  - compatibility with multiple python versions
  - type checking
- (partially) autogenerated documentation with `sphinx`
- Setting up a build on github actions
- ...

Installation
------------

**TODO**

For now I don't think a project that is started from this template will have a clear installation instruction.
Perhaps it will have clear "starting development" instructions instead.

Usage
-----

To use this repository as a template, perform the following steps:

- copy the relevant files

  ```bash
  cd ff.examplelib
  cp -r {README.md,CHANGELOG.md,mypy.ini,pyproject.toml,poetry.lock,tox.ini,docs,src,tests,.gitignore,Makefile,bamboo-specs} path/to/new/repo/
  ```

- change the description in the README.
- change the package metadata in `pyproject.toml`. Reset the version.
- change the package name. Change this in all copied files!
  Do a text search (e.g. `grep`) to check you've found all references.
- remove any unneeded dependencies in `pyproject.toml` (e.g. `numpy`)

Development guide
-----------------

### Requirements

- Supported Python versions (see `pyproject.toml` )installed.
  See [HERE](./explanation/pyenv.md).
- The poetry dependency manager. Install as described [HERE](./explanation/poetry.md)

### Setup

First create a virtual environment:

On Mac:

```bash
pyenv virtualenv 3.9.8 exampleproj_3_9_8
```

On Windows:

```powershell
pyenv local 3.9.8
python -m venv .venv
.\.venv\Scripts\activate
```

To install all development requirements, run:

```bash
# running this in a virtualenv is highly recommended
poetry install
```

### make/run script?

**TODO** write some explanation on the make/run script.

### Checks

To run all checks (tests, linting, docs, etc), run:

```bash
tox
```

Use the `--parallel auto` option to run in parallel. If you run into
issues, try using the `--recreate` option to recreate the environments.

### Tests

To run the tests, use the following command:

```bash
pytest
```

To analyze test coverage, use:

```bash
make pytest
```

On Windows:

```powershell
.\scripts\make.ps1 pytest
```

### Type checking

```bash
make type-check
```

On Windows:

```powershell
.\scripts\make.ps1 type-check
```

### Style and formatting

`black` can be used to automatically format code, so you don\'t have to
worry about the nitty-gritty of code style.

```bash
make format-check
```

On Windows:

```powershell
.\scripts\make.ps1 format-check
```

Use `isort` to automatically sort imports.

```bash
make isort-check
```

On Windows:

```powershell
.\scripts\make.ps1 isort-check
```

`flake8` checks some additional things that can't be fixed automatically
with `black`. Run this command to list any issues:

```bash
make lint
```

On Windows:

```powershell
.\scripts\make.ps1 lint
```

To fix `black` and `isort` issues automatically, run:

```bash
make fix
```

On Windows:

```powershell
.\scripts\make.ps1 fix
```

### Documentation

To generate documentation with `sphinx`, run the following command:

```bash
make documentation
```

On Windows:

```powershell
.\scripts\make.ps1 documentation
```

This command will output a local URI which you can open in your browser.

### Github Actions

A pipeline to run tests and checks on Github can be found in `.github/workflows/test-check.yaml`.
This pipeline can be started manually. It will also start automatically for each pull-request.

It checks the code and runs tests on python version 3.11. On Python version 3.9 and 3.10 it also runs and tests the code, but does not do thorough checking.

It is possible to make this succesfull pipeline run a mandatory check of any Pull Request, more info:
[HERE](https://docs.github.com/en/actions/using-workflows/required-workflows)

### Contributing

To contribute, create a pull request.
Before merging, all checks must pass successfully (i.e. the `tox` command).

Please update the `CHANGLELOG.md` and the version in `pyproject.toml` accordingly.

### Publishing

TODO.

It is better that a pipeline is configured that automatically publishes
each new commit to the `main` branch. Every new version should be tagged then as well.

Make sure pyproject.toml's version is updated.
