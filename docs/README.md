# Training Course Sources

This subdirectory contains the sources for the hybrid cloud and edge
computing training course

This documentation appears on a [GitHub Pages
site](https://training.yobitrust.com) linked to this
repository. Commits to the master branch of this repository will
automatically update the pages website.

## Syntax

Markdown syntax as supported by
[Kramdown](https://kramdown.gettalong.org/) is the primary formatting
for the bulk of the documentation. However, the pages are processed by
[Jekyll](https://jekyllrb.com/), so you can also use Jekyll/Liquid
directives in the sources.

One customized element in this documentation is a code block (from a
file) that contains a "copy to clipboard" button.  The following
directive:

```
{% include code_snippet.md file='code/my_file.py' language=python %}
```

will include `code/my_file.py` as a preformatted code block with a
"copy to clipboard" button in the upper, right corner. The language
option is optional.

## Serving Documentation Locally

When writing documentation, it can be frustrating to run through the
commit, wait, fix with updates on the GitHub Page site. Fortunately,
this documentation can be served locally to shorten the editing
cycle.

First, you **must** have a full Ruby development environment setup on
your machine.

For MacOS, Ruby is available via [Homebrew](https://brew.sh/). If you
use Homebrew, be sure to setup your path to use the ruby executable
from Homebrew and not the default `ruby` on macOS. This can be done
with:

```sh
export PATH="/usr/local/opt/ruby/bin:$PATH"
```

You may want to add this to your `~/.zshrc` script. You should
also make sure that the bundler gem is installed:

```sh
gem install bundler
```

Again, be sure that the `gem` from Homebrew is the one in your
path. Check with `which gem`. 

For other platforms, see the Ruby site for [installation
instructions](https://www.ruby-lang.org/en/documentation/installation/).

Next, clone this repository and move to the `docs` subdirectory of
your local copy.

Install the necessary Ruby gems on your machine.  To avoid a global
installation, you use the following command:

```sh
bundle config set --local path 'vendor/bundle'
bundle install --path vendor/bundle
```

which will install all of the gems into the `vendor/bundle`
subdirectory.  You should only need to run the first command once. The
contents of this directory are ignored by git.

Finally, build and serve the documentation with the following command:

```sh
bundle exec jekyll serve --livereload --baseurl "" --config _config_local.yml,_config.yml
```

The startup logging will indicate the server's URL; this is usually
http://127.0.0.1:4000/.

The double configuration files are required to allow the content to be
served locally and also on GitHub pages without build errors in either
place.

## Live Reload Troubles

If you run into problems with live reload on macOS, there are two
solutions.

The first is to replace the `--livereload` option with `--watch`.
This will recompile the jekyll web site on changes, but not reload
your browser.

Presuming that the live reload is failing with a link error on macOS,
you need to fix your ruby configuration. Be sure that you're using the
`ruby` and `gem` executables from Homebrew and not the macOS default
ones. Then with the correct `gem` executable, install the bundler gem
with `gem install bundler`. This should resolve any issues you're
having. 
