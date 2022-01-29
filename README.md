# 📺 Setup Headless Display Action

Setup a headless display on Linux and Windows (not needed on MacOS)

```yml
- name: Setup headless display
  uses: pyvista/setup-headless-display-action@v1
```

## 🚀 Usage

```yml
name: Tests that require virtual display

on:
  pull_request:
  workflow_dispatch:
  push:
    tags:
      - "*"
    branches:
      - main

jobs:
  test:
    strategy:
      matrix:
        os: [macos-latest, ubuntu-latest, windows-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - name: Setup headless display
        uses: pyvista/setup-headless-display-action@v1
```


### 🖼️ PyVista Example

```yml
name: Workflow that uses PyVista for plotting

on:
  pull_request:
  workflow_dispatch:
  push:
    tags:
      - "*"
    branches:
      - main

jobs:
  test:
    strategy:
      matrix:
        os: [macos-latest, ubuntu-latest, windows-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Setup headless display
        uses: pyvista/setup-headless-display-action@v1

      - name: Setup Python
        uses: actions/setup-python@v1
        with:
          python-version: 3.9

      - name: Install PyVista
        run: pip install pyvista

      - name: Use PyVista
        run: python -c "import pyvista;pyvista.Sphere().plot(screenshot='${{ matrix.os }}-sphere.png')"

      - uses: actions/upload-artifact@v2
        with:
          name: sphere
          path: ${{ matrix.os }}-sphere.png
```
