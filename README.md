# Packaging Python Projects

- Tutorial how to package a simple Python project
- Source: [Packaging Python Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects)
- shows
    - necessary files
    - how to build the package
    - how to use the build package

Start by install the latest version of `pip`

Unix/macOS
```
python3 -m pip install --upgrade pip
```

Windows
``` 
python.exe -m pip install --upgrade pip
```

## A simple project

- simple project with project name `example_project_ST`
- Create the following file structure:
```
PackagingUserGuide/
└── src/
    └── example_package_ST/
        ├── __init__.py
        └── example.py
```

- `__init__.py` recommended as directory can be imported as package. Here: empty
- `example.py` is an example of a moudle with some functionality (functions, classes, constants, etc.)
- run all commands inside this root directory `PackagingUserGuide`

## Creating the package files
```
PackagingUserGuide/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── example_package_ST/
│       ├── __init__.py
│       └── example.py
└── tests/
```

## Creating a test directory

`test/` is a placeholder for test files. Leave it empty for now

## Choosing a buil backend: Here ``setuptools``
- `setuptools` is a build backend which converts source code into a districution package (like a wheel)
- the `pyproject.toml` tells build frontend tools like `pip` which backedn to ise for your project

```
[build-system]
requires = ["setuptools>=61.0]
build-backend = "setuptools.build_meta
```

- `requires`: list of packages needed to build the package. Frontends install them automatically when building the package
- `build-backend`: name of Python object that frontends will use to perform the build

## Configuring metadata
```
[project]
name = "example_package_ST"
version = "0.0.1"
authors = [
  { name="Simon Traub", email="s.traub@sensopart.de" },
]
description = "A small example package"
readme = "README.md"
requires-python = ">=3.12"
classifiers = [
    "Programming Language :: Python :: 3",
    "Operating System :: OS Independent",
    "License :: OSI Approved :: MIT License",
]

[project.urls]
Homepage = "https://github.com/TraubSimon/PackagingUserGuide"
Issues = "https://github.com/TraubSimon/PackagingUserGuide/issues"
```

- `name`: distribution name of the project
- `version`: package version
- `authors`: lists name and email adress to reach the author
- `description`: short, one-sentece summary of the package
- `readme`: path to file containing a detailed description of the package
- `requires-python`: gives the supported python version of your project
- `classifier`: additional metadata about the package. Here: package compatible with Python 3 and OS-Independent
- `license`: SPDX license expression
- `license-file`: list of glob paths to license files relative to the location of `pyproject.toml`
- `urls`: links to source, documentation, issue teacker, etc

See the [pyproject.toml guide](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#writing-pyproject-toml) for details

## Crreating a LICENSE
- important to include a license into every Python Package
-  [Here]( https://choosealicense.com/) you can find help how to chosse a license file
- Here we used MIT license: see `LICENSE` file: 

```
Copyright (c) 2018 The Python Packaging Authority

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```


## Generating distribution archives
- gegenrate a `distribution package` for this example package
- these can be installed via pip
- Run the commands where the `pyproject.toml` is located

Unix/macOS
```
python3 -m build
```

Windows
``` 
python.exe -m build
```

This command should output a lot of textr and once completed should generate two files in the `dist` directory
```
dist/
├── example_package_ST-0.0.1-py3-none-any.whl
└── example_package_ST-0.0.1.tar.gz
```

- `tar.gz`: source distribution
- `.whl`: built distribution


## Install the package with pip
- You can directly install the package via pip
```
pip install $PathToFile$/example_package_ST-0.0.1.tar.gz
``` 
