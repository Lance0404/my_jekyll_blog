# my_jekyll_blog

* install ruby, bundle and jekyll
```shell
gem install jekyll bundler
```
* draft steps
```shell
git init my_jekyll_blog
jekyll new my_jekyll_blog
cd my_jekyll_blog
# git checkout -b gh-pages
bundle install
bundle update
bundle install
bundle update github-pages
# remember to use the default localhost
bundle exec jekyll serve
# bundle exec jekyll serve --host 0.0.0.0
git remote add origin git@github.com:Lance0404/jekyll_blog.git
git push -u origin master
```
