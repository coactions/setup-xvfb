# XVFB Github Action

This action installs [XVFB](http://elementalselenium.com/tips/38-headless) and runs your headless tests with it. It cleans up the xvfb process after your tests are done.

## Support

- `ubuntu-latest`: Supported, but not required, because the image already [includes xvfb](https://github.com/actions/runner-images/blob/main/images/linux/Ubuntu2204-Readme.md?rgh-link-date=2023-09-07T09%3A28%3A22Z)
- `windows-latest`: Supported
- `macos-latest`: Supported

## Example usage

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
        uses: actions/checkout@v2
      - name: Run headless test
        uses: coactions/setup-xvfb@v1
        with:
          run: npm test
          working-directory: ./ #optional
          options: #optional
```
