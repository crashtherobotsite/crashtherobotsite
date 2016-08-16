# Crash the Robot

This is the repository for the blog [Crash the Robot][1]. 

### Installing locally on Ubuntu 14.04

Install rvm:
```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 
\curl -sSL https://get.rvm.io | bash -s stable --rails
```

Activate and install dependencies
```bash
source ~/.rvm/scripts/rvm        # Activate RVM
sudo apt-get install libgmp3-dev # Required for the json gem
gem install bundler              # Ensure bundle is available
bundle install                   # Install jekyll dependencies
```

Build and run the web site. It will autoregenerate automatically.
```bash
bundle exec jekyll serve
```

### Installing locally on Mac

Follow the [GitHub pages instructions][2] for downloading the repository and installing Jekyll locally.

[1]: http://www.crashtherobot.com/ 
[2]: https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/
