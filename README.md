# ruby.org.au

The `ruby.org.au` site is a static site hosted with Github Pages.

* Content is in `/pages` as ERB templates
* Styles are `/stylesheets`, compiled using compass

## How to Contribute

Want to help? Sweet! We like help. Pull requests are very welcome. Here's how
to get started:

* Fork the repository
* Make some changes (see _Build instructions_ below)
* Push your changes to your fork
* Open a pull request

When you open a pull request, we'd appreciate if you follow some basic
guidelines:

* Describe what you're changing, and more importantly _why_ you're changing it
* Keep the pull request focused on one thing - if you make two different,
  unrelated changes, please separate them into two pull requests
* Some pull requests won't get merged. All changes are reviewed by a committee
  member, and sometimes changes don't fit with the organisation's vision.

## Build instructions

Building and deploying the site is done via rake tasks:

* `rake build:all` (aliased as default) compiles the site into `/site`
* `rake deploy` copies the _committed_ versions of all files in `/site` to the
  root of the `gh-pages` branch

So, your normal process would look something like this:

```
# ... Edit some content in /pages
git add pages/the-awesome-page.html.erb
rake build:all
git add site
git commit -m "Add an awesome page"
rake deploy
git push origin
# BOOM!
```

