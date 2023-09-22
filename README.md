# Welcome to Faradawn's Website
It is nice to meet you!

### Install Jekyll
- Default Mac Ruby 2.6.0 cannot `gem install jekyll`, permission denied. 
```
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
(echo; echo 'eval "$(/usr/local/bin/brew shellenv)"') >> /Users/faradawn/.bash_profile

# Install Ruby
brew install chruby ruby-install xz
ruby-install ruby 3.1.3 
    # Take 5 minutes, compile C


# Enable chruby
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.bash_profile
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.bash_profile
echo "chruby ruby-3.1.3" >> ~/.bash_profile # run 'chruby' to see actual version

# Install jekyll
gem install jekyll
gem install bundler

# Install dependencies 
bundle install
bundle add webrick

# Serve
bundle exec jekyll serve
```


## Add inline katex
- [Stackoverflow](https://stackoverflow.com/questions/27375252/how-can-i-render-all-inline-formulas-in-with-katex)
- Search repo "https://stackoverflow.com/questions/27375252/how-can-i-render-all-inline-formulas-in-with-katex"
- Add `{left: "$$", right: "$$", display: true},`
- Change assets/katex/contrib/auto-render.mjs 
- Change assets/katex/contrib/auto-render.min.js
- Change assets/katex/contrib/auto-render.js