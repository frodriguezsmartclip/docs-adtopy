# :computer: Docs Adtopy (Smartclip)

Using this combo: **[Hugo CMS](https://github.com/gohugoio/hugo) + [docsy theme](https://github.com/google/docsy-example) + github + netlify** :star:

[![Netlify Status](https://api.netlify.com/api/v1/badges/0497bbba-6424-4317-83ea-932fefdb490a/deploy-status)](https://app.netlify.com/sites/docs-adtopy/deploys) ![GitHub repo size](https://img.shields.io/github/repo-size/frodriguezsmartclip/docs-adtopy) ![GitHub](https://img.shields.io/github/license/frodriguezsmartclip/docs-adtopy) ![Netlify](https://img.shields.io/netlify/0497bbba-6424-4317-83ea-932fefdb490a?label=netlify%20workflow) ![Website](https://img.shields.io/website?label=status%20web%20docs-adtopy&url=https%3A%2F%2Fdocs-adtopy.netlify.com%2F)

## Step 1

Install [Hugo CMS](https://gohugo.io/getting-started/quick-start/) on  [Windows 10](https://imalexissaez.github.io/2018/07/08/instalando-hugo-en-windows/) (TODO: version Linux or Mac [getting started hugo (oficial site)](https://gohugo.io/getting-started/installing/))

## Step 2

Fork the repo docsy-theme from Google using the Github UI.

### Using the GitHub UI

Note that the following approach [forks](https://help.github.com/en/articles/fork-a-repo) our repo and so creates a connection in GitHub between your project repo and the Docsy example site project repo - our project will be the "upstream" version of your site project:

1. In the [the Docsy example site's GitHub repo](https://github.com/google/docsy-example), click **Fork** and follow the prompts.
1. Rename your new fork:
    1. Click **Settings**, and type a new name in the **Repository name** field.
    1. Click **Rename** to save your changes.
1. Get the web URL for cloning your site repo by clicking **Clone or download** on its main repo page.
1. Make your own local working copy of your repo using `git clone`, replacing `https://github.com/my/example.git` with your repo's web URL:

```git
git clone --recurse-submodules --depth 1 https://github.com/my/example.git
```

In our case, should be:

```git
git clone --recurse-submodules --depth 1 https://github.com/frodriguezsmartclip/docs-adtopy.git
```

You can now edit your local versions of the site's source files. To preview your site, go to your site root directory and run `hugo server`. By default, your site will be available at <http://localhost:1313/>. To push changes to your new repo, go to your site root directory and use `git push`.

## Step 3

Configure Netlify with this repo, and tha's it. Magic happens!! :smile:

### Deployment with Netlify

We recommend using [Netlify](https://www.netlify.com/) as a particularly simple way to serve your site from your Git provider (GitHub, GitLab, or BitBucket), with [continuous deployment](https://www.netlify.com/docs/continuous-deployment/), previews of the generated site when you or your users create pull requests against the doc repo, and more. Netlify is free to use for Open Source projects, with premium tiers if you require greater support.

Follow the instructions in [Host on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/) to set up a Netlify account (if you don't have one already) and authorize access to your GitHub or other Git provider account. Once you're logged in:

1. Click **New site from Git**.
1. Click your chosen Git provider, then choose your site repo from your list of repos.
1. In the **Deploy settings** page:
   1. For your **Build command**, specify `cd themes/docsy && git submodule update -f --init && cd ../.. && hugo`. You need to specify this rather than just `hugo` so that Netlify can use the theme's submodules.
   1. Click **Show advanced**.
   1. In the **Advanced build settings** section, click **New variable**.
   1. Specify `HUGO_VERSION` as the **Key** for the new variable, and `0.53` or later as its **Value**.
1. Click **Deploy site**.

If you have an existing deployment you can view and update the relevant information by selecting the site from your list of sites in Netlify, then clicking **Site settings** - **Build and deploy**. Ensure that **Ubuntu Xenial 16.04** is selected in the **Build image selection** section - if you're creating a new deployment this is used by default. You need to use this image to run the extended version of Hugo.

Si todo ha ido bien, enhorabuena, tenemos **Docs-Adtopy** configurado con Netlify para hacer desarrollo continuo apoyándonos en GitHub + Netlify. :white_check_mark:

:link: La URL del proyecto de documentación está accesible en: [Docs-Adtopy web en Netlify](https://docs-adtopy.netlify.com/)

:link: Documentación oficial de [**Docsy Theme**](https://www.docsy.dev/docs/)
