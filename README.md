## Installation

```sh
sudo port install rbenv ruby-build
rbenv init
```

Put these in your shell config file (for me, `~/.zshenv`)
```sh
if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi
export PATH="$PATH:$HOME/.gem/ruby/2.7.2/bin"
```

Continuing...
```sh
rbenv install 2.7.2
rbenv global 2.7.2
gem install --user-install bundler jekyll
bundle install
bundle exec jekyll serve --livereload
```

If you have problems with Ruby:
```sh
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
```

## Usage

To remove a post from the list, add to post meta:
```
sitemap: false
```
