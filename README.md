# jupyter-book-autobuild
Autobuild a Jupyter Book and deploy to Github Pages.


Create an account on CircleCI by logging in using Github authentication.

With this repo:

- generate your own repo from this template repo.
- place source files — markdown or Jupyter .ipynb documents — in the `content` directory;
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

When you commit to the `master` branch of your repo, `jupyter book` will generate a table of contents file from the contents of the `content` folder and generate a set of Sphinx source files using settings in the `_config.yml` file, putting the created files into a `jupyterbook` branch of your repo; Sphinx will then be run over the contents of the `jupyterbook` branch and a Sphinx documentation site built into the `gh-pages` branch. Your documentation site should then be viewable at: `YOUR_GITHUB_USERNAME.github.io/YOUR_REPO`
