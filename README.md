# python-package-action

Create Python distribution packages: source, wheel and Debian packages

## Usage

### Create Python library packages

Will generate source and wheel packages.
In addition, it will create a Debian package for the library using FPM: python3-<library-name>.deb
Upon installing on a Debian system, it will install the library to the system's Python3 environment.

```yaml
jobs:
  package:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: GlobalScope-HUN/python-package-action@v1
        with:
          debian-dist-type: 'library'
```

### Create Python application packages

Will generate source and wheel packages.
In addition, it will create a Debian package for the application using dh-virtualenv: <application-name>.deb

> [!Note]
> The application should have the `debian` directory with the necessary files for the package creation.

```yaml
jobs:
  package:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: GlobalScope-HUN/python-package-action@v1
        with:
          debian-dist-type: 'application'
          debian-dist-command: 'make package'
```

### Create cross-platform Python application packages

Will build the platform dependent packages in a devcontainer using a build script or command.

> [!Note]
> The application should have a `devcontainer.json` configuration with the necessary setup.

```yaml
jobs:
  package:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: GlobalScope-HUN/python-package-action@v1
        with:
          is-cross-platform: 'true'
          debian-dist-type: 'application'
          docker-username: ${{ secrets.DOCKERHUB_USERNAME }}
          docker-password: ${{ secrets.DOCKERHUB_TOKEN }}
          devcontainer-config: 'armhf'
          devcontainer-command: '.devcontainer/build.sh'
```
