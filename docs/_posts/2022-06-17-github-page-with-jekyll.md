---
layout: post
title:  "GitHub Page with Jekyll"
categories: jekyll update
---
This is my first post and I want to record how I set up my gihub page using Jekyll here.

## 1. Installation (on Ubuntu or WSL)
(NOTE: Refer to [here][jekyll-install].)

Install Ruby and other prerequisites:
```shell
$ sudo apt-get install ruby-full build-essential zlib1g-dev
```

Set the RubyGems packages (called gems) installation path to avoid installing gems as the root user:
```shell
$ echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
$ echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
$ echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
$ source ~/.bashrc
```

Install Jekyll and Bundler (gem installer):
```shell
$ gem install jekyll bundler
```
&nbsp;

## 2. GitHub Page Set-up
Check out the full Gihub documentation [here][github-page].
1. Create a repository for your site by the name of `YOUR_ID.github.io` on GitHub and make it public.
  * NOTE: You can choose a specific folder to publish your site from (e.g., docs)  

2. Clone the remote repository to your local environment.
```shell
$ git clone https://github.com/YOUR_ID/YOUR_ID.github.io.git
```

3. Navigate to your publishing source (e.g., docs) and create a new (default) Jekyll site.
```shell
$ jekyll new --skip-bundle .
```

4. Open `GemFile` and replace `gem "jekyll"` with the following:
```shell
gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
```
  * NOTE: You can look up the lastest version of `github-pages` gem on [here](https://pages.github.com/versions/) and replace GITHUB-PAGES-VERSION above with it.

5. Install all the required gems.
```shell
$ bundle install
```

6. Test your site locally
```shell
$ bundle exec jekyll serve --livereload
```
  * NOTE: This will build and make the site running on a local server. `--livereload` option is for automatically refreshing the page with each change.

&nbsp;

## 3. Using Jekyll Themes
Here, the [Basically Basic](https://github.com/mmistakes/jekyll-theme-basically-basic) theme is assumed.  

### Local Hosting
For local hosting, follow the steps below:  
1. Add this line to your Jekyll site's Gemfile:
```shell
$ gem "jekyll-theme-basically-basic"
```
2. Add this line to your Jekyll site's _config.yml file:
```shell
$ theme: jekyll-theme-basically-basic
```
3. Then run Bundler to install the theme gem and dependencies:
```shell
$ bundle install
```

### Remote Hosting
For remote hosting (including GitHub Pages hosted by GitHub), do the following:
1. Replace gem "jekyll" with:
```shell
$ gem "github-pages", group: :jekyll_plugins
```
2. Run bundle update and verify that all gems install properly.

3. Add remote_theme: `"mmistakes/jekyll-theme-basically-basic@1.4.5"` to your `_config.yml` file. Remove any other `theme:` or `remote_theme:` entries.

### CV Page
You can add your CV page by simply upload a JSON file to `_data` folder as '_data/cv.json'. Please refer to [here](https://jsonresume.org/schema/ "JSON-based file standard") for the CV template.

&nbsp;

## Tips & Troubleshooting
* Pagination
  1. Include the jekyll-paginate plugin in your Gemfile.
  ```shell
  group :jekyll_plugins do
  gem "jekyll-paginate"
  end
  ```
  2. Add jekyll-paginate to gems array in your _config.yml file and the following pagination settings:
  ```shell
  paginate: 5  # amount of posts to show per page
  paginate_path: /page:num/
  ```
  3. Create index.html (or rename index.md) in the root of your project and add the following front matter:
  ```shell
  layout: home
  paginate: true
  ```

* Home Image
  * Add `image:[IMAGE_PATH]` to the front matter in 'index.html'.
  ```shell
  image: /assets/images/bench_in_duck_lake_resized.jpg
  ```

* Emoji
  (NOTE: `jemoji` is installed with the `github-pages` gem.)
  * Add the following to your site's `_config.yml`:
  ```yml
  gems:  
    - jemoji
  ```

* Markdown
  * [GitHub basic formatting](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
  * [Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

[gitHub-page]: https://docs.github.com/en/pages
[jekyll-install]: https://jekyllrb.com/docs/installation/ubuntu/