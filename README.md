# jupyter-book-autobuild
Autobuild a Jupyter Book and deploy to Github Pages.


Create an account on CircleCI by logging in using Github authentication.

With this repo:

- generate your own repo from this template repo;
- edit the `master` branch `.circleci/config.yml`: in the two locations where the `ghp-import` command is issued, change the `https://${GITHUB_PERSONAL_TOKEN}@github.com/ouseful-testing/jupyter-book-autobuild` line to `https://${GITHUB_PERSONAL_TOKEN}@github.com/YOUR_GITHUB_USERNAME/YOUR_REPO`; [TO DO: can we autodetect these and insert them automatically? Or perhaps set them via additional environment variables?]
- place source files — markdown or Jupyter .ipynb documents — in the `content` directory;
- optionally, place a table of contents file, `toc.yml`, at the top level of the repo;
- change the `_config.yml` file so that the `url:` and `baseurl:` settings point to your repo on Github pages:

```
baseurl: YOUR_REPO_NAME/
url: https://YOUR_GITHUB_USERNAME.github.io 
```

In CircleCI:

- add a project based on your repo; (?? need some permission granting in Github over what organisation repos are visible to CircleCI if you have several organisations associated with your account? Via the [Github OAuth Applications](https://github.com/settings/connections/applications/) page, select `CircleCI` and grant access over the desired organisations ).

In Github:

- create a *Personal Access Token* from your user `Settings > Developer Settings > Personal Access Tokens` and check the appropriate scope (`repo > public_repo`); copy the token;

In CircleCI:

- select the project associated with your repo, go to the settings (cog icon), select *Build Settings > Environment Variables*, and create an environment variable `GITHUB_PERSONAL_TOKEN` using the Github Personal Access Token you just created.

When you commit to the `master` branch of your repo:

- if a `toc.yml` file is provided, it will be used to be the book, otherwise, `jupyter book` will generate a table of contents (TOC) file from the contents of the `content` folder;
- `jupyter book` will use the generated TOC file ans the contents of the `content` directory to generate a set of Jekyll source files using settings in the `_config.yml` file;
- the generated Jekyll documentation source fileswill be pushed into a `jupyterbook` branch of your repo;
- Jekyll will run over the contents of the `jupyterbook` branch and a Jekyll documentation site built into the `gh-pages` branch;
- your documentation site should then be viewable at: `YOUR_GITHUB_USERNAME.github.io/YOUR_REPO`
