# jupyter-book-autobuild
Autobuild a Jupyter Book and deploy to Github Pages using Github Actions.

With this repo:

- generate your own repo from this template repo;
- place source files — markdown or Jupyter .ipynb documents — in the `content` directory;
- optionally, place a table of contents file, `toc.yml`, at the top level of the repo;
- change the `_config.yml` file so that the `url:` and `baseurl:` settings point to your repo on Github pages:

```
baseurl: YOUR_REPO_NAME/
url: https://YOUR_GITHUB_USERNAME.github.io 
```

When you commit to the `master` branch of your repo:

- if a `toc.yml` file is provided, it will be used to be the book, otherwise, `jupyter book` will generate a table of contents (TOC) file from the contents of the `content` folder;
- `jupyter book` will use the generated TOC file ans the contents of the `content` directory to generate a set of Jekyll source files using settings in the `_config.yml` file;
- the generated Jekyll documentation source fileswill be pushed into a `jupyterbook` branch of your repo;
- Jekyll will run over the contents of the `jupyterbook` branch and a Jekyll documentation site built into the `gh-pages` branch;
- your documentation site should then be viewable at: `YOUR_GITHUB_USERNAME.github.io/YOUR_REPO`
