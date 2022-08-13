# docs-template-site

This is a template site for Sphinx documentation.

## Getting Started

If you have a completely new site, start here.

1. Create a docs directory and add a requirements.txt file:

   ```sh
   mkdir docs
   cd docs
   touch requirements.txt
   ```

1. Add the following to the `requirements.txt` file:

   ```sh
   cat <<EOT >> requirements.txt 
   sphinx==5.0.0
   -e git+https://github.com/pytorch/pytorch_sphinx_theme.git#egg=pytorch_sphinx_theme
   sphinx_design
   sphinx-serve
   EOT
   ```
   
   If you want to be able to use Markdown files, `myst-parser` to that list.

1. If you are using a virtualenv or conda, start your environment. Example for
   virtualenv:
   
   ```sh
   virtualenv venv
   source venv/bin/activate
   ```

1. Install the requirements:

   ```sh
   pip3 install -r requirements.txt
   ```

1. Run sphinx-quickstart and answer all the questions:

   ```sh
   sphinx-quickstart
   ```

   Output:

   ```sh
   > Separate source and build directories (y/n) [n]: y
   > Project name: My Project
   > Author name(s): PyTorch Contributors
   > Project release []: 'release'
   > Project language [en]: en
   ...
   Finished: An initial directory structure has been created.

   ```
1. Check the directory structure:

   ```sh
   tree
   ```
   
   Output:

   ```sh
   .
   ├── README.md
   └── docs
      ├── Makefile
      ├── build
      ├── make.bat
      └── source
          ├── _static
          ├── _templates
          ├── conf.py
          └── index.rst

   5 directories, 5 files
   ```

Next, configure conf.py.

## Configure conf.py

You need add the following minimum settings to the `conf.py` file:

```
import pytorch_sphinx_theme
project = 'MyProject'
copyright = '2022, PyTorch Contributors'
author = 'PyTorch Contributors'
release = 'release'
extensions = [
    'sphinx_design',
]
# optional for markdown support
# source_suffix = ['.rst', '.md']
templates_path = ['_templates']
exclude_patterns = []
html_theme = 'pytorch_sphinx_theme'
html_theme_path = [pytorch_sphinx_theme.get_html_theme_path()]
html_theme_options = {
    "pytorch_project": "myproject",
    "collapse_navigation": True,
    "analytics_id": "UA-117752657-2",
}
html_static_path = ['_static']
```

## Preview Locally

To preview your docs locally, you can run `make html` and `sphinx-serve`.
You'll need to install `sphinx-serve` to be able to preview:
`pip install sphinx-serve`.

1. Test and preview your doc build:

   ```sh
   make html
   sphinx-serve
   ```

Open your browser and go to `http://0.0.0.0:8081` to preview your site.
If you are building into any other directory but `build`, specify that
directory with the `sphinx-serve` command–`sphinx-serve -b <buildir>`.
