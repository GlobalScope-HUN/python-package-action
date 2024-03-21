# python-package-action
Create Python distribution packages: source, wheel and Debian packages

## Usage

### Create Python library packages

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

### Create cross platform Python application packages

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
