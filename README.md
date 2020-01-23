# Docs Adtopy (Smartclip) :computer:

Using this combo: **Hugo CMS + docsy theme + github + netlify**

### Step 1

Install Hugo CMS on  [Windows 10](https://imalexissaez.github.io/2018/07/08/instalando-hugo-en-windows/) (TODO: version Linux or Mac)

### Step 2

Fork the repo docsy-theme from Google using the Github UI.

#### Using the GitHub UI

<!--This is the simplest approach, as the Docsy example site repo is a [template repository](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/). To create your own copy of the Docsy example site repo:

1. Go to the [repo page](https://github.com/google/docsy-example) and click **Use this template**.

1. Type your chosen name for your new repository in the **Repository name** field. You can also add an optional **Description**.

1. Click **Create repository from template** to create your new repository. Congratulations, you now have a Docsy site repo!

1. To test your copied site locally with Hugo, or make local edits, you'll also need to make a local copy of your new repository. To do this, use `git clone`, replacing `https://github.com/my/example.git` with your repo's web URL (don't forget to use `--recurse-submodules` or you won't pull down some of the code you need to generate a working site):

    <pre>
    git clone --recurse-submodules --depth 1 <em>https://github.com/my/example.git</em>
    </pre>

You can now edit your local versions of the site's source files. To preview your site, go to your site root directory and run `hugo server`. By default, your site will be available at http://localhost:1313/. To push changes to your new repo, go to your site root directory and use `git push`.-->

Note that the following approach [forks](https://help.github.com/en/articles/fork-a-repo) our repo and so creates a connection in GitHub between your project repo and the Docsy example site project repo - our project will be the "upstream" version of your site project:

1.  In the [the Docsy example site's GitHub repo](https://github.com/google/docsy-example), click **Fork** and follow the prompts.
1.  Rename your new fork:
    1.  Click **Settings**, and type a new name in the **Repository name** field.
    1.  Click **Rename** to save your changes.
1.  Get the web URL for cloning your site repo by clicking **Clone or download** on its main repo page.
1.  Make your own local working copy of your repo using `git clone`, replacing `https://github.com/my/example.git` with your repo's web URL:

    <pre>
    git clone --recurse-submodules --depth 1 <em>https://github.com/my/example.git</em>
    </pre>
    
In our case, should be:

    git clone --recurse-submodules --depth 1 https://github.com/frodriguezsmartclip/docs-adtopy.git

You can now edit your local versions of the site's source files. To preview your site, go to your site root directory and run `hugo server`. By default, your site will be available at http://localhost:1313/. To push changes to your new repo, go to your site root directory and use `git push`.

### Step 3

Configure Netlify with this repo, and tha's it. Magic happens!! :smile:

## Deployment with Netlify

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
