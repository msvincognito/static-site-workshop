# Jekyll Workshop - Create your own online portfolio!

This template uses the [jekyll-bootstrap-resume-theme](https://github.com/nscharrenberg/jekyll-bootstrap-resume).
Specifics on the theme (such as the required data structures) can be found on that repository readme.

## Github Actions

If you would want your website to be deployed to github-pages, each time you make a change to your master branch, then you'll need to do some additional permission/authorization steps.

First create a `personal-access-token` on github, [follow the guide provided by github](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) and copy the given access token.

Then go to your github Settings, and open the "Secrets" tab, then create a new secret and name it `JEKYLL_PAT`, and paste the `personal-access-token` that you copied to the value. Then save this, and now whenever you make a change to your master branch, an action will be started to make a new build of your website and deploy it to your github-pages site.

NOTE: This process may take a couple of minutes.
