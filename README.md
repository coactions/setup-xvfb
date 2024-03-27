# XVFB Github Action

This action installs [XVFB](http://elementalselenium.com/tips/38-headless) and runs your headless tests with it. It cleans up the `xvfb` process after your tests are done. If it detects you're **not** using Ubuntu, your tests still run without `xvfb`, which is very practical for multi-platform workflows.

### Example usage

```yml
on: [push]

jobs:
  build:
    strategy:
      matrix:
        os: [macos-latest, ubuntu-latest, windows-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Run headless test
        uses: coactions/setup-xvfb@v1
        with:
          run: npm test
          working-directory: ./ #optional
          options: #optional
```

Modern [GitHub Actions Ubuntu images](https://github.com/actions/runner-images/tree/main/images/ubuntu) now include `xvfb` so this Action could be replaced by:

```yml
- if: startsWith(matrix.os, 'ubuntu')
  run: xvfb-run npm test
- if: "!startsWith(matrix.os, 'ubuntu')"
  run: npm test
```
