# platon-rlp

[![Join the chat at https://gitter.im/platonnetwork/platon-rlp](https://badges.gitter.im/platonnetwork/platon-rlp.svg)](https://gitter.im/platonnetwork/platon-rlp?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://circleci.com/gh/platonnetwork/platon-rlp.svg?style=shield)](https://circleci.com/gh/platonnetwork/platon-rlp)
[![PyPI version](https://badge.fury.io/py/platon-rlp.svg)](https://badge.fury.io/py/platon-rlp)
[![Python versions](https://img.shields.io/pypi/pyversions/platon-rlp.svg)](https://pypi.python.org/pypi/platon-rlp)
[![Docs build](https://readthedocs.org/projects/platon-rlp/badge/?version=latest)](http://platon-rlp.readthedocs.io/en/latest/?badge=latest)
   

RLP definitions for common Platon objects in Python

Read more in the [documentation on ReadTheDocs](http://platon-rlp.readthedocs.io/). [View the change log](http://platon-rlp.readthedocs.io/en/latest/release_notes.html).

## Quickstart

```sh
pip install platon-rlp
```

## Developer Setup

If you would like to hack on platon-rlp, please check out the [Snake Charmers
Tactical Manual](https://github.com/platonnetwork/snake-charmers-tactical-manual)
for information on how we do:

- Testing
- Pull Requests
- Code Style
- Documentation

### Development Environment Setup

You can set up your dev environment with:

```sh
git clone git@github.com:platon/platon-rlp.git
cd platon-rlp
virtualenv -p python3 venv
. venv/bin/activate
pip install -e .[dev]
```

### Testing Setup

During development, you might like to have tests run on every file save.

Show flake8 errors on file change:

```sh
# Test flake8
when-changed -v -s -r -1 platon_rlp/ tests/ -c "clear; flake8 platon_rlp tests && echo 'flake8 success' || echo 'error'"
```

Run multi-process tests in one command, but without color:

```sh
# in the project root:
pytest --numprocesses=4 --looponfail --maxfail=1
# the same thing, succinctly:
pytest -n 4 -f --maxfail=1
```

Run in one thread, with color and desktop notifications:

```sh
cd venv
ptw --onfail "notify-send -t 5000 'Test failure' 'python 3 test on platon-rlp failed'" ../tests ../platon_rlp
```

### Release setup

For Debian-like systems:
```
apt install pandoc
```

To release a new version:

```sh
make release bump=$$VERSION_PART_TO_BUMP$$
```

#### How to bumpversion

The version format for this repo is `{major}.{minor}.{patch}` for stable, and
`{major}.{minor}.{patch}-{stage}.{devnum}` for unstable (`stage` can be alpha or beta).

To issue the next version in line, specify which part to bump,
like `make release bump=minor` or `make release bump=devnum`. This is typically done from the
master branch, except when releasing a beta (in which case the beta is released from master,
and the previous stable branch is released from said branch).

If you are in a beta version, `make release bump=stage` will switch to a stable.

To issue an unstable version when the current version is stable, specify the
new version explicitly, like `make release bump="--new-version 4.0.0-alpha.1 devnum"`
