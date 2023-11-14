# Install Jekyll

We use Jekyll to generate static web sites (and GitHub Pages uses it too!).

Official page: [link](https://jekyllrb.com).

## Install Jekyll (Ubuntu)

Bundler requires Ruby version >= 2.3.0, which is the default for Ubuntu 18.04 Bionic and Ubuntu 20.04 Focal

```bash
sudo apt install ruby-dev
sudo gem install bundler jekyll
```

## To be able to serve via Jekyll
Make sure your project has a file called `Gemfile` in its root with the following contents:
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

It is also common practice to have a file called `.gitignore` in the project root with (at least) the following contents:
```
# Jekyll generated
/_site/
/Gemfile.lock
```

## Serve via Jekyll
```bash
bundle exec jekyll serve
```

Now browse to <http://localhost:4000>

## Troubleshooting Jekyll
To install missing components:
```bash
bundle install
```
