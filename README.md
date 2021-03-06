# Scrolliris Concept

Code Name: `Willisau /víliʒau/`

[![pipeline status][pipeline]][commit] [![coverage report][coverage]][commit]

[pipeline]: https://gitlab.com/scrolliris/scrolliris-concept/badges/master/build.svg
[coverage]: https://gitlab.com/scrolliris/scrolliris-concept/badges/master/coverage.svg
[commit]: https://gitlab.com/scrolliris/scrolliris-concept/commits/master

```txt
 _               _   _
(_|   |   |_/o  | | | | o
  |   |   |     | | | |     ,   __,
  |   |   |  |  |/  |/  |  / \_/  |  |   |
   \_/ \_/   |_/|__/|__/|_/ \/ \_/|_/ \_/|_/

Willisau; the WILL and our concept Integrated Server Application willisaU
```

The website of [https://try.scrolliris.com/](https://try.scrolliris.com/).


## Repository

https://gitlab.com/scrolliris/scrolliris-concept


## Requirements

* Python `3.5.4` (or `>= 2.7.14`)
* Node.js `8.9.0` (npm `>= 5.6.0`, for build assets)
* [Scrolliris Concept Documentation](https://gitlab.com/scrolliris/scrolliris-concept-documentation) as git subtree


## Integrations

* Google Fonts
* Scrolliris (tracking script)
* Scrolliris (mini-heatmap widget)
* Scrolliris (badge)


## Setup

```zsh
: setup python environment (e.g. virtualenv)
% python3.5 -m venv venv
% source venv/bin/activate
(venv) % pip install --upgrade pip setuptools

: node.js (e.g. nodeenv)
(venv) % pip install nodeenv
(venv) % nodeenv --python-virtualenv --with-npm --node=8.9.0
: re-activate for node.js at this time
(venv) % source venv/bin/activate
(venv) % npm install --global npm@5.6.0
(venv) % npm --version
5.6.0
```

### Dependencies

#### Ettiswil

See article project [Scrolliris Concept Documentation](
https://gitlab.com/scrolliris/scrolliris-concept-documentation) (Ettiswil).

Don't commit directly the changes on above article project into this repo.

```zsh
: setup `doc`
% git remote add concept-documentation https://gitlab.com/scrolliris/scrolliris-concept-documentation.git
% git subtree add --prefix doc/article concept-documentation master

: synchronize with updates into specified branch
% git pull -s subtree -Xsubtree=doc/article ettiswil master

: subtree list
% git log | grep git-subtree-dir | tr -d ' ' | cut -d ":" -f2 | sort | uniq
```


## Development

Use `waitress` as wsgi server.  
See `Makefile`.

```zsh
% cd /path/to/willisau
% source venv/bin/activate

: set env
(venv) % cp .env.sample .env

: install packages
(venv) % ENV=development make setup

: install node modules & run gulp task
(venv) % npm install --global gulp-cli
(venv) % npm install

(venv) % gulp

: run server
(venv) % make serve
```

### Style check & lint

* flake8
* pylint
* eslint

```zsh
: add hook
(venv) % flake8 --install-hook git

: run make check target
(venv) % make check
```


## Deployment

Use `CherryPy` as wsgi server.

```zsh
: run install and start server for production
(venv) % ENV=production make setup

: or start server by yourself
(venv) % ./bin/serve --env production --config config/production.ini --install
```

### Delivery

E.g. Google App Engine

```zsh
: this script install cloud sdk into `./lib` directory
(venv) % ./bin/setup-google-cloud-sdk
```

Above script is equivalent following steps.

```zsh
: take latest sdk from https://cloud.google.com/sdk/downloads
% cd lib
(venv) % curl -sLO https://dl.google.com/dl/cloudsdk/channels/rapid/ \
  downloads/google-cloud-sdk-<VERSION>-linux-x86_64.tar.gz

: check sha256 checksum
(venv) % echo "CHECKSUM" "" ./google-cloud-sdk-<VERSION>-linux-x86_64.tar.gz \
  | sha256sum -c -
./google-cloud-sdk-<VERSION>-linux-x86_64.tar.gz: OK
(venv) % tar zxvf google-cloud-sdk-<VERSION>-linux-x86_64.tar.gz

: setup lib/ as a root for sdk
(venv) % CLOUDSDK_ROOT_DIR=. ./google-cloud-sdk/install.sh
(venv) % cd ../
```

```zsh
: publish website (create `app.yaml`)
(venv) % source ./bin/load-gcloud
(venv) % gcloud app deploy ./app.yaml --project <project-id> --verbosity=info
```

E.g. Heroku

```zsh
(venv) % echo '3.6.X' >> ./runtime.txt
(venv) % git push heroku master
```


## Testing

```zsh
(venv) % make test
```

### CI

You can check it by yourself using `gitlab-ci-multi-runner` on locale machine.
It requires `docker`.

```zsh
% ./bin/setup-gitlab-ci-multi-runner

: use script
% ./bin/ci-runner test
```

#### Links

See documents.

* https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/issues/312
* https://docs.gitlab.com/runner/install/linux-manually.html


## Documentation

TODO


## Translation

TODO


## License

This project is distributed as various licenses by parts.

### Documentation

`GFDL-1.3`

The files in the `willisau/doc` directory are distributed as
GNU Free Documentation License. (version 1.3)

```txt
Permission is granted to copy, distribute and/or modify this document
under the terms of the GNU Free Documentation License, Version 1.3
or any later version published by the Free Software Foundation;
with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
A copy of the license is included in the section entitled "GNU
Free Documentation License".
```

Check the [GNU Free Documentation License](
https://www.gnu.org/licenses/fdl-1.3.en.html).

### Resource (image)

`CC-BY-NC-SA-4.0`

The files in the `beregnz/assets/img` directory are licensed under the
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International
Public License.

[![Creative Commons License](
https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](
http://creativecommons.org/licenses/by-nc-sa/4.0/)

Check the [Legalcode](
https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode).

### Software (program)

`AGPL-3.0`

```
Scrolliris Concept
Copyright (c) 2017 Lupine Software LLC

This is free software: You can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program. If not, see <https://www.gnu.org/licenses/>.
```

See [LICENSE](LICENSE).
