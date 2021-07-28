# To edit the website:

1. Clone Repository
2. Install bundler
```
sudo gem install bundler
bundle install
```
3. If you get an error, you may also need to install the following
```
sudo apt install zlib1g
sudo apt install ruby-dev
bundle install
```
4. To preview the website:
```
bundle exec jekyll serve
```
5. Then, in your web browser, navigate to http://localhost:4000.

Note: If you get any warnings from github, you can fix the dependencies in `Gemfile`
