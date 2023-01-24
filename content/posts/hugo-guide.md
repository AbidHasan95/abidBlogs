---
title: "Hugo Guide"
date: 2022-12-31T21:43:59+05:30
tags: ["Hugo","PaperMod"]
showToc: true
# UseHugoToc: true
---
## Installation
### Installing the library

Install hugo using the appropriate package manager

For nix package manager
```bash
nix-env -iA nixpkgs.hugo
```
## Configuration
### Creating new project
Initialise a new hugo site. Create the folder structure for the hugo project

```bash
hugo new site abidBlogs
cd abidBlogs
```
### Git initialisation and adding Theme

Initialise the project as a git repo and add an appropriate theme. (optional) change the branch name from `master` to `main`.
Browse themes here: https://themes.gohugo.io/
```bash
git init
git branch -m main
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

The theme name needs to be updated in the `config.toml` file as well
```bash
echo "theme = 'PaperMod'" >> config.toml
```
## Customisation
### Override partials
To override a particular partial (eg. Table of contents), create custom files under `layouts`. Use whatever folder structure is followed in the theme. To apply additional css files, override the `head.html` partial and add imports for additional css in the file. Some themes also allow extra css to be added/bundled as an extension to its own css file. eg. In `PaperMod` add additional css files in `assets/css/extended/my_custom_stylesheet.css`. The css file(s) can be named anything.

## Preview
### Start the server
Starts the server in your local environment. You can preview the changes in your browser.
```bash
hugo server
```

## FAQs

[Can we use our Dockerfile to build an image and deploy it in netlify](https://answers.netlify.com/t/can-we-use-our-dockerfile-to-build-an-image-and-deploy-it-in-netlify/26996)
