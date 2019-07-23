# New challenges

## jekyll

###  What is jekyll

- Jekyll is a simple, extendable, static site generator. You give it text written in your favorite markup language and it churns through layouts to create a static website.
- Jekyll is written in Ruby
- A gem is code you can include in Ruby projects, It allows you to package up functionality and share it across other projects or with other people
- Gems can perform functionality such as
    - Converting a Ruby object to JSON
    - Pagination
    - Interacting with APIs `what is API : When you use an application on your mobile phone, the application connects to the Internet and sends data to a server. The server then retrieves that data, interprets it, performs the necessary actions and sends it back to your phone. The application then interprets that data and presents you with the information you wanted in a readable way. This is what an API is - all of this happens via API` such as GitHub
    - Jekyll itself is a gem as well as many Jekyll plugins including jekyll-feed, jekyll-seo-tag and jekyll-archives
- A Gemfile is a list of gems required for your site
- Bundler installs the gems in your Gemfile
- It’s not a requirement for you to use a Gemfile and bundler, You only need to install it once — not every time you create a new Jekyll project
- Jekyll is a static site generator so we need Jekyll to build the site before we can view it.
- http://simpleprimate.com/blog/markdown-basics

### How to install

- `sudo apt-get install ruby-full build-essential zlib1g-dev`
- `echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc`
- `echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc`
- `echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc`
- `source ~/.bashrc`
- `gem install jekyll bundler`

if problems happend
- `sudo gem update --system`
- `bundle install`
- `bundle exec jekyll serve`

### How to work
- Working with github pages
    - GitHub Pages is available in public repositories with GitHub Free, and in public and private repositories with GitHub Pro, GitHub Team, GitHub Enterprise Cloud, and GitHub Enterprise Server.
    - You can set up a local version of your Jekyll GitHub Pages site to test changes to your site locally.
    - Requirements
        - We recommend using Bundler to install and run Jekyll, Bundler manages Ruby gem dependencies, reduces Jekyll build errors, and prevents environment-related bugs.
        - To install Bundler, you must install Ruby
            1. Open Terminal
            2. Check whether you have Ruby 2.1.0 or higher installed  
            `ruby --version`
            3. If you don't have Ruby installed  
            [install Ruby 2.1.0 or higher](https://www.ruby-lang.org/en/downloads/).
            4. Install Bundler  
            `gem install bundler`
        - Create a local repository for your Jekyll site
            1. If you haven't already downloaded Git, install it.
            2. Open Terminal.
            On your local computer, initialize a new Git repository for your Jekyll site  
            `git init JEKYLL-SITE-REPOSITORY-NAME`  
            3. Change directories to the new repository you created  
            `cd JEKYLL-SITE-REPOSITORY-NAME`
        - Install Jekyll using Bundler
            - To track your site's dependencies, Ruby will use the contents of your Gemfile to build your Jekyll site
            1. Check to see if you have a Gemfile in your local Jekyll site repository  
            `ls`
            2. If you don't have a Gemfile, open your favorite text editor, such as Atom, and add these lines to a new file: `source 'https://rubygems.org'`
            `gem 'github-pages', group: :jekyll_plugins`
            3. Name the file Gemfile and save it to the root directory of your local Jekyll site repository.
            4. Install Jekyll and other dependencies from the GitHub Pages gem  
            `bundle install`
        - Generate Jekyll site files (optional)
            - To build your Jekyll site locally, preview your site changes, and troubleshoot build errors, you must have Jekyll site files on your local computer. You may already have Jekyll site files on your local computer if you cloned a Jekyll site repository
            - If you don't have a Jekyll site downloaded, you can generate Jekyll site files for a basic Jekyll template site in your local repository
            - If you want to use an existing Jekyll site repository on GitHub as the starting template for your Jekyll site, fork and clone the Jekyll site repository on GitHub to your local computer
            1. If you don't already have a Jekyll site on your local computer, create a Jekyll template site in a new directory  
            `bundle exec jekyll _3.3.0_ new NEW-JEKYLL-SITE-REPOSITORY-NAME`
            2. Navigate into your new site directory  
            `cd NEW-JEKYLL-SITE-REPOSITORY-NAME`
            3. Edit your Gemfile and remove the following line  
            ` "jekyll", "3.3.0"`
            4. In the Gemfile, delete the # at the beginning of this line  
            `gem "github-pages", group: :jekyll_plugins`
            5. Initialize your site directory as a Git repository  
            `git init`
            6. Connect your remote repository on GitHub to your local repository for your GitHub Pages site.  
            `git remote add origin https://github.com/username-or-organization-name/your-remote-repository-name`
            

#### Test

- gem install jekyll bundler
- jekyll new myblog
- cd myblog
- bundle exec jekyll serve
- run a local host from a website

####

- 

## pandoc

### what is pandoc

`If you need to convert files from one markup format into another, pandoc is your swiss-army knife`

### how to install

- `sudo apt-get update`
- `sudo apt-get install pandoc`
- `apt install dpkg`
- `dpkg -L pandoc`
- `pandoc -v`

### How to work

## mkdocs

### What is mkdocs

`MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.`

### How to install

- install python https://www.python.org/downloads/source/
- install pip https://pip.readthedocs.io/en/stable/installing/

### How to work

## gohugo

### What is gohugo

`Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.`

### how to install

- `brew install hugo`
- Prerequisite Tools
    - http://git-scm.com/
    - https://golang.org/dl/

### how to work